---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Customer Engagement Suite with Google AI Architecture/02 Planning/"}
---

# Índice

[[#Planning para Conversational Agents]]
[[#Planning para Agent Assist]]
[[#Planning para Conversational Insights]]

---

# Planning para Conversational Agents

### **Consideraciones iniciales**

Antes de desplegar, es vital responder a preguntas sobre:

- **Alcance:** ¿Uno o múltiples agentes?
    
- **Residencia de datos:** ¿Dónde se almacenarán los datos?
    
- **Disponibilidad y recuperación ante desastres:** ¿Se necesitan alta disponibilidad y un plan de recuperación?
    
- **Idiomas y zonas horarias:** ¿Qué idiomas y zonas horarias se deben soportar?
    
- **Seguridad y redes:** ¿Qué arquitectura de red y seguridad se implementará?
    
- **Privacidad de datos:** ¿Cómo se gestionará la recopilación de datos sensibles?
    
- **Canales y omnicanalidad:** ¿A través de qué canales se interactuará con el usuario?
    

### **Alta disponibilidad**

Para lograr una alta disponibilidad, hay dos enfoques principales:

1. **Múltiples agentes regionales:**
    
    - **Pros:** Permite redirigir el tráfico a un agente en otra región en caso de fallo.
        
    - **Contras:** Introduce una complejidad considerable en la infraestructura (requiere un proxy L7) y en las operaciones (necesidad de sincronizar las configuraciones de los agentes).
        
2. **Agente global único (opción recomendada):**
    
    - **Pros:** Simplifica la gestión, minimiza la complejidad operativa y de infraestructura.
        
    - **Funcionamiento:** Un único agente global puede enrutar las solicitudes al agente más cercano en la región disponible, lo que garantiza la alta disponibilidad de forma más eficiente.
        

### **Diseño de interacciones**

- **Idiomas:** Debes identificar los idiomas que tus usuarios finales hablan. Por ejemplo, en Canadá, un agente podría necesitar soporte para inglés y francés, lo que podría implicar la integración de sistemas de _backend_ diferentes.
    
- **Canales:** Hay que considerar los distintos canales que el agente soportará, como chat web, aplicaciones móviles, servicios de mensajería, o servicios de voz.
    
- **Experiencia omnicanal:**
    
    - Un sistema omnicanal permite soportar múltiples canales simultáneamente (ej. voz y chat).
        
    - Para diseñarlo, debes optimizar las respuestas para cada canal y considerar la integración de sistemas de _backend_ como CRM.
        
    - A pesar de ser más complejos de construir, ofrecen una experiencia de usuario superior.
        

### **Gestión de sesiones y seguridad**

- **Gestión de sesiones:** Es recomendable almacenar la información de la sesión en tu _middleware_ (además de en el agente conversacional).
    
    - Esto permite usar los datos para reportes, análisis y funciones avanzadas como la restauración de la sesión.
        
    - Se sugiere usar herramientas como **Cloud Firestore** para almacenar atributos clave de la sesión.
        
- **Datos sensibles:**
    
    - Es crucial manejar datos sensibles con mucho cuidado, especialmente aquellos clasificados como **PCI** o **PHI**.
        
    - Se pueden usar herramientas como **Sensitive Data Protection** y la **API de Prevención de Pérdida de Datos** para eliminar PII (información de identificación personal) de tus datos.
        
    - Además, se debe evaluar si los datos en tránsito requieren cifrado adicional más allá del estándar **TLS**.

---

# Planning para Agent Assist
### **¿Qué es Agent Assist?**

**Agent Assist** es una solución de **CES** que utiliza inteligencia artificial para empoderar a los agentes humanos de los centros de llamadas. Su objetivo principal es aumentar la productividad y la calidad del servicio al proporcionar asistencia en tiempo real, actuando como un "compañero digital".

---

### **Funcionalidades clave**

**Agent Assist** ofrece una serie de características para mejorar el servicio:

- **`Smart Reply` y `Smart Compose`:** Sugieren respuestas precisas y contextuales para interacciones de chat, ahorrando tiempo.
    
- **`Generative Knowledge Assist`:** Proporciona un agente de IA generativa para agentes humanos, mostrando proactivamente respuestas generadas y artículos de conocimiento relevantes.
    
- **`Baseline LLM Summarization`:** Ofrece resúmenes de llamadas en tiempo real con áreas de enfoque y estilos de escritura personalizables.
    
- **`Sentiment Analysis`:** Detecta las emociones predominantes del cliente (positivas o negativas) para un análisis más profundo de la interacción.
    
- **`Live Transcription`:** Transcribe en tiempo real cada palabra de la conversación entre el cliente y el agente.
    

### **Integración y flujo de trabajo**

El proceso de integración de **Agent Assist** varía según el tipo de entrada, ya sea chat o voz.

#### **1. Integración de chat**

1. El cliente inicia un chat.
    
2. El servidor de _backend_ de chat (`customer serving stack`) transmite el texto a la API de **Conversational Agents**.
    
3. La API envía las transcripciones y recomendaciones al servidor de _backend_.
    
4. El servidor transfiere la información al escritorio del agente humano.
    

#### **2. Integración de voz**

Hay dos enfoques principales para la integración de voz:

- **Integración basada en `gRPC`:**
    
    1. Se establece un perfil de conversación y se inicia con las APIs de **Conversational Agents**.
        
    2. Se definen los participantes (`HUMAN_AGENT`, `AUTOMATED_AGENT`, `END_USER`).
        
    3. Se utiliza el método `StreamingAnalyzeContent` para transmitir el flujo de audio y obtener transcripciones en tiempo real. Esto permite generar sugerencias relevantes para el agente.
        
- **Integración basada en `SIPREC`:**
    
    1. El protocolo **SIPREC** se usa para establecer sesiones de grabación y reportar metadatos.
        
    2. Un controlador de sesión de borde (`SBC`) puede duplicar una copia del flujo de audio y enviarla a la **Plataforma de Telefonía de Google (GTP)**.
        
    3. **GTP** reenvía el flujo a **CES** y **Agent Assist**, que lo analiza en tiempo real usando **STT** (`Speech-to-Text`).
        
    4. Las sugerencias se entregan al escritorio del agente a través de APIs **REST** o mediante la suscripción a un _topic_ de **PubSub**.
        

### **Recomendaciones de arquitectura final**

- Utiliza controladores de borde para minimizar la ruta entre los participantes de la llamada.
    
- Usa el _endpoint_ **SIPREC** de Google Cloud para duplicar los flujos de audio, ya que ofrece menor latencia que la integración **gRPC**. Esto se debe a que su _endpoint_ global enruta inteligentemente las conexiones al servidor más cercano, y la regionalización minimiza los retrasos.

---

# Planning para Conversational Insights

**Conversational Insights** es una solución de **CES** que usa los modelos de lenguaje de Google para transformar datos de centros de contacto en información útil. Su principal valor es extraer _insights_ de grandes volúmenes de grabaciones de llamadas y transcripciones de chat, que son difíciles de analizar manualmente.

---

### **Funcionalidades clave**

- **Modelado de temas (`Topic modeling`):** Identifica los temas o "motivadores de llamadas" de las conversaciones. Es útil para descubrir tendencias y definir los _intents_ de los agentes conversacionales.
    
- **Resaltadores (`Highlighters`):** Permite identificar segmentos relevantes en las conversaciones.
    
    - **`Smart highlighters`:** Preconfigurados con frases comunes como "información de autenticación" o "confirmar resolución".
        
    - **Resaltadores personalizados:** Capturan palabras clave o segmentos específicos.
        
- **Análisis de sentimiento (`Sentiment analysis`):** Detecta las emociones del cliente.
    
- **Resumen con LLM:** Proporciona resúmenes de las conversaciones.
    
- **Extracción de entidades:** Identifica información importante como precios, números de modelo, etc.
    
- **Búsqueda de conversaciones:** Permite a los usuarios buscar conversaciones por palabras clave, agentes, temas, etc.
    

### **Integración y flujo de datos**

La ingesta de conversaciones en **Conversational Insights** se puede realizar de varias maneras:

1. **Ruta en vivo:** Las conversaciones completadas en **Conversational Agents** o **Agent Assist** se ingieren automáticamente.
    
2. **Integración con CES:** Se pueden enviar archivos de audio o transcripciones a un _bucket_ de **Cloud Storage** para su posterior importación.
    
3. **Carga directa:** Subiendo archivos directamente a un _bucket_ de **Cloud Storage** e importándolos a **Conversational Insights**.
    

Todas las rutas de ingesta utilizan **Speech-to-Text** para la transcripción y la **API de Sensitive Data Protection** para la redacción de datos sensibles. Una vez que las conversaciones son analizadas, pueden ser exportadas a **BigQuery** para visualización en **Looker** o para usarse como fuente de datos para modelos de _machine learning_ en **Vertex AI**.

### **Perfiles de usuario y su valor**

**Conversational Insights** es valioso para diferentes roles dentro de un centro de contacto:

- **Gerente de producto de Centro de Contacto:**
    
    - **Problema:** No tiene suficiente información para priorizar funciones.
        
    - **Valor:** **Conversational Insights** le da datos para tomar decisiones, lo que reduce la carga de trabajo, el riesgo de errores y ayuda a identificar oportunidades.
        
- **Gerente de operaciones:**
    
    - **Problema:** Predecir necesidades de personal y evitar el agotamiento.
        
    - **Valor:** Usa el modelado de temas, junto con datos de metadatos (como el número de turnos o la duración de la conversación), para planificar, asignar capacitaciones y reducir el agotamiento.
        
- **Supervisor de agentes:**
    
    - **Problema:** Monitorear el rendimiento de los agentes y proporcionar un entrenamiento personalizado.
        
    - **Valor:** Se beneficia de los resúmenes de conversaciones, los mapeos de temas manejados por cada agente y los resaltadores que capturan momentos importantes para el entrenamiento.

---