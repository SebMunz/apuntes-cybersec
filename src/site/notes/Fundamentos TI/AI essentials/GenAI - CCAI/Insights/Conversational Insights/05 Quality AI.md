---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/05 Quality AI/"}
---

# Índice

[[#Descripción general de Quality AI]]
[[#Usar Quality AI con UI]]
[[#Casos de éxito y precisión]]

---
# Descripción general de Quality AI

**Quality AI** es una función que se suma a las capacidades existentes de Insights (como el modelado de temas, el análisis de sentimiento y los marcadores) para proporcionar un análisis más profundo.

Las funcionalidades que trae son:

- **Auto QA:** Califica automáticamente las conversaciones usando tarjetas de puntuación personalizadas.
    
- **Rendimiento del agente en vivo:** Evalúa el rendimiento de los agentes basándose en el 100% de sus conversaciones con los clientes.
    
- **Rendimiento del agente virtual:** Analiza el rendimiento de los agentes virtuales para mejorar su contención y eficacia.
    
- **Email y redes sociales:** Amplía el análisis a estos canales de conversación.
    
- **Entrenador de IA:** Permite entrenar a los agentes con LLMs usando sus datos de conversaciones anteriores.
    
- **Generative FAQ:** Convierte listas de conversaciones en preguntas frecuentes con respuestas.
    

### **Roles clave y casos de uso**

Mientras que Insights era utilizado principalmente por ingenieros de datos, Quality AI requiere la participación de otros roles para aprovechar al máximo la interfaz de usuario:

- **Interesados del negocio (`Business Stakeholders`):** Usan los datos para rastrear los indicadores clave de rendimiento (KPIs), entender el retorno de la inversión de las tecnologías del centro de contacto y optimizar los flujos de trabajo.
    
- **Líderes de equipo (`Team Leads`):** Monitorean las métricas del centro de llamadas, supervisan el rendimiento de los agentes y se encargan de la contratación y la capacitación.
    
- **Agentes de control de calidad (`Quality Assurance Agents`):** Auditan llamadas y transcripciones para asegurarse de que cumplan con las tarjetas de puntuación de la empresa y evalúan el rendimiento general de los agentes.
    

El principal caso de uso de **Quality AI** es la **gestión de la calidad**, y la participación de estos roles en la interfaz de usuario ayuda a acelerar el tiempo de comercialización.

---

# Usar Quality AI con UI
### **1. Análisis de conversaciones a través de la consola**

- **Requisitos:** Asegúrate de que todas las conversaciones estén cargadas en el panel de Insights y de que el modelo de temas esté entrenado y desplegado si es necesario.
    
- **Pasos:**
    
    1. Navega al panel de Insights y selecciona tu proyecto.
        
    2. Verifica el recuento de conversaciones en la sección `Conversation history`.
        
    3. Aplica filtros si solo quieres analizar un subconjunto de conversaciones.
        
    4. Haz clic en `Analyze` y establece el porcentaje de conversaciones a analizar.
        
    5. Haz clic en `Analyze number of conversations` para comenzar.
        

### **2. Análisis de conversaciones a través de la API**

- **Flujo de trabajo:** Este proceso se realiza utilizando un _Vertex AI workbench_.
    
    1. Crea un archivo llamado `request.json` donde especifiques el porcentaje de conversaciones a analizar.
        
    2. Usa un comando `curl` para enviar una solicitud de análisis masivo, reemplazando el ID del proyecto y la ubicación.
        
- **Operación de larga duración:** El análisis masivo es una operación que tarda un tiempo considerable. Puedes verificar el estado en la interfaz de usuario, revisando el ícono del reloj de arena en la esquina superior derecha del panel.
    

### **3. Revisión de las conversaciones analizadas**

Una vez finalizado el análisis, puedes verificar los resultados:

- **Verificación en la interfaz de usuario:** Realiza revisiones puntuales en el **Conversation Hub** para confirmar que los temas, los resúmenes, la detección de silencio y el análisis de sentimiento se generaron con precisión.
    
- **Confirmación de la precisión:** Revisa si los temas y los campos asignados reflejan con exactitud el contenido de las conversaciones.

---

# Casos de éxito y precisión

**Quality AI** ha demostrado su efectividad en diversos sectores, incluidos telecomunicaciones, venta minorista y la industria automotriz. Los resultados de los proyectos piloto (Proof of Concept, POC) muestran una **precisión consistente** a pesar de las grandes diferencias en los casos de uso y la cantidad de preguntas.

- **Resultados destacados:**
    
    - **Grandes empresas de telecomunicaciones:** Un caso de uso con más de 100 preguntas logró un promedio del **70% de precisión** (con picos del 95%) utilizando solo el 40% de los datos de ejemplo recomendados. En otro caso con más de 70 preguntas, se alcanzó un promedio del **80% de precisión** (con un pico del 94%).
        
    - **Venta minorista y automotriz:** Aunque contaban con menos preguntas, lograron un promedio del **80% de precisión** (con picos de 97% y 96% respectivamente), demostrando que la herramienta puede ser efectiva incluso con datos limitados.
        

El uso de **ejemplos de conversación** es crucial para mejorar la precisión. La recomendación ideal es tener al menos 100 ejemplos por cada respuesta (sí, no, no aplicable) para crear un modelo ajustado (`fine-tuned`) y personalizado. Esto permite que el modelo entienda el comportamiento esperado para cada respuesta y emule la labor de un evaluador humano, lo que permite auditar el **100% de las conversaciones**.

---

### Mejores prácticas y estrategia de implementación

Para una implementación exitosa, se recomienda seguir las siguientes prácticas desde el primer día:

- **Comprender el entorno del cliente:** Cada cliente es único. Es fundamental planificar la integración telefónica, el formato de archivos, el tipo de ingesta de datos y el soporte de idiomas.
    
- **Definir la estrategia de ingesta:** Puedes optar por una **integración en tiempo de ejecución** para un análisis inmediato o por una **ingesta por lotes (`batch ingestion`)** almacenando datos en un bucket de Google Cloud Storage.
    
- **Incluir metadatos:** Además de las conversaciones, es vital adjuntar metadatos como el ID del agente, el nombre del equipo y la resolución de la llamada. Esto permite un análisis más detallado y dashboards personalizados.
    
- **Establecer métricas de éxito:** Define una precisión base y un objetivo claro para determinar cuándo una función está lista para producción. El esfuerzo para pasar de 60% a 80% de precisión es considerable, y este esfuerzo aumenta con cada punto porcentual adicional.
    
- **Proveer ejemplos de conversación:** Aunque los modelos base de Gemini son capaces de responder preguntas, proporcionar ejemplos es la mejor manera de entrenar un modelo personalizado para que la precisión sea alta.
    

---

### Precios y diferenciadores

- **Análisis de Insights:** $0.02 USD por conversación. Incluye sentimiento, entidades y marcadores (`highlighters`).
    
- **Análisis de temas:** $0.02 USD adicionales por conversación.
    
- **Calidad de IA (`Quality AI`):**
    
    - **Pago por uso:** $0.005 USD (medio centavo) por conversación y por pregunta.
        
    - **Suscripción:** $50 USD por agente al mes.
        

**Diferenciadores clave de Quality AI:**

- **IA avanzada y confiable:** Utiliza los últimos modelos de **Gemini** y permite refinar los modelos para asegurar la precisión.
    
- **Comprensión automatizada:** Transforma transcripciones de conversaciones en datos procesables de manera automática.
    
- **Empoderamiento del usuario:** Su interfaz intuitiva (`UI`) permite a los gerentes y equipos de control de calidad acceder directamente a los datos, sin depender de otros departamentos técnicos.
    
- **Valor inmediato:** A diferencia del software tradicional, Insights puede generar valor desde el primer día de uso, con análisis de impulsores de llamadas y calidad del agente.
    
- **Visión integral:** Captura todo el recorrido del cliente, desde el agente virtual hasta la resolución final con un agente humano, proporcionando una visión completa de la experiencia.

---

