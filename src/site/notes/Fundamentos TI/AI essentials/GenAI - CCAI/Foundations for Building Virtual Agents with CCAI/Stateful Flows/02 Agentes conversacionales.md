---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Stateful Flows/02 Agentes conversacionales/"}
---

# Índice

[[#Creando Agentes Conversacionales desde cero]]
[[#Entidades Conceptos Fundamentales]]
[[#Creando y gestionando Intenciones (`Intents`)]]
[[#Mejores prácticas para la optimización de intenciones y entidades]]

---
# Creando Agentes Conversacionales desde cero

Un **agente conversacional** es un agente virtual que maneja conversaciones con los usuarios. Funciona con un modelo de comprensión del lenguaje natural (NLU) que traduce texto o audio a datos estructurados para que tus aplicaciones los entiendan.

#### **Proceso de creación**

1. **Abre la Consola de Conversational Agents:** El primer paso es acceder a la plataforma de Google Cloud.
    
2. **Crea o selecciona un proyecto:** Elige el proyecto de Google Cloud en el que trabajarás.
    
3. **Haz clic en "Crear agente":** En la consola, selecciona la opción para crear uno nuevo.
    
4. **Elige el tipo de agente:**
    
    - **"Use a prebuilt agent":** Si quieres usar un agente ya configurado.
        
    - **"Build your own":** Si quieres tener control total sobre la experiencia. Esta es la opción para empezar desde cero.
        
    - **"Create a Q&A agent":** Para crear un agente de preguntas y respuestas basado en una URL.
        
5. **Configura el agente:** Asigna un nombre, una ubicación, una zona horaria y un idioma.
    
6. **Crea el agente:** Una vez configurado, haz clic en "Crear".
    

#### **Explorando la Consola**

Una vez que el agente está creado, serás llevado a la consola principal, que tiene varias secciones:

- **Pestañas de "Build" y "Manage":**
    
    - La pestaña **"Build"** es donde pasas la mayor parte del tiempo trabajando en flujos, _Playbooks_, etc.
        
    - La pestaña **"Manage"** se usa para gestionar otros recursos, como intenciones, entidades y _webhooks_.
        
- **Sección de "Flows":** Aquí verás el "Default Start Flow", que es el flujo principal a menos que tengas un agente más complejo con múltiples flujos.
    
- **"Graph settings":** Te permite cambiar la vista de la configuración de tu agente, mostrando la relación entre las páginas que has creado.
    
- **"Task indicator":** Un icono que te muestra si hay alguna tarea en curso, como el entrenamiento del agente.
    
- **"Agent settings":** Aquí puedes configurar detalles como el nombre del agente, la zona horaria, el idioma y las configuraciones de voz.
    
- **"Test agent":** Abre el panel del **Simulador**, donde puedes interactuar con tu agente escribiendo o hablando. El panel de la derecha se adapta para mostrar la información relevante según lo que hayas seleccionado.

---

# Entidades: Conceptos Fundamentales

Las **entidades** son piezas de información clave que un agente conversacional extrae de las frases del usuario. Piense en ellas como los datos específicos que necesita para completar una tarea. Hay tres términos principales para entender cómo funcionan:

- **Tipo de entidad (`Entity type`):** La categoría general a la que pertenece la información.
    
    - **Ejemplo:** `vegetal`, `color`, `fecha`.
        
- **Entrada de entidad (`Entity entry`):** Una palabra o frase específica dentro de la categoría.
    
    - **Ejemplo:** `zanahorias`, `cebollas verdes`, `remolachas`.
        
- **Sinónimos de entidad (`Entity synonyms`):** Palabras o frases que significan lo mismo que una entrada de entidad.
    
    - **Ejemplo:** Para la entrada `cebollas verdes`, los sinónimos podrían ser `cebollines` o `cebolletas`.
        

### **Tipos de Entidades**

Existen dos tipos principales de entidades que puedes usar:

- **Entidades del sistema (`System entities`):** Son entidades preconstruidas por Conversational Agents para extraer información común. Sus nombres siempre comienzan con `$sys.`.
    
    - **Ejemplos:** `$sys.color`, `$sys.date`, `$sys.number`.
        
    - **Nota:** La disponibilidad de estas entidades puede variar según el idioma y la región.
        
- **Entidades personalizadas (`Custom entities`):** Te permiten crear tus propias entidades para necesidades específicas de tu negocio.
    
    - **Ejemplo:** Un tipo de entidad `producto-telefonia` para un agente de telecomunicaciones.
        

### **Cómo Crear Entidades Personalizadas**

Para crear una entidad personalizada, sigue estos pasos:

1. Ve a la pestaña **"Manage"** en la consola de Conversational Agents.
    
2. Haz clic en el botón **"Create"**.
    
3. Ingresa un **nombre visible (`display name`)** para el tipo de entidad.
    
4. Agrega las **entradas de entidad** y sus **sinónimos** correspondientes.
    

También hay opciones avanzadas para crear entidades de maneras diferentes:

- **Entidades de expresión regular (`Regular expression entities`):** Te permiten definir entidades usando expresiones regulares, útiles para formatos específicos como un PIN de cuatro dígitos.
    
- **Entidades compuestas (`Composite entities`):** Son un tipo especial de entidad personalizada que contiene otras entidades. Puedes crearlas seleccionando la opción "Entities only (no synonyms)".
    
    - **Ejemplo:** Una entidad `producto` que contiene las entidades `fruta` y `vegetal`.

---

# Creando y gestionando Intenciones (`Intents`)

Las intenciones son la forma en que el agente conversacional agrupa las frases de los usuarios con el mismo propósito. El proceso para crearlas se realiza en la consola y consta de varios pasos.

#### **Proceso de creación**

1. **Navegación:** Ve a la pestaña **"Manage"** y selecciona **"Intents"**.
    
2. **Creación:** Haz clic en el botón **"Create"** para añadir una nueva intención.
    
3. **Configuración:**
    
    - **Nombre:** Dale un nombre descriptivo (ej., `intencion-principal-item-supermercado`).
        
    - **Etiqueta (`Label`):** Agrega una etiqueta (ej., `contextual`) para describir el tipo de intención.
        
    - **Descripción:** Escribe una breve descripción del propósito de la intención.
        
4. **Frases de entrenamiento (`Training phrases`):**
    
    - Agrega frases que representen lo que un usuario diría para activar esta intención.
        
    - **Etiqueta entidades:** Dentro de estas frases, puedes etiquetar las entidades que definiste previamente (por ejemplo, `producto` o `número`). Para hacerlo, selecciona la palabra o frase y elige el tipo de entidad que quieres asociar.
        
    - **Parámetros:** A cada entidad etiquetada se le asigna una etiqueta de parámetro (`Parameter id`), que se usa para identificar el valor extraído en la conversación.
        

#### **Intenciones por defecto**

Al crear un nuevo agente, hay dos intenciones que vienen por defecto:

- **`Default Welcome Intent`:** Se usa para saludar al usuario al comienzo de la conversación. Viene con frases de entrenamiento comunes como "Hola" o "Buenos días".
    
- **`Default Negative Intent`:** Sirve para enseñarle al agente las frases que debe **ignorar** o que **no debe asociar** a ninguna de tus intenciones. Esto ayuda a evitar emparejamientos incorrectos. Un buen ejemplo es si tu agente es para reservar habitaciones, podrías añadir la frase "Quisiera comprar un libro sobre habitaciones" a esta intención negativa para que el agente no la confunda con una solicitud de reserva.
    

#### **Entrenamiento del agente**

El proceso para que el modelo NLU (Comprensión del Lenguaje Natural) reconozca y asocie las frases a las intenciones se llama "entrenamiento del agente". Por defecto, el entrenamiento se activa automáticamente cada vez que guardas tu agente, procesando todas las frases de entrenamiento que has agregado. Esto se puede configurar en la pestaña de **Machine Learning (ML) Settings**.


---

# Mejores prácticas para la optimización de intenciones y entidades

La calidad del agente conversacional depende en gran medida de cómo se configuran las intenciones y las entidades. Sigue estas prácticas recomendadas para obtener mejores resultados.

#### **Frases de entrenamiento: Calidad y cantidad**

- **Usa datos reales:** Si es posible, utiliza transcripciones de conversaciones humanas reales.
    
- **Busca variedad lingüística:** Incluye frases que varíen en gramática y longitud (frases cortas como "pagar mi factura" y frases largas como "Acabo de recibir un correo que dice que necesito pagar mi saldo").
    
- **Evita la sobre-representación:** No añadas todas las frases posibles que encuentres para evitar el sobreajuste (`overfitting`).
    
- **Equilibra la cantidad:** Un número desequilibrado de frases de entrenamiento entre intenciones puede sesgar al modelo. Si una intención tiene muchas más frases que las demás, reduce su número para que el modelo no la favorezca de forma indeseada.
    
- **Anotación consistente:** Anota (`tag`) las entidades de forma consistente y precisa. El texto seleccionado debe ser exacto, sin palabras innecesarias.
    
    - **Regla general:** Cada parámetro debe usarse en al menos cinco frases de entrenamiento.
        

#### **Gestión de intenciones**

- **Usa intenciones distintas:** Si las solicitudes de los usuarios son muy diferentes (ej., "solicitar información sobre hotspot" vs. "activar hotspot"), usa intenciones separadas para cada una.
    
- **Diseña para la reutilización:** Una intención debe ser reutilizable en diferentes contextos. Por ejemplo, la palabra "cancelar" puede significar "no" en un contexto, pero en otro puede ser una acción distinta. En este caso, es mejor tener una intención separada para "cancelar" y otra para "no".
    
- **Maneja la ambigüedad:** Para solicitudes vagas, usa una intención de desambiguación (`disambiguation intent`) que le pida al usuario más información para aclarar su intención.
    
- **Aprovecha el etiquetado:** Usa el etiquetado de entidades para reducir el número de frases de entrenamiento repetitivas. Puedes reducir varias frases a una sola si usas una entidad.
    

#### **Mejores prácticas para entidades**

- **Regla fundamental:** Las **intenciones** se asocian a **acciones** y las **entidades** a **objetos**.
    
    - **No crees intenciones que se diferencien solo por el valor de una entidad.** Por ejemplo, en lugar de `ventas-comprar-pixel` y `ventas-comprar-iphone`, usa una sola intención `ventas-comprar` con una entidad para el `producto`.
        
- **Consistencia y variedad:**
    
    - Asegúrate de que todas las ocurrencias de una entidad en una frase de entrenamiento estén etiquetadas.
        
    - No es necesario etiquetar todos los sinónimos o valores de una entidad en cada frase de entrenamiento. Las frases de entrenamiento actúan como plantillas.
        
- **Usa entidades del sistema:** Siempre que sea posible, utiliza las entidades del sistema que ya existen (`$sys.`) para conceptos comunes como fechas, direcciones, números de teléfono, etc., en lugar de crear las tuyas propias.

---
