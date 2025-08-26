---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/03 Data Labelling/"}
---

#### **Buenas prácticas para el etiquetado**

- **Secciones del resumen:**
    - Un resumen debe contener hasta 3 secciones para contar una historia completa:
        - **Situación:** Describe el problema del cliente. Captura los problemas principales, no los sub-problemas.
        - **Acción:** Describe lo que hizo el agente para ayudar. Se enfoca en las acciones principales.
        - **Resultado (`Outcome`):** Describe el resultado de las acciones del agente (ej. "Problema resuelto", "Escalado a supervisor").
        - **Próximos pasos (`Next Steps`):** Describe las acciones de seguimiento sugeridas por el agente (si no hay, usar `N.A.`).
- **Vocabulario:**
    - Usar un vocabulario consistente.
    - Si se usa el mismo modelo para voz y chat, preferir términos neutrales como "conversación" en lugar de "llamada".
- **Frases predefinidas:**
    - Usar las mismas frases para eventos comunes ayuda a reducir errores y asegura una salida más consistente del modelo.
    - Ejemplo: `Issue resolved with no further steps needed`.
- **Datos de PII (`Personal Identifiable Information`):**
    - **No incluir** información sensible (nombres, identificadores personales).
    - Se puede incluir información menos sensible, como fechas de pago, ya que el sistema de DLP puede diferenciarlas.
- **Nivel de detalle:**
    - Mantener la granularidad correcta para cada caso de uso.
    - Describir la situación y la acción con detalles concisos (ej. "Se extendió número de días hasta fecha").

#### **Extracción de conversaciones**

- Para mejorar la calidad del modelo, es clave obtener una variedad de conversaciones.
- Se recomienda tomar conversaciones aleatorias de un período largo (6 meses a 1 año).
- Se debe considerar el tipo de conversaciones (voz, chat, bot) y el área de negocio (ventas, finanzas).

#### **Estructura y estilo de escritura**

- **Oraciones cortas:** Priorizar la claridad y la brevedad. Evitar la voz pasiva y no repetir información.
    - Ejemplo: "Provided customer answers" en lugar de "Answers have been provided by an expert to the customer".
- **Pronombres neutros:** Usar pronombres de género neutro para respetar la privacidad del cliente.
- **Mejora continua:**
    - Organizar sesiones semanales de retroalimentación para revisar los resúmenes de los etiquetadores.
    - El _feedback_ es crucial para ajustar el modelo.

#### **Formato y anotación**

- **Fuente de datos:** Se usa una hoja de cálculo.
    - Cada fila representa una frase o una intervención (`utterance`).
    - Cada fila incluye el contenido, el rol del hablante y el `transcript_id` al que pertenece.
    - Las frases están ordenadas secuencialmente.
- **Tarea de anotación:**
    - En una pestaña separada, se crean los resúmenes.
    - Cada fila de esta pestaña corresponde a un `transcript_id`.
    - La tarea es destilar la conversación en un resumen informativo y conciso.
    - Los resúmenes se escriben en columnas separadas para `Situación`, `Acción` y `Resultado`.
- **Ejemplo práctico:**
    - Se presenta una transcripción.
    - Se crean las anotaciones que se ajustan al formato de resumen.
    - Ejemplo de anotación:
        - **Situación:** "Customer was able to login to account".
        - **Acción:** "Agent sent an email with password reset instructions"
        - **Resultado:** "Problem was resolved".

