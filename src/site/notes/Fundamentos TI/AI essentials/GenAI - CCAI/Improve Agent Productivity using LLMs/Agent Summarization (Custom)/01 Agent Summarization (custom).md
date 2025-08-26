---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/01 Agent Summarization (custom)/"}
---


#### **1. ¿Qué es y para qué sirve?**

- **Definición:** Es una herramienta que condensa interacciones complejas con clientes en resúmenes concisos y claros.
- **Propósito:** Captura la esencia de la conversación sin perder detalles clave.
- **Modelo subyacente:** Un modelo de **resumen abstracto** de última generación que entiende el contexto y los matices para generar resúmenes.

#### **2. Hoja de ruta para el desarrollo**

1. **Preparación de los datos (`Data Preparation`):** El primer paso es preparar la data adecuada, como los ingredientes antes de cocinar.
2. **Etiquetado de datos (`Data Labeling`):** Categorizar y etiquetar los datos correctamente es crucial para el éxito del modelo.
3. **Construcción del modelo (`Model Building`):** Se crea un modelo robusto a partir de los datos preparados y etiquetados.
4. **Evaluación del modelo (`Model Evaluation`):** Se evalúa el modelo para asegurar que cumple con los estándares de calidad requeridos.
5. **Despliegue del modelo (`Model Deployment`):** Se implementa el modelo en escenarios del mundo real.
6. **Mejora del modelo (`Model Improvement`):** Se refina y mejora el modelo con el tiempo.
7. **Resumen LLM personalizado (`Custom LLM Summarization`):** Se adapta el modelo de resumen a las necesidades específicas de la organización.

#### **3. Casos de uso**

- **Para los agentes:**
    - Sugiere un borrador de resumen al final de una conversación.
    - Reduce el tiempo y el esfuerzo para crear notas.
    - Funciona como un asistente útil.
- **Para clientes recurrentes:**
    - Los agentes pueden revisar rápidamente conversaciones pasadas.
    - Asegura la continuidad y la personalización del servicio.
- **Para QA y gerentes:**
    - Permite monitorear y revisar eficientemente la calidad del servicio.
    - Ayuda a asegurar que cada interacción cumpla con los estándares.

#### **4. Pasos esenciales de implementación**

1. **Preparar y subir datos de entrenamiento:** Se utiliza el servicio de `conversation dataset` para cargar los datos que servirán de base.
2. **Configurar un perfil de conversación:** Se definen los parámetros para que el sistema se adapte a las necesidades específicas.
3. **Integrar el _runtime_ con las APIs de Agent Assist:** Se asegura que la interfaz de usuario se comunique sin problemas con el sistema (ya sea para chat o voz).
4. **Obtener resúmenes en tiempo real:** A través de la API, se obtienen resúmenes en tiempo real de las conversaciones.
5. **Enviar comentarios a través del servicio de registro de respuestas (`Answer Record Service`):** El _feedback_ de los usuarios es valioso para la mejora continua del modelo.