---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/07 Model Improvement/"}
---

#### **Cómo mejorar continuamente el modelo**

- La mejora del modelo es un proceso continuo, como la jardinería.
- **Uso de resúmenes editados por agentes:**
    - Si las ediciones de los agentes se alinean con las reglas del conjunto de datos de entrenamiento, sus resúmenes pueden ser valiosos para volver a entrenar el modelo.
    - Si la calidad de las ediciones es incierta, se necesita un enfoque más analítico:
        1. **Diagnosticar áreas de bajo rendimiento:** Identificar qué áreas o temas son problemáticos para el modelo.
        2. **Extraer datos:** Identificar las conversaciones donde los resúmenes fueron significativamente editados (usando el `ROUGE score`).
        3. **Reescribir:** Crear resúmenes "perfectos" para esas conversaciones, que reflejen el contenido y el espíritu de la interacción.
        4. **Entrenar de nuevo:** Combinar los nuevos resúmenes con los datos de entrenamiento anteriores y volver a entrenar el modelo.

#### **Desafíos comunes y soluciones**

1. **Plantilla DLP:** Los resúmenes deben generarse después de que la información sensible haya sido redactada (`redaction`). La información redactada no debe aparecer en los resúmenes.
2. **Límite de _tokens_:** El modelo procesa hasta 2048 _tokens_ para los resúmenes. Las conversaciones más largas serán truncadas, lo que podría afectar la calidad del resumen.
3. **Conversaciones con _bots_:** Es un reto incluir la parte del _bot_ en el resumen. Es esencial vincular las partes de la conversación del _bot_ y del agente humano para una comprensión completa.
4. **Retroalimentación y reportes:** A pesar de que los clientes pueden enviar _feedback_ a través de la API, no hay un reporte automático que rastree KPIs como el porcentaje de resúmenes editados.
5. **Cambio de hábitos de los agentes:** Algunos agentes pueden añadir información extra a los resúmenes (ej. un ID de conversación), lo que aumenta la tasa de ediciones. Esto debe ser manejado mediante directrices claras.
6. **Repetición del modelo:** Un problema raro en el que el modelo se repite. La adopción de modelos basados en **T5** ha reducido este problema.

#### **Fase post-despliegue**

- **Evaluación de la calidad del resumen:**
    - Evaluar un resumen no es tan simple como evaluar un problema matemático, ya que puede haber múltiples resúmenes correctos para una misma conversación.
    - El objetivo es capturar la esencia en pocas palabras.
- **Identificar nuevos datos para iteración:**
    - Hay que ser cauteloso al usar la retroalimentación de los agentes para nuevos datos, ya que puede tener un impacto negativo.
    - A veces, los agentes añaden información extra (ej. números de referencia), cometen errores gramaticales, usan abreviaciones u omiten detalles cruciales.
    - La mejor práctica es extraer y **revisar** los resúmenes editados por los agentes. Un **etiquetador** o un **experto en la materia** (`SME`) debe verificar la legitimidad de las ediciones y reescribirlas si es necesario para que cumplan con las reglas establecidas.