---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/04 Advanced Settings/"}
---

# Índice

[[#Configuración del agente en Dialogflow CX]]
[[#Función de sistema]]
[[#Tipos de respuestas del agente conversacional]]
[[#Tipos de respuestas del agente conversacional]]
[[#Implementación de agentes multilingües]]

---

# Configuración del agente en Dialogflow CX

La configuración del agente en **Dialogflow CX** se encuentra en el botón **`Agent settings`** y contiene 7 pestañas principales que controlan diversas funcionalidades.

---

### **Pestañas de configuración**

#### **1. General**

- **Nombre de visualización (`Display Name`):** Permite cambiar el nombre del agente y la zona horaria.
    
- **Punto de entrada (`Entry Point`):** Define si las conversaciones empiezan con **flujos** o **libros de estrategias (`Playbooks`)**.
    
- **Bloqueo del agente:** Permite bloquear al agente para evitar ediciones.
    
- **Configuración de registro (`Logging settings`):**
    
    - Habilita el registro en la nube (`Cloud Logging`) para exportar consultas y datos de depuración.
        
    - Habilita el historial de conversaciones.
        
    - Habilita la censura de datos del usuario.
        
- **Sugerencias de intenciones (`Intent suggestions`):** El sistema hace sugerencias automáticas para ajustar intenciones existentes o crear nuevas, basándose en entradas de usuario que no fueron reconocidas.
    
- **Retroalimentación del usuario (`User feedback`):** Permite que los usuarios califiquen las conversaciones.
    
- **Integración con Git:** Permite subir y bajar el agente de un repositorio Git.
    

#### **2. IA generativa (`Generative AI`)**

- **General:**
    
    - **Frases prohibidas (`Banned phrases`):** Lista de frases que **IA generativa** no debe usar. Su uso aumenta la latencia.
        
    - **Filtros de seguridad:** Permite ajustar la sensibilidad de los filtros de contenido dañino.
        
    - **Seguridad de la pregunta (`Prompt security`):** Afecta a los libros de estrategias y tiendas de datos (`Data store`), protege contra ataques de inyección de _prompts_.
        
    - **Respaldo generativo (`Generative fallback`):** Define un _prompt_ que el agente usará cuando se active una acción de **`generative fallback`**.
        
- **Libro de estrategias (`Playbook`):** Permite seleccionar el modelo de lenguaje, definir límites de _tokens_ y otros parámetros relacionados con la longitud de la conversación.
    
- **Tienda de datos (`Data store`):** Permite definir el nivel de confianza de las respuestas basadas en datos, así como la información del agente y el comportamiento de respaldo en caso de que una respuesta no se encuentre en la tienda de datos.
    

#### **3. Flujos deterministas (`Deterministic Flows`)**

- **Entrenamiento del NLU:** Permite re-entrenar los flujos del agente de forma manual o automática (`Auto-train`).
    
- **Umbral de clasificación (`Classification threshold`):** Determina si el **NLU** coincide con una intención, un parámetro o con nada (`no-match`), basándose en un nivel de confianza.
    
- **Idiomas:**
    
    - **Idiomas raíz (`Root languages`):** Idiomas genéricos como el inglés (`en`). Se debe priorizar el diseño del agente en estos idiomas.
        
    - **Idiomas específicos de la zona (`Locale-specific languages`):** Idiomas con una región específica, como el inglés de Estados Unidos (`en-US`).
        
    - **Detección automática de idioma:** Habilita al agente para detectar y cambiar automáticamente al idioma del usuario.
        

#### **4. Conectividad (`Connectivity`)**

- Define plantillas personalizadas, cargas útiles (`payloads`) y credenciales para conectar el agente con servicios de terceros.
    

#### **5. Voz e IVR (`Speech and IVR`)**

- **Configuración de texto a voz (`Text-to-speech`):** Permite seleccionar el modelo de voz para cada idioma.
    
- **Configuración de voz a texto (`Speech-to-text`):**
    
    - **Adaptación automática de voz (`Auto speech adaption`):** Mejora la calidad del reconocimiento de voz usando la información del agente.
        
    - **Sensibilidad del fin del habla (`End of speech sensitivity`):** Controla el tiempo que el _bot_ espera antes de procesar lo que el usuario ha dicho.
        
    - **Tiempo de espera sin habla (`No speech timeout`):** Controla cuánto tiempo el _bot_ espera que el usuario hable.
        
- **`Barge-in`:** Permite que el usuario interrumpa al _bot_.
    
- **Exportación de audio:** Especifica un _bucket_ de **Google Cloud Storage** para guardar archivos de audio.
    
- **DTMF:** Permite que el agente procese las entradas de audio como eventos **DTMF**.
    

#### **6. Configuración de UI (`UI Settings`)**

- Permite modificar la apariencia de la interfaz de usuario que los clientes verán a través de **Call Companion**.
    
- Se puede cambiar el título del cuadro de diálogo, la fuente y los colores.
    
- Los cambios pueden probarse en un entorno real a través de **Dialogflow CX Messenger**.
    

#### **7. Seguridad (`Security`)**

- **Configuración de seguridad:** Permite configurar los ajustes de seguridad relacionados con la ubicación, la censura y la retención de datos.
    
- **Permisos:** Permite especificar los permisos del agente para acceder a otros servicios de **Google Cloud**.

---

# Función de sistema

La función del sistema de **Dialogflow CX** genera valores dinámicos durante las conversaciones. Se utiliza para generar respuestas, establecer parámetros y manipular datos.

---

### **Sintaxis y uso**

Las funciones del sistema siguen un patrón de sintaxis específico:

```
$sys.func.NOMBRE_DE_FUNCION(argumento1, argumento2, ...)
```

- El prefijo siempre es `$sys.func.`.
    
- El **NOMBRE_DE_FUNCION** siempre va en mayúsculas.
    
- Los argumentos pueden ser:
    
    - Valores directos (ej. números, _strings_, _booleanos_, listas).
        
    - Referencias a parámetros (ej. `$session.params.color`).
        
    - Funciones anidadas.
        

**Anotaciones:**

- Si un parámetro referenciado es nulo, se trata como tal.
    
- Las funciones no admiten objetos en línea.
    

### **Casos de uso y ejemplos**

- **Contar elementos:** Usar `COUNT` para saber cuántos elementos hay en una lista. Por ejemplo: contar el número de miembros en una lista de "**miembros de equipo**".
    
- **Manipular datos:** Las funciones pueden sumar (`ADD`), restar (`MINUS`), etc. Se pueden anidar para realizar operaciones más complejas.
    
- **Conversiones:** Si una entrada no es del tipo esperado (ej. un _string_ en lugar de un número), hay funciones que pueden convertirla.
    

### **Depuración y mejores prácticas**

- **Resultados de evaluación:** Para verificar el resultado de una función, revisa el campo **`SystemFunctionResults`** en la sección **`Diagnostic Info`** de los resultados de la consulta. Este campo registra los resultados y errores de las evaluaciones.
    
- **Considera las entradas:** Ten cuidado con el tipo de datos que utilizas (ej. la diferencia entre **números** y **cadenas de texto**).
    
- **Usar _webhooks_ para tareas complejas:** Si bien las funciones del sistema reducen la latencia, para la manipulación de datos y funciones más complejas es recomendable usar un _webhook_ en lugar de anidar funciones del sistema de manera muy compleja.

---

# Tipos de respuestas del agente conversacional

En **Dialogflow CX**, cada **cumplimiento** (`fulfillment`) puede incluir uno o varios tipos de respuestas que el agente proporcionará al usuario. Estas respuestas determinan cómo el agente interactúa y presenta información.

---

### **Nueve tipos de respuestas del agente**

1. **Texto (`Text`):** La respuesta más común; envía texto plano al usuario.
    
2. **Carga útil personalizada (`Custom payload`):** Permite enviar respuestas enriquecidas en formato **JSON**, compatibles con integraciones específicas (como **Dialogflow CX Messenger**). Se pueden incluir referencias a parámetros dentro del JSON.
    
3. **Transferencia a agente en vivo (`Live agent handoff`):** Transfiere la conversación a un agente humano.
    
4. **Metadatos de éxito de la conversación (`Conversation success metadata`):** Registra información para indicar que la conversación ha sido exitosa.
    
5. **Reproducir audio pregrabado (`Play pre-recorded audio`):** Reproduce un archivo de audio específico.
    
6. **Salida de audio a texto (`Output audio text`):** Convierte texto a voz para que el agente lo hable.
    
7. **Respuesta condicional (`Conditional response`):** Permite mostrar diferentes respuestas basadas en condiciones específicas (ej. edad del usuario).
    
8. **Transferir llamada telefónica (`Telephony transfer call`):** Transfiere la llamada a otro número de teléfono.
    
9. **Respuesta de almacén de datos (`Data store response`):** Recupera y presenta información de un **almacén de datos** (`data store`).
    

---

### **Respuestas detalladas**

- **Carga útil personalizada (`Custom payload`):**
    
    - Se usa para integrar **respuestas enriquecidas** con canales específicos que soporten formatos **JSON**.
        
    - La documentación de la integración (ej. en **Google Cloud**) detalla el formato específico.
        
    - Las referencias a parámetros dentro del JSON deben ser tratadas como **cadenas de texto** y, por lo tanto, deben ir entre comillas dobles.
        
    - Si se envía a integraciones personalizadas, **Dialogflow CX** no las procesa; la lógica debe ser implementada por la integración.
        
- **Respuesta condicional (`Conditional Response`):**
    
    - Permite mostrar diferentes mensajes basados en **condiciones**.
        
    - Funciona con una lógica **"si-entonces"**. Por ejemplo, se puede mostrar un mensaje diferente a un usuario mayor de 21 años que a uno menor.
        

---

**Nota:** Cuando se incluyen múltiples respuestas en un mismo cumplimiento, se presentan en el orden en que se definieron.

---

### **Respuestas del agente**

Las respuestas del agente se pueden agregar en la **cumplimentación (`fulfillment`)** del agente. Hay nueve tipos diferentes, que se pueden usar de forma individual o combinada. Si se usan varias, se ejecutarán en el orden en que se añadan.

#### **Tipos de respuestas del agente**

- **Texto (`Text`):** Muestra o lee un texto al usuario.
    
- **Carga útil personalizada (`Custom payload`):** Permite enviar una respuesta en formato **JSON**, compatible con integraciones que manejan respuestas enriquecidas (ej. **Dialogflow CX Messenger**). Deben seguir la documentación de la integración.
    
- **Transferencia a agente en vivo (`Live agent handoff`):** Transfiere la conversación a un agente humano.
    
- **Metadatos de conversación exitosa (`Conversation success metadata`):** Proporciona metadatos sobre una conversación exitosa.
    
- **Reproducir audio pregrabado (`Play pre-recorded audio`):** Reproduce un archivo de audio previamente grabado.
    
- **Texto de salida de audio (`Output audio text`):** Convierte el texto en audio y lo reproduce.
    
- **Respuesta condicional (`Conditional response`):** Permite mostrar respuestas de texto diferentes según una condición (`if-then`). Útil para personalizar la interacción basándose en parámetros.
    
- **Transferencia de llamada telefónica (`Telephony transfer call`):** Transfiere la llamada telefónica a otro número.
    
- **Respuesta de tienda de datos (`Data store response`):** Proporciona una respuesta basada en la información de una tienda de datos.
    

### **Componentes preconstruidos (`Prebuilt components`)**

Los componentes preconstruidos son plantillas que te permiten importar, personalizar y desplegar rápidamente tareas conversacionales comunes. Incluyen flujos, entidades, intenciones y _webhooks_ predefinidos.

#### **Tipos de componentes preconstruidos**

- **Bloques de construcción (`Building blocks`):** Componentes pequeños enfocados en una sola tarea (ej. recolectar un nombre, una dirección, etc.).
    
- **Casos de uso (`Use cases`):** Componentes más grandes y complejos que cubren un recorrido de usuario más largo (ej. agendar una cita).
    

#### **Beneficios**

- **Reducción del tiempo de desarrollo:** Permiten implementar funcionalidades rápidamente.
    
- **Mejores prácticas de Google:** Han sido rigurosamente probados y siguen las mejores prácticas.
    
- **Manejo consistente de casos extremos:** Estandarizan el manejo de errores y casos especiales.
    
- **Integración simplificada:** Los _webhooks_ flexibles con plantillas de integración simplifican la conexión con servicios externos.
    

#### **Cómo usarlos**

1. **Importación:** Se importan a un proyecto existente o nuevo desde el **Centro de componentes preconstruidos** (`Prebuilt Component Hub`). El sistema verifica conflictos entre recursos existentes y los nuevos. Se recomienda **conservar los recursos originales** para no perder personalizaciones.
    
2. **Personalización:**
    
    - Se pueden editar las configuraciones predefinidas.
        
    - Se actualizan las respuestas del agente para que coincidan con la marca.
        
    - Se pueden editar las entidades personalizadas e intenciones.
        
    - Los parámetros configurables se encuentran en la **página de inicio** (`Start Page`) en la ruta `'true'`.
        
3. **Integración:**
    
    - Los componentes se comportan como flujos normales.
        
    - Se pueden crear transiciones al flujo desde cualquier parte del agente.
        
    - Algunos componentes, especialmente los de casos de uso, requieren integraciones con servicios externos (ej. para autenticación o para agendar citas). Esto se hace a través de **webhooks flexibles** que proporcionan patrones de solicitud, respuesta y autenticación.
        

#### **Componentes disponibles**

Existen numerosos bloques de construcción y casos de uso disponibles. Se puede acceder a la lista más reciente en el **Centro de componentes preconstruidos** dentro de la consola de **Dialogflow CX**.

---

# Implementación de agentes multilingües

Para crear un agente multilingüe, es crucial seguir un proceso metodológico que garantice la calidad en cada idioma. La estrategia ideal es desarrollar primero el agente por completo en un idioma principal y luego incorporar los demás.

---

### **Puesta en marcha y estructura del idioma**

- **Configuración inicial:** Agrega los idiomas relevantes en la pestaña **`Languages`** en la configuración del agente.
    
- **Tipos de idioma:**
    
    - **Idioma raíz (`Root language`):** Idioma general sin especificación regional (ej. `en` para inglés).
        
    - **Idioma específico de la zona (`Locale-specific language`):** Idioma dirigido a una región o país específico (ej. `en-US` para inglés de EE. UU.).
        
- **Datos del agente:**
    
    - **Datos comunes:** La mayoría de los datos, como flujos, intenciones, entidades y _webhooks_, son comunes a todos los idiomas.
        
    - **Datos específicos del idioma:** El texto de interacción con el usuario (frases de entrenamiento, respuestas, etc.) debe ser específico para cada idioma.
        

### **Fases de diseño**

1. **Fase de diseño principal:** Construye el marco del agente en el idioma predeterminado.
    
2. **Fase de diseño secundaria:**
    
    - **Integración de idiomas:** Integra los idiomas adicionales (raíz y local).
        
    - **Traducción:** Utiliza la traducción automática y la curación manual para el entrenamiento **NLU**.
        
    - **Entrenamiento y pruebas:** Entrena y prueba rigurosamente cada idioma.
        

### **Entrenamiento y curación**

- **Entrenamiento NLU:**
    
    - **Traducción masiva automatizada:** Traduce las frases de entrenamiento del idioma raíz a los nuevos idiomas utilizando APIs como **Cloud Translation**. Se necesitan conocimientos de la **API** de **Dialogflow** para importar y exportar frases.
        
    - **Curación manual:** Desarrolladores con conocimiento del idioma de destino deben revisar las traducciones en la consola de **Dialogflow**. Deben ajustar el lenguaje para **`code-switching`** (cambio de código) o regionalismos (ej. el uso de _"bill"_ en lugar de _"factura"_ en español), y deben anotar las entidades correctamente.
        
- **Entidades:**
    
    - La traducción de entradas de entidades suele ser un proceso manual.
        
    - Es fundamental que los valores de entrada de la entidad principal sean **consistentes** en todos los idiomas para que puedan ser usados por _webhooks_ y para el enrutamiento.
        

### **Respuestas del agente**

- **Respuestas estáticas:**
    
    - Son respuestas predefinidas en la consola (ej. `"¿Sobre qué servicio llama?"`).
        
    - Se pueden traducir en masa con un _script_ y luego curar manualmente.
        
- **Respuestas dinámicas:**
    
    - Se generan en tiempo de ejecución a través de _webhooks_ o condiciones internas.
        
    - Es importante establecer una convención de nombres (ej. añadir sufijos de idioma como `_es` o `_en`) para que el _backend_ sepa qué parámetro llenar. En caso de que el _webhook_ se adapte al código de idioma, esto no es necesario.
        

### **Pruebas y garantía de calidad**

- **Pruebas de regresión NLU:**
    
    - Traduce los casos de prueba del idioma original a los nuevos idiomas. Esto se puede automatizar con la **API** de **Dialogflow** para operaciones masivas.
        
    - La **curación humana** es esencial para asegurar que las traducciones sean precisas y que las pruebas evalúen correctamente el rendimiento del **NLU**.
        
- **Pruebas de voz:**
    
    - Las pruebas de voz introducen una capa adicional de complejidad en los agentes multilingües.
        
    - **Pruebas automatizadas de voz:** Evalúan la capacidad del agente para entender y responder en diferentes idiomas.
        
    - **Pruebas de pronunciación:** Aseguran que las respuestas del agente se pronuncien de forma inteligible y correcta en el idioma de destino.
        

### **Enrutamiento de idiomas**

- **Rutas condicionales:** El enrutamiento de idiomas es una solución que establece rutas condicionales basadas en el parámetro `request.language` que envía el cliente.
    
- **Funcionalidades:** Es útil para agentes multilingües que tienen diferentes reglas de negocio o funcionalidades habilitadas por idioma.
    
- **Implementación de nuevos idiomas:** El enrutamiento de idiomas facilita la adición de nuevos idiomas, ya que las conversaciones pueden dirigirse temporalmente a un agente humano mientras se completa la experiencia conversacional del nuevo idioma.
---
