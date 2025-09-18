---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Basic Performance Measurement/01 Feedback Loop/"}
---

# Índice

[[#Qué es]]
[[#Optimizaciones]]

---

# Qué es

El ciclo de retroalimentación es un proceso iterativo de cinco pasos para mejorar el rendimiento de un agente conversacional. Consiste en: comprender, analizar, identificar, mejorar y monitorear, usando datos reales de conversaciones.

---

### **1. ¿Qué es un ciclo de retroalimentación?**

Un **ciclo de retroalimentación** es un proceso en el cual la información de salida de un sistema se reintroduce como entrada para optimizar su rendimiento. En el contexto de un agente conversacional, esto significa usar datos de conversaciones reales para hacer mejoras basadas en información, lo que lleva a un mejor rendimiento del _bot_. Puede ser un ciclo positivo (que refuerza un buen resultado) o negativo (que corrige un resultado indeseado).

### **2. Pasos del ciclo de retroalimentación**

1. **Comprender:** Analizar el rendimiento actual del agente conversacional. Esto se puede lograr de varias maneras, como:
    
    - Revisar transcripciones de conversaciones para identificar problemas como la latencia o un alto volumen de llamadas.
        
    - Analizar datos de llamadas para ver cómo el agente maneja diferentes tipos de conversaciones.
        
    - Pedir retroalimentación a los clientes.
        
    - Revisar métricas clave que cambian con el tiempo, como la tasa de escalada a un agente humano.
        
2. **Analizar:** Usar métricas e indicadores clave de rendimiento (**KPIs**) para encontrar patrones, tendencias y áreas de mejora. Se pueden usar herramientas de visualización de datos para obtener _insights_ más profundos y tomar decisiones informadas. El objetivo es identificar puntos problemáticos comunes, errores de reconocimiento de intenciones o partes del flujo de conversación que causan que los usuarios abandonen.
    
3. **Identificar:** Comprender la causa raíz de las métricas de rendimiento positivas o negativas. Esto implica examinar factores como la calidad de los datos de entrenamiento, el diseño del flujo de conversación y la precisión del reconocimiento de intenciones del agente.
    
4. **Mejorar:** Aplicar las mejoras basadas en los _insights_ obtenidos en el análisis. Hay tres áreas clave para enfocar las mejoras:
    
    - **Modelo NLU (Natural Language Understanding):** Refinar el modelo para que interprete mejor las solicitudes de los usuarios, incluso con lenguaje informal. El **NLU** es una rama de la inteligencia artificial que permite a las máquinas comprender el lenguaje humano, extrayendo el significado, la intención y los detalles clave de una frase.
        
    - **Flujo de conversación:** Optimizar el flujo de la conversación para hacerlo más intuitivo y fácil de seguir. El **flujo de conversación** es el camino lógico que un usuario sigue al interactuar con un _chatbot_ o agente conversacional. Un buen diseño previene la frustración y ayuda a los usuarios a lograr sus objetivos eficientemente.
        
    - **Respuestas del agente:** Actualizar las respuestas para que sean más precisas, útiles y personalizadas.
        
5. **Monitorear:** Después de implementar las mejoras, se deben monitorear las métricas clave para establecer **líneas de base (`baselines`)** y hacer un seguimiento del rendimiento a lo largo del tiempo. Una **línea de base** es un punto de referencia contra el cual se mide el rendimiento actual para determinar si las mejoras han tenido un impacto positivo. Este monitoreo continuo permite comenzar el ciclo de retroalimentación de nuevo, lo que asegura una mejora constante.
---
# Optimizaciones

### **Tipos de optimizaciones**

- **Comprensión del lenguaje natural (NLU):** Mejora la capacidad del _bot_ para comprender lo que el usuario quiere. Incluye identificar la intención, extraer información relevante y generar una respuesta útil.
    
- **Flujo de conversación:** Optimiza la forma en que el agente interactúa con el usuario, incluyendo la estructura de la conversación, el uso de lenguaje natural y el tono.
    
- **Respuestas del agente:** Se refiere a cómo el agente responde para influir en la respuesta del usuario.
    
- **Manejo de _fallbacks_:** Mejora la forma en que el agente responde cuando no puede entender al usuario o no puede satisfacer una solicitud. Las acciones pueden incluir ofrecer opciones alternativas, sugerir reformular la pregunta o transferir la conversación a un agente humano.
    
- **Viaje del cliente (`Customer Journey`):** Busca optimizar el recorrido del cliente al poner más datos o procesos automatizados a disposición del agente.
    

### **Clasificación de las optimizaciones**

- **Oportunidades incrementales:** Son mejoras pequeñas que se pueden hacer a la experiencia actual. Por ejemplo, corregir defectos menores o realizar optimizaciones pequeñas.
    
- **Oportunidades `ten-ex`:** Son metas más ambiciosas que podrían llevar a una mejora significativa en el rendimiento del agente. Por ejemplo, rediseñar completamente la forma en que el agente interactúa con los usuarios.
---

