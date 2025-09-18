---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Virtual FAQ/02 Build/"}
---

# Índice

[[#Fase de construcción de un agente de almacén de datos]]
[[#Fuentes de datos para almacenes de datos]]
[[#Conectores de datos en agentes conversacionales]]
[[#Conectar a un agente]]
[[#Configuraciones de búsqueda avanzada]]
[[#Problemas comunes y soluciones]]

---
# Fase de construcción de un agente de almacén de datos

Después de definir el alcance y el diseño, el siguiente paso es la fase de construcción, que comienza con la elección del tipo de almacén de datos.

#### **Tipos de almacenes de datos y sus fuentes**

Hay tres tipos principales de almacenes de datos, cada uno con diferentes fuentes y mecanismos de entrada:

1. **Datos web:** Para contenido público, como sitios web.
    
2. **Datos no estructurados:** Para contenido privado, como documentos PDF o HTML sin un formato fijo.
    
3. **Datos estructurados:** Para contenido privado, organizado en un formato específico, como preguntas y respuestas.
    

Aunque hay 3 tipos de almacenes, existen 10 fuentes de datos posibles.

- **Para datos web:** La única fuente es una URL de un sitio web público.
    
- **Para datos estructurados o no estructurados (privados):** Las fuentes pueden ser BigQuery, Google Cloud Storage, Google Drive, Cloud SQL, Spanner, Bigtable, Firestore o API.
    

---

### **Tipos de almacenes de datos en detalle**

1. **Almacenes de datos web (`Website data stores`)**
    
    - **Cómo funcionan:** Utilizan un rastreador de búsqueda que indexa el contenido de una URL pública.
        
    - **Consideraciones:**
        
        - Los archivos PDF en el sitio web también son indexados.
            
        - Existe un límite de **1 millón de documentos** por almacén. Si tu sitio excede este límite, debes considerar otra opción.
            
        - El rastreador respeta el archivo `robots.txt`, por lo que solo indexará las URLs permitidas.
            
2. **Almacenes de datos no estructurados (`Unstructured data stores`)**
    
    - **Cómo funcionan:** Permiten subir datos sin una estructura fija, como PDF o HTML.
        
    - **Con metadatos:** **Altamente recomendado**. Se suben archivos JSONL, donde cada línea es un objeto JSON que describe un documento (con su ID, URI, título y URL opcionales).
        
    - **Sin metadatos:** Es más simple, solo se suben los archivos directamente. Sin embargo, no se usarán los títulos de los documentos para la indexación o recuperación.
        
    - **Límite:** El tamaño máximo por documento es de 100 Megabytes.
        
3. **Almacenes de datos estructurados (`Structured data stores`)**
    
    - **Cómo funcionan:** Almacenan información en un formato organizado (esquema) como preguntas y respuestas, títulos y URLs.
        
    - **Usos:** Ideales para preguntas frecuentes (FAQs). Cuando una pregunta del usuario coincide con una pregunta del almacén con alta confianza, el agente devuelve la respuesta correspondiente sin modificaciones.
        
    - **Formato de subida:** Los datos deben estar en formato **CSV**, con un encabezado que describa las columnas (ej., `question, answer, title, URL`). Los campos `title` y `URL` son opcionales.

---

# Fuentes de datos para almacenes de datos

La elección de la fuente de datos depende de si necesitas usar información pública o privada y del formato de tus datos.

#### **1. Sitios web públicos** 🌐

- **Uso:** Para contenido disponible públicamente en internet.
    
- **Implementación:**
    
    - Identifica la **URL** principal del sitio web.
        
    - Puedes **incluir o excluir** URLs específicas o patrones usando **comodines** (como `*`).
        
    - **Verificación de dominio:** Es **obligatorio** verificar que eres el propietario del dominio. Esto se hace a través de la consola de Búsqueda de Google. Si no es posible, se puede solicitar una excepción.
        
- **Limitaciones:**
    
    - El rastreo respeta el archivo `robots.txt`.
        
    - Límite de **1 millón de documentos** indexados por almacén.
        
- **Excepciones:**
    
    - **Búsqueda básica en sitios web:** Para información pública de sitios gubernamentales.
        
    - **Solicitud de exención:** Si la información no es pública pero no puedes verificar la propiedad, puedes solicitar una exención (requiere justificación).
        

#### **2. Cloud Storage** ☁️

- **Uso:** Para contenido **privado**, ya sean documentos **estructurados** o **no estructurados**.
    
- **Para datos no estructurados:**
    
    - Sube archivos (PDF, HTML) a un bucket de Cloud Storage.
        
    - **Recomendado:** Usa archivos **JSONL** con **metadatos** (título, URL) para mejorar la recuperación.
        
    - **Sin metadatos:** Más simple, pero la recuperación es menos precisa y el agente usará una URL genérica para el archivo.
        
    - **Límite:** Tamaño máximo de documento de 100 MB.
        
- **Para datos estructurados (FAQs):**
    
    - Los datos deben estar en formato **NDJSON** o **JSON Lines** (preguntas y respuestas).
        
    - Crea el almacén de datos especificando el nombre y la ubicación (URI) del archivo/carpeta en Cloud Storage.
        

#### **3. BigQuery** 📊

- **Uso:** Para datos **estructurados** o **no estructurados** (privados).
    
- **Implementación:**
    
    - Proporciona la ruta a la fuente de datos en BigQuery.
        
    - Puedes elegir si la sincronización es única o periódica.
        
    - Define si los datos son estructurados o no estructurados, y si incluyen metadatos (que definen si los campos son indexables, buscables, etc.).
        
- **Limitación:** Los almacenes de datos de BigQuery **no convierten las solicitudes en consultas SQL**. Solo realizan búsquedas directas, lo que puede afectar la precisión en operaciones analíticas complejas (agregaciones, filtros).

![](https://i.imgur.com/WYaADkn.png)

---

# Conectores de datos en agentes conversacionales

Los conectores permiten a los agentes conversacionales interactuar con fuentes de datos externas y realizar acciones en ellas. Hay dos tipos principales:

1. **Fuentes de Google:** Como Google Calendar, Google Sites, Google Storage o BigQuery.
    
2. **Fuentes de terceros:** Sistemas externos que también pueden ser integrados.
    

**Consideraciones importantes:**

- **Acceso restringido:** Algunas fuentes de Google y conectores de terceros requieren **listas blancas (`allowlisting`)** o licencias específicas (como la licencia Agentspace para conectores de Workspace y terceros). Para acceder, se debe solicitar una aprobación.
    
- **Permisos:** La integración no otorga acceso adicional al que ya se tiene. El agente solo podrá acceder a la información que el usuario que interactúa con él tiene permiso para ver.
    
- **Entrenamiento de modelos:** La información accedida a través de los conectores **no se usará** para entrenar modelos de Google.
    

---

### **Partes de una integración**

La mayoría de las integraciones constan de dos partes:

- **Almacenes de datos (`Data stores`):** Permiten **consultar información** (ej., obtener el historial de reuniones de Google Calendar).
    
- **Acciones (`Actions`):** Permiten **realizar cambios** o ejecutar funciones (ej., crear una reunión en Google Calendar).
    

---

### **Pasos para crear un conector**

Existen tres pasos principales para configurar un conector y un almacén de datos asociado:

1. **Configurar un proveedor de identidad:**
    
    - **Propósito:** Autenticar y autorizar al agente para acceder al sistema externo.
        
    - **Opciones:**
        
        - **Google Identity:** Los usuarios inician sesión con sus credenciales de Google (Gmail, Google Workspace). Se puede usar IAM para asignar accesos. Si se usa directamente con Google Cloud, la identidad de Google está integrada.
            
        - **Proveedor de identidad de terceros:** Los usuarios usan credenciales no-Google. Requiere crear un **Pool de Identidad de Trabajo (`Workforce Identity Pool`)** en Google Cloud y configurar el proveedor (ej., Okta). Se usa IAM para asignar permisos. **No aplica para proyectos @google.com.**
            
2. **Configurar el conector:**
    
    - Cada conector puede contener múltiples almacenes de datos, que se guardan como entidades en el sistema conversacional.
        
    - Si usas un proveedor de identidad de terceros, necesitas crear el Pool de Identidad de Trabajo y configurar el proveedor en la consola de **Identidad de Trabajo (`Workforce Identity Federation`)**.
        
    - Luego, en la consola de IAM, asigna permisos como `Dialogflow API Admin` y `Discovery Engine Viewer` al pool.
        
    - En la consola de **AI Applications**, configura la autenticación por defecto (global o por ubicación), eligiendo entre tu identidad de Google o la de terceros (vinculando el Pool de Identidad de Trabajo creado).
        
3. **Crear el almacén de datos:**
    
    - En la consola de **AI Applications**, crea un nuevo almacén de datos.
        
    - Selecciona tu proveedor de terceros (ej., Salesforce).
        
    - Configura los detalles específicos de la integración (ej., `Client ID`, `secret`, URL de la instancia).
        
    - Elige las identidades a sincronizar (que se representarán como **Entidades de Agente Conversacional**).
        
    - Selecciona la **ubicación** correcta (ej., Global).
        
    - Define un nombre y la **frecuencia de sincronización** (ej., diaria, cada 3 o 5 días).
        
    - Puedes ver el historial de sincronización en la pestaña **`Data Ingestion`**.

---

# Conectar a un agente

### **1. Conectar el almacén de datos** 🔗

Existen dos formas de conectar un almacén de datos a un agente:

- **En la interfaz de Conversational Agents:**
    
    1. Ve a la página del agente donde deseas agregar el almacén.
        
    2. Haz clic en **"Edit data stores"**. Si no ves esta opción, agrega el manejador de estado **"Data stores"** a la página.
        
    3. Una vez allí, puedes seleccionar un almacén de datos existente o crear uno nuevo. Recuerda que el almacén de datos debe estar en la misma **región** que el agente.
        
- **A través del manejador de estado:**
    
    - Una vez que el almacén de datos está conectado, el parámetro `$request.knowledge.answers` se agrega automáticamente a la sección **"Agent responses"** para que el agente devuelva las respuestas del almacén. Puedes configurar el **número máximo de enlaces** a incluir en la respuesta, con un máximo de **5**.
        

---

### **2. Configurar el comportamiento de IA generativa** 🤖

Puedes personalizar el comportamiento del agente de IA generativa en la sección **"Generative AI"** de la configuración del agente.

- **Frases prohibidas (`Banned phrases`):** Agrega frases que, si aparecen en la consulta del usuario o en la respuesta del modelo, harán que el agente revierta a una opción de reserva (_fallback_).
    
- **Configuración de seguridad:** Personaliza los niveles de seguridad para cuatro categorías: **discurso de odio**, **contenido peligroso**, **contenido sexualmente explícito** y **acoso**. Cada una tiene tres niveles: `Block some`, `Block few` y `Block most`.
    
- **Seguridad de la consulta (`Prompt security`):** Habilita esto para que el agente verifique la consulta del usuario y se proteja contra ataques de inyección.
    
- **Confianza de la fundamentación (`Grounding confidence`):** Esto mide qué tan seguro está el modelo de que su respuesta está respaldada por la información en los almacenes de datos. Puedes establecer el **nivel mínimo de confianza** que deseas aceptar. Si una respuesta tiene una confianza por debajo de este umbral, el agente no la mostrará y podría usar un _fallback_.
    
- **Identidad del agente (`Data store prompt`):** Personaliza la **identidad** del agente, como el nombre y la compañía, para asegurar que las respuestas se ajusten a la persona y objetivos del agente.
    

---

### **3. Personalizar respuestas con información del usuario** 🧑‍💼

Puedes personalizar las respuestas del agente añadiendo información sobre el usuario final. Esto se puede hacer de dos maneras:

1. **A través de la API:** Pasa la información en formato **JSON** en cada solicitud `detectIntent` utilizando el campo `queryParams.endUserMetadata`.
    
2. **Con Conversational Messenger:** Usa el método `set context` para enviar la información solo una vez por sesión.

---

# Configuraciones de búsqueda avanzada

Puedes modificar el comportamiento de las solicitudes de búsqueda utilizando **controles de servicio (`serving controls`)**. Para que un control funcione, debes crearlo y luego adjuntarlo a una configuración de servicio (`serving config`). Un control no tiene efecto si no está adjunto a ninguna configuración de servicio.

Estos controles son configuraciones avanzadas que requieren interactuar directamente con la API.

---

### **Tipos de controles**

Existen dos tipos principales de controles de búsqueda:

- **Control de Impulso (`Boost`):** Modifica el orden de los resultados de búsqueda. Puede **promover** o **degradar** resultados para que aparezcan más arriba o más abajo, respectivamente.
    
- **Control de Filtro (`Filter`):** Especifica los requisitos que un documento debe cumplir para ser incluido en la respuesta. Si un documento no cumple la condición, se **excluye** de los resultados.
    

---

### **Configuraciones adicionales**

Puedes añadir los siguientes elementos a un control para definir cuándo debe aplicarse:

- **`queryTerms`:** Permite que el control se active solo cuando se buscan consultas específicas.
    
- **`activeTimeRange`:** Define un período de tiempo (inicio y fin) durante el cual el control estará activo.
    

---

### **Sintaxis de la expresión de filtro**

Un control de filtro utiliza una sintaxis de expresión específica. Por ejemplo, la condición de un filtro se define con el `DATASTORE_ID` (el nombre completo del almacén de datos) y una **condición** que sigue la sintaxis de expresiones de filtro de la plataforma de AI Applications.


---

# Problemas comunes y soluciones

- **La consulta es apropiada pero no devuelve una respuesta:** 🚫
    
    - **Solución:**
        
        - Añade más contenido relevante al almacén de datos.
            
        - Añade **personalización** a las respuestas del agente.
            
        - Ajusta las configuraciones de la IA generativa: cambia el modelo, ajusta el nivel de fundamentación (`grounding level`) o modifica la persona del agente.
            
- **La consulta es inapropiada pero devuelve una respuesta:** 🤡
    
    - **Solución:**
        
        - Elimina contenido del almacén de datos.
            
        - Añade personalización.
            
        - Ajusta las configuraciones de IA generativa.
            
- **Error de "permiso denegado":** 🔑
    
    - **Solución:** Asegúrate de que los usuarios o grupos de usuarios tengan los permisos necesarios.
        
    - Existen dos roles: **Editor** para hacer cambios en la interfaz y **Lector** para solo visualizar el sistema.
        
- **El agente no devuelve respuestas:** ⏳
    
    - **Problema:** A menudo, esto ocurre porque el sitio web o los documentos aún no han terminado de indexarse. Durante la indexación, el agente no puede conversar sobre la información que se está procesando.
        
    - **Solución:** Verifica el estado de la indexación en la consola de **Vertex AI Applications**.
        
- **El sitio web es demasiado grande:** 📖
    
    - **Problema:** Los almacenes de datos tienen un límite máximo de **1,000,000 de documentos por proyecto**. Si un sitio web es demasiado grande, puede exceder este límite.
        
    - **Solución:** Usa **filtros** para limitar el número de documentos a indexar o reduce el alcance de la búsqueda. Si necesitas indexar más de 200,000 páginas, contacta a Google.
        
- **Respuestas no fundamentadas (`ungrounded`):** 🧠
    
    - **Problema:** El agente de almacén de datos incluye una verificación de **fundamentación** para asegurar que las respuestas se basen en las fuentes de datos. Un resultado no fundamentado significa que la información en la respuesta no se puede encontrar en las fuentes. Esto puede llevar a **alucinaciones**.
        
    - **Solución:** La mejor práctica es primero ajustar el contenido del almacén de datos. Si eso no funciona, puedes considerar reducir el umbral de fundamentación, aunque esto aumenta el riesgo de alucinaciones.
        
- **Cuota de documentos agotada:** 📈
    
    - **Problema:** Tu proyecto alcanzó el límite de 1,000,000 de documentos.
        
    - **Solución:** Reduce el alcance de tus fuentes de datos o solicita un aumento de la cuota.
        
- **Otros problemas:** ❗
    
    - Si encuentras problemas como fallas en las llamadas de búsqueda, fallas en los turnos de ReAct o activaciones de la seguridad de IA responsable, y ninguna de las soluciones anteriores funciona, contacta al soporte de la nube. Para ello, crea un caso de soporte y proporciona el ID del proyecto, ID del chat engine, ID del agente, la consulta realizada y el resultado esperado.