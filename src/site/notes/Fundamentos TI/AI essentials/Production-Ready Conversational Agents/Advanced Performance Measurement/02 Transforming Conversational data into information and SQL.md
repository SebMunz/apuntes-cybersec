---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Advanced Performance Measurement/02 Transforming Conversational data into information and SQL/"}
---

# Índice 

[[#Habilitar BigQuery]]
[[#Transformar a BQ]]

---

# Habilitar BigQuery

Para transformar los datos de registro de **Dialogflow CX** en información analizable, es necesario exportarlos a **BigQuery (BQ)**. Esta función automatizada, llamada **BQ Export**, envía los registros de sesión a una tabla de **BigQuery** para su análisis.

---

### **Pasos para usar BQ Export**

1. **Crear una tabla en BigQuery:** En el mismo proyecto de **Google Cloud Platform (GCP)** donde está el agente, debes crear una tabla con un esquema específico. Esto permite que **Dialogflow** comience a enviar los datos.
    
2. **Habilitar el registro de interacciones:** En la configuración de **Dialogflow CX**, tienes que activar el registro de interacciones y seleccionar el proyecto, el conjunto de datos y la tabla de **BigQuery** que creaste en el paso anterior.
    
3. **Los datos se llenan automáticamente:** Una vez configurado, toda la información de registro de interacciones en tiempo casi real se empezará a llenar en la tabla de **BigQuery**.
    

### **Estructura de los datos**

Los datos de los paquetes de solicitud y respuesta son modulares y están en un formato similar a **JSON**. La exportación a **BigQuery** es el primer paso para poder transformar estos datos en información que pueda ser consultada fácilmente.

---

# Transformar a BQ

Tras exportar los registros de **Dialogflow CX** a **BigQuery**, el siguiente paso es transformar esos datos para extraer información útil. Dado que **Dialogflow CX** funciona como una máquina de estados, es beneficioso desglosar los datos a nivel de transición de estado para un análisis más profundo.

---

### **Transformación de datos de BigQuery**

La transformación de datos es crucial porque los registros brutos contienen mucha información, pero está en un formato que no es directamente consultable ni fácil de interpretar. El objetivo es convertir estos datos en **información accionable**.

- **Nivel de turno vs. Nivel de transición:** Los registros exportados ya contienen información a nivel de turno (como la posición del turno o la hora de la solicitud). Sin embargo, se pueden extraer **informaciones (`insights`)** más profundas al desglosar los datos dentro de cada turno, ya que una sola transición de estado puede implicar múltiples pasos.
    
- **JSON de respuesta de `Detect Intent`:** Este es uno de los campos más importantes para extraer información clave para el seguimiento del rendimiento. Contiene detalles sobre:
    
    - **`transcript`:** La frase del usuario.
        
    - **`language`:** El idioma configurado.
        
    - **`match`:** Información sobre la coincidencia de intenciones (confianza, tipo, nombre de la intención).
        
    - **`parameters`:** Parámetros de sesión establecidos.
        
    - **`responseMessages`:** Las respuestas del _bot_ (puede haber varias).
        
    - **`diagnosticInfo`:** Información detallada sobre la transición de estado del agente (páginas, flujos, intenciones, _webhooks_).
        

### **Consideraciones específicas**

- **Interacciones de voz vs. chat:**
    
    - **Voz:** Los usuarios pueden interactuar con comandos de voz o con dígitos DTMF (teclado).
        
    - **Chat:** Los usuarios tienen más opciones (ej. botones). Es importante consultar con el diseñador de **Dialogflow CX** para entender las implementaciones específicas.
        
- **Respuestas del agente:**
    
    - **Voz:** Las respuestas suelen estar en los campos `Agent Says` o `Conditional Response`. En **SQL**, estas respuestas se verán concatenadas.
        
    - **Chat:** La forma en que se renderiza un mensaje puede variar según la implementación.
        
- **Páginas de origen y secuencia de ejecución:**
    
    - La **página de origen (`source page`)** indica a qué respondió el usuario.
        
    - La **secuencia de ejecución (`execution sequence`)** es crucial para entender los pasos intermedios entre las páginas, especialmente para la información de navegación y validación.
        
- **Llamadas a `Webhooks`:** El array dedicado a `webhooks` contiene información clave como la página de origen, el tiempo de respuesta y los parámetros de sesión actualizados.
    
- **Escaladas y finalización de conversaciones:** Es fundamental consultar con los diseñadores de **Dialogflow CX** cómo rastrean las escaladas de agentes y cuándo finalizan las conversaciones (por colgado del usuario o escalada). Estas se rastrean a nivel de turno.
    

La recomendación es transformar los datos de las columnas más utilizadas en el análisis para maximizar la usabilidad. Dado que los paquetes de solicitud y respuesta son modulares y en formato JSON, la transformación a un formato consultable es esencial.

---

# Medir métricas en SQL

Para obtener _insights_ procesables de tus datos en **BigQuery**, concéntrate en las métricas de tres áreas principales: **experiencia de interacción**, **diseño del agente** y **preparación del _backend_**. Estas métricas te permiten entender el rendimiento general del _bot_ e identificar áreas de mejora.

---

### **Métricas de experiencia de interacción**

Evalúan la efectividad con que el agente interactúa con los usuarios para satisfacer sus necesidades.

- **Tasa de escalada del agente:** El porcentaje de conversaciones que se transfieren a un agente humano. Se calcula dividiendo las conversaciones escaladas por el total de conversaciones. Monitorear esta métrica por flujo, intención o página, y a lo largo del tiempo, ayuda a medir el impacto de las mejoras.
    
- **Tasa de contención de 72 horas:** Una métrica clave de los _call centers_ que mide la "resolución en la primera llamada". Una sesión está "contenida" si el usuario no necesita volver a contactar al agente en el mismo canal o por el mismo caso de uso dentro de las siguientes 72 horas.
    
- **Volumen por dimensión:** Analiza el volumen de conversaciones por intención principal o por fecha para identificar cambios estacionales o el impacto de un error.
    

### **Métricas de diseño del agente**

Evalúan la calidad del agente y su capacidad para funcionar de manera óptima.

- **Tasa de "no coincidencia" (`No-match rate`):** El porcentaje de turnos en los que el **NLU** no pudo detectar ninguna intención en la frase del usuario. Una tasa alta indica problemas de diseño.
    
    - **Cálculo:** Se divide el número de mensajes sin coincidencia por el número de mensajes únicos.
        
    - **Uso:** Sirve para identificar **puntos de fricción** en los flujos o páginas y encontrar la necesidad de nuevas intenciones o frases de entrenamiento.
        
- **Tasa de "no entrada" (`No-input rate`):** La frecuencia con la que un usuario no responde después de que el agente le hace una pregunta.
    
    - **Cálculo:** Se divide el número de turnos de "no entrada" por el número total de turnos.
        
    - **Uso:** Indica si las preguntas del agente son confusas o si el usuario no tiene claro qué decir.
        

### **Métricas de preparación del _backend_**

Evalúan la capacidad de los sistemas de soporte para mantener las operaciones del agente, especialmente el rendimiento de los _webhooks_.

- **Tasa de fallos de _webhooks_:** Mide cuántas veces un _webhook_ no se completa con éxito, lo que a menudo causa una escalada directa.
    
- **Latencia de _webhooks_:** Mide el tiempo de respuesta, que debe ser lo más bajo posible para una experiencia fluida del cliente.
    

### **Cómo usar las métricas para la optimización**

- **Identifica los cuellos de botella del NLU:** Una trama de serie temporal de la tasa de "no coincidencia" muestra el efecto de las mejoras en el NLU.
    
- **Análisis de la transferencia (`Hand-off`):** Analiza la tasa de transferencia a un agente humano en diferentes contextos (a lo largo del tiempo, por intención o por página) para detectar dónde ocurren los problemas.
    
- **Prioriza mejoras `10x`:** Una oportunidad **`10x`** es una característica que reduce significativamente la escalada en una intención con mucho volumen.