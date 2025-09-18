---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/02 Topic Modeling/"}
---

# Índice

[[#Cómo funciona el modelado de temas]]
[[#Creación de un Modelo de Temas]]
[[#Topic Model DEMO]]
[[#Idiomas soportados y consideraciones]]
[[#Análisis de conversaciones y modelos de temas]]

---

El modelado de temas (`Topic Modeling`) en **Conversational Insights** es una herramienta que analiza y clasifica conversaciones de centros de contacto para identificar los temas principales. Esto ayuda a las empresas a entender por qué los clientes se comunican y a optimizar sus operaciones.

---

# Cómo funciona el modelado de temas

El modelado de temas funciona de la siguiente manera:

- **Identificación de temas:** La herramienta agrupa conversaciones similares y les asigna un nombre representativo para el tema. También identifica temas secundarios, que a menudo están relacionados con el proceso de la llamada (ej., autenticación).
    
- **Entrenamiento del modelo:** Un modelo de temas se entrena para identificar los temas principales de cada conversación. Esto crea un informe con nombres y descripciones de temas que se puede ajustar.
    
- **Inferencia de temas:** Una vez desplegado el modelo, puede clasificar nuevas conversaciones en tiempo real, lo que permite un análisis continuo del tráfico de llamadas.
    

### **Casos de uso y fases de implementación**

El modelado de temas es útil para reducir el volumen de llamadas e incrementar la contención. El proceso se divide en varias fases:

1. **Identificar los impulsores de llamadas (`Call drivers`):**
    
    - Ingiere todas las conversaciones en **Conversational Insights**.
        
    - Filtra las conversaciones por tema, canal (ej., voz, chat), duración o contención para establecer una línea de base de temas por volumen. Esto se convierte en tu **modelo de temas**.
        
    - Puedes usar filtros para crear modelos de temas de segundo nivel, lo que te permite profundizar en temas específicos.
        
2. **Razonamiento:**
    
    - **Para reducir volumen:** Examina las transcripciones de los temas más frecuentes para identificar qué partes se pueden **automatizar** o mejorar. Busca casos recurrentes o brechas en la base de conocimiento.
        
    - **Para aumentar la contención:** Analiza las excepciones, con foco en el usuario final y el agente humano, para encontrar áreas de mejora en los flujos del agente virtual.
        
3. **Mejorar el autoservicio:**
    
    - Analiza los flujos que has construido y auméntalos para que los clientes puedan resolver ciertos temas por su cuenta. Esto aumenta el nivel de automatización.
        
    - También puedes integrar o modificar la funcionalidad de asistencia del agente o el contenido de tu base de conocimiento.
        
4. **Monitoreo y medición:**
    
    - Usa la **inferencia de temas** para monitorear continuamente cómo se manejan los temas y rastrear el volumen de llamadas.
        
    - Compara las métricas clave **antes y después** de los cambios.
        
    - Repite el proceso para evaluar la efectividad y hacer más mejoras.
        

### **Datos de entrenamiento**

La calidad del modelo de temas depende de los datos de entrenamiento.

- **Requisito mínimo:** 1,000 conversaciones (con al menos 5 turnos de conversación entre el agente y el cliente).
    
- **Recomendación:** 10,000 conversaciones.
    
- **Calidad de los datos:** Los datos de entrenamiento deben ser similares al tráfico de conversaciones en vivo. Esto significa que si tienes 30 temas de contacto, los datos de entrenamiento deben tener conversaciones que cubran esos 30 temas.

---

# Creación de un Modelo de Temas

Para crear un modelo de temas en la consola de Conversational Insights, debes completar dos secciones:

1. **Detalles del modelo:**
    
    - **Nombre de visualización del modelo:** Un nombre descriptivo para tu modelo.
        
    - **Idioma del modelo (opcional):** Puedes especificar el idioma si es necesario.
        
2. **Conjunto de datos de entrenamiento:**
    
    - **Importar conversaciones:** Puedes usar todas las conversaciones ingeridas o filtrar un subconjunto para entrenar el modelo.
        
    - **Filtros comunes:** `Conversation Language`, `Conversation Channel`, `Turn Count` y `Conversation Import Time`.
        
    - **Recomendación:** Para una mejor calidad, se sugieren temas cortos de **3 a 6 palabras** (ej. "solución de problemas de mi control remoto" o "consulta sobre política de facturación").
        
    - **Iniciar entrenamiento:** Haz clic en **"Start Training"** para comenzar el proceso.
        

---

## **Evaluación de un Modelo de Temas**

La consola de Conversational Insights no ofrece métricas automáticas para cuantificar el rendimiento del modelo. La evaluación generalmente se basa en los criterios que cada cliente considere más adecuados.

### **Método de evaluación de ejemplo (evaluación humana)**

Un enfoque común es la evaluación humana de las conversaciones, considerando los siguientes parámetros:

- **`Is_Top_Topic_Match`:** Una medida binaria para evaluar si el tema principal predicho por el modelo es relevante.
    
- **`Is_Any_Topic_Match`:** Una medida binaria para evaluar si _cualquiera_ de los temas predichos (incluido el principal) es relevante.
    
- **Comentarios:** Un espacio para añadir notas sobre temas adicionales que el modelo debería haber identificado.
    

La agregación de estos resultados puede dar una idea del porcentaje de predicciones correctas (tanto del tema principal como de cualquier tema relevante).

---

# Topic Model DEMO

<iframe width="560" height="315" src="https://www.youtube.com/embed/wzP0R4hFJFE?si=EkpMhJ7Y7gmpFKj4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

# Idiomas soportados y consideraciones

- **Idiomas soportados:** El modelado de temas actualmente soporta **inglés, francés, alemán, italiano, portugués y español**. Puedes ver la lista completa de idiomas soportados por Conversational Insights en la documentación del producto.
    
- **Integración entre productos:** Antes de usar un nuevo idioma, es crucial verificar que sea compatible con todos los productos que planeas usar en tu _pipeline_, como **Speech-to-Text (STT)**, **Data Loss Prevention (DLP)** o **Agent Assist**.
    
- **Combinación de idiomas y ubicación:** Algunas funcionalidades pueden estar restringidas a regiones específicas. Por ejemplo, ciertas opciones de enmascaramiento de datos en DLP o la disponibilidad de STT pueden variar según la ubicación.
    

---

### **Manejo de idiomas en la ingesta**

- **Configuración del idioma por conversación:** Al ingerir una conversación a través de la API, tienes la opción de especificar manualmente el **código de idioma** para cada una. Esto es útil para indicar qué idioma se utiliza en cada transcripción.
    
- **Idioma predeterminado:** Si sabes que todas las conversaciones de un _pipeline_ están en un idioma específico, puedes configurarlo como el idioma predeterminado en la página de configuración de Insights.
    
- **Múltiples idiomas en la misma instancia:** Conversational Insights puede manejar conversaciones en **varios idiomas en la misma instancia**. Esto te permite obtener información de alto nivel para todo tu conjunto de datos, mientras mantienes la posibilidad de usar filtros para analizar los detalles específicos de cada idioma.
    

---

### **Uso de filtros y regionalización**

- **Filtro de idioma:** Puedes usar un filtro de idioma para entrenar un modelo de temas solo con datos de un idioma específico. Esto te permite tener un modelo para conversaciones en español, otro para inglés, y así sucesivamente, todo en la misma instancia de Insights.
    
- **Instancias por región:** Alternativamente, puedes tener instancias de Insights separadas para diferentes idiomas y regiones, por ejemplo, una instancia para conversaciones en portugués ubicada en el entorno de Brasil.

---

### **Nueva herramienta de LLM Topic Discovery**

- **Diferencia clave:** A diferencia del modelo de temas tradicional, que usa un modelo personalizado para el descubrimiento, la nueva herramienta de LLM Topic Discovery usa un **modelo de lenguaje grande (LLM)** para leer las conversaciones y generar temas.
    
- **Proceso:** El proceso de modelado de temas se divide en dos fases:
    
    1. **Topic Discovery:** Descubre los temas del conjunto de datos.
        
    2. **Topic Inference:** Asigna los temas descubiertos a las conversaciones.
        
- **Ventajas del LLM:** El uso de un LLM puede descubrir **más temas** y proporcionar una comprensión más profunda de los ya existentes, lo que ayuda en la toma de decisiones para crear agentes virtuales.
    
- **Requisitos:** Todavía se necesitan **mil conversaciones** como mínimo para iniciar el proceso de descubrimiento de temas con LLM.
    
- **Implementación:** Esta nueva funcionalidad se relanzará como un "motor de descubrimiento". La interfaz de usuario se está actualizando para separar el descubrimiento de la inferencia. Actualmente, se puede habilitar en proyectos seleccionados, pero el objetivo es que se integre en el modelo de temas.
    
- **Modelos personalizados:** Los modelos pre-entrenados no son suficientes para obtener resultados de alta calidad. Los modelos deben ser **ajustados** para el descubrimiento y la inferencia de temas específicos. Los nuevos modelos usarán LLMs, a diferencia de los actuales.
    

---

### **Otras características de Conversational Insights**

- **API de Speech:** La API de Speech ofrece herramientas para evaluar la calidad de la transcripción y calcular la tasa de error de palabras (`word error rate`). Puedes usar diferentes modelos de reconocimiento según tu caso de uso. También puedes integrar un **reconocedor personalizado** creado en la consola de Speech.
    
- **Corrección de errores:** Para la ingesta por lotes, se pueden usar herramientas como Speech o Gemini para corregir las transcripciones **antes de la ingesta**. Una vez que las conversaciones están en Insights, se puede acceder a ellas a través de la API para su posterior procesamiento.
    
- **Métricas y metadatos:** En el **Conversation Hub**, puedes ver métricas clave como el número total de conversaciones, la duración promedio y la cantidad de turnos.
    
    - Para ver los temas principales, necesitas un modelo de temas activo que analice constantemente las conversaciones.
        
    - El modelado de temas depende cada vez más de los **metadatos** para proporcionar información más profunda. La API de ingesta permite incluir metadatos como el ID del agente, el nombre del agente, los puntajes CSAT y el estado de resolución. Esto permite agregar datos y construir paneles informativos.
        
- **Ejemplo:** En el ejemplo del video, se usa un conjunto de datos sintético generado por Gemini sobre un cambio de plan telefónico. Se puede ver el canal (chat), la duración, los turnos y el tema principal. También se muestra cómo un modelo de temas extrae temas de un conjunto de datos, como "consulta sobre cambio de plan telefónico", que representa un **45%** de los datos de entrenamiento.

---

# Análisis de conversaciones y modelos de temas

- **Análisis manual:** Puedes analizar conversaciones de forma individual o masiva desde el **Conversation Hub**. El análisis se puede limitar a un modelo de temas específico o ser un análisis completo.
    
- **Análisis automático:**
    
    - **Integración en tiempo de ejecución:** Con la integración de **Agent Assist** o **Dialogflow**, las conversaciones se analizan automáticamente al ser ingeridas.
        
    - **Integración de API:** La función de transcripción automática permite el análisis automático de conversaciones subidas a través de la API.
        
- **Página de análisis:** Los _dashboards_ de análisis ofrecen una visión más amplia, mostrando métricas como el tiempo promedio de manejo, el porcentaje de silencio, el número de turnos y el sentimiento.
    

---

### **Creación de modelos de temas**

1. **Modelo de tema inicial:**
    
    - Empieza con un **modelo de temas amplio** utilizando solo el filtro de idioma. Esto te dará una gran cantidad de temas, algunos de los cuales podrían ser similares.
        
    - **Tamaño del modelo:** Puedes sugerir un número de temas al modelo (ej. 350). El modelo intentará consolidar temas para alcanzar ese número, pero no generará más temas si no hay suficientes en los datos (se recomienda usar un mínimo de 1,000 conversaciones para obtener resultados óptimos, aunque la documentación actual sugiere que 100 conversaciones con 5 turnos también son suficientes para los modelos v2).
        
    - **Idioma:** Puedes seleccionar el idioma del modelo entre los soportados (inglés, francés, alemán, italiano, portugués y español).
        
2. **Modelo de tema secundario:**
    
    - Una vez que tienes un modelo inicial, puedes crear una **segunda capa de análisis**.
        
    - Filtra las conversaciones basándote en un **tema primario** del modelo inicial (ej., "cambio de dirección").
        
    - Usa este subconjunto de conversaciones para entrenar un **nuevo modelo de temas**, que te permitirá obtener información más detallada sobre ese tema específico (ej., "cambio de dirección para servicio de electricidad", "suscripciones a revistas", etc.).
        

---

### **Manejo de múltiples idiomas**

- **Reglas de análisis (`Analysis Rules`):** Un nuevo conjunto de APIs que te permite combinar el análisis automático con los temas que has creado.
    
- **Funcionamiento:** Puedes crear reglas para que, cada vez que una conversación en un idioma específico (ej., alemán) sea ingerida, se analice automáticamente con el modelo de temas correspondiente a ese idioma.
    
- **Instancias:** Puedes trabajar en un **único espacio multilingüe** o crear **diferentes instancias de Insights** en distintas regiones para cumplir con requisitos regulatorios (ej., datos alemanes en la región Europa West 3 y datos en inglés en la región Global).
    

---

### **Otras características**

- **Acceso a los datos:** Puedes acceder a los datos de la conversación desde el **Conversation Hub**, que muestra la ubicación del archivo. También se puede acceder a la información de la conversación a través de una API (con el ID de la conversación) o exportarla en lote a **BigQuery**.
    
- **Generación de datos de prueba:** Se pueden crear conversaciones de ejemplo en un formato compatible con Insights usando un _prompt_ en **Gemini**. Esto es útil para generar datos genéricos o específicos de la industria para pruebas.
    
- **Actualización del modelo:** Los modelos de temas deben ser **actualizados y re-entrenados** regularmente con nuevos datos y filtros para evitar la "deriva" y asegurar que reflejen con precisión las conversaciones actuales de los clientes.

---

