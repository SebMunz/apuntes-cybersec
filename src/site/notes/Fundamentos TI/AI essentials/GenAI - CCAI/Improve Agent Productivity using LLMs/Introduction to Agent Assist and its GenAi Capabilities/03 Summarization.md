---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Introduction to Agent Assist and its GenAi Capabilities/03 Summarization/"}
---

# Summarization evaluation

## Resumen de conversaciones con IA Generativa

La funcionalidad de resumen de conversaciones utiliza un **modelo de lenguaje grande (LLM)**, ya sea pre-entrenado por Google o uno propio, para generar resúmenes automáticos a partir de conversaciones de voz o texto. Esta herramienta ayuda a los agentes a comprender rápidamente el contexto y los puntos clave de una interacción, mejorando la eficiencia y la calidad del servicio.

Los beneficios clave de esta función son:
- **Comprensión rápida:** Permite a los agentes entender de inmediato lo que el cliente necesita y el historial de la conversación.
- **Sugerencias automáticas:** El sistema sugiere resúmenes en tiempo real, lo que agiliza el trabajo del agente. 

El sistema por defecto genera resúmenes con las siguientes secciones:
- **Situation:** Describe la necesidad o el problema del cliente. 
- **Action:** Detalla las acciones que el agente tomó para ayudar.
- **Resolution:** Muestra el resultado de la interacción (ej. `yes`, `no`, `partial`, `n/a`).
- **Customer Satisfaction:** Indica la satisfacción del cliente (`satisfied` o `unsatisfied`).
- **Reason for cancelation:** Captura el motivo si el cliente solicitó una cancelación (o `n/a` si no fue así).
- **Entities:** Extrae pares de clave-valor de las entidades mencionadas en la conversación (ej. `product_name: "smartphone"`).

Para mantener la calidad, los resúmenes de baja calidad pueden ser eliminados. La carga de transcripciones para el análisis es sencilla y requiere una carpeta específica dentro de un bucket en Google Cloud Storage.

---

### Personalización de resúmenes

Más allá de las secciones predefinidas, puedes personalizar el resumen para adaptarlo a las necesidades de tu negocio. Para esto, el LLM utiliza toda la conversación y las secciones que tú definas como parte de un "prompt de texto" que guía al modelo en la tarea de resumen.

Cada sección personalizada requiere dos componentes:

- **Nombre de sección:** Un título descriptivo para la nueva sección (ej. `Información del producto`).
- **Definición:** Una descripción clara que le dice al modelo qué información debe extraer y cómo debe presentarla (ej. "Resume los detalles técnicos del producto que se discutieron en la llamada").

Puedes utilizar el **generador de pruebas** en la consola de Google Cloud para experimentar y refinar tus definiciones antes de implementarlas.

---

### Evaluación del rendimiento del resumidor

Para garantizar que los resúmenes sean precisos y útiles, es importante evaluarlos. Las **buenas prácticas** para crear definiciones de sección efectivas incluyen:
- **Ser específico:** Describe claramente el contexto, el formato, el estilo y la terminología que debe usar el resumen. Por ejemplo, "Resume en tiempo verbal pasado".
- **Uso de énfasis:** Usa mayúsculas para dar énfasis a palabras clave en la definición del prompt (ej. "SOLO incluye el modelo del dispositivo").
- **Razonamiento guiado:** Guía al modelo paso a paso para que siga un proceso lógico.
- **Añadir ejemplos:** Incluir entre 5 y 10 ejemplos de buena calidad ayuda al modelo a entender la tarea deseada.

La evaluación del rendimiento se basa en métricas como:
- **Situation:** ¿Qué necesita el cliente?
- **Action:** ¿Qué realizó el agente para ayudar al cliente?
- **Resolution:** Resultado de la interacción
- **Satisfacción del cliente**
- **Razón de cancelación:** Si es que aplica y cuál es el motivo (N/A si no aplica)
- **Entidades:** Se evalúa si las entidades extraídas son precisas y si están completas.

Además podemos medir valores como **Situation** y **Action** con métricas numéricas.
- **Precisión (Accuracy):** ¿Qué tan exacto es el resumen en relación con la conversación real?
- **Integridad (Completeness):** ¿El resumen incluye toda la información relevante sin omisiones?

Es fundamental proteger la **Información de Identificación Personal (PII)** durante todo el proceso de evaluación. Los valores de evaluación pueden ser tanto numéricos como descriptivos (`satisfied`, `partially`, `yes`, etc.).


---

### Configuración del resumen para audio

La configuración para el resumen de grabaciones de voz se realiza típicamente en un entorno como **Jupyter Notebooks**, donde se establecen varios parámetros esenciales:

**Parámetros principales:**
- **`PROJECT_NAME`**: El nombre de tu proyecto en Google Cloud.
- **`GCS_BUCKET_URI`**: La ruta base de tu bucket en Google Cloud Storage (ej. `gs://tu-bucket-nombre`).
- **`TRANSCRIPTS_INPUT_FOLDER_PREFIX`**: Carpeta donde se encuentran las transcripciones.
- **`AUDIO_FILE_INPUT_FOLDER_PREFIX`**: Carpeta que contiene los archivos de audio.
- **`SUMMARIZATION_OUTPUT_FOLDER_PREFIX`**: Carpeta donde se guardarán los resúmenes generados.
- **`CONV_PROFILE_ID`**: El ID del perfil de conversación para correlacionar correctamente los datos.
- **`NUM_CHANNELS`**: El número de canales de audio (`1` para mono, `2` para estéreo).
- **`LANGUAGE_CODE`**: El idioma del audio, por ejemplo, `en-US` o `es-ES`.
- **`MODEL`**: El tipo de modelo de reconocimiento de voz a usar, como `latest_long` para conversaciones generales, `phone_call` para llamadas telefónicas, `default` o `medical_conversation` para contextos médicos.

**Configuraciones avanzadas:**
- **`SAMPLE_RATE_HZ`**: La frecuencia de muestreo del audio, desde 8kHz hasta 48kHz.
- **`ENCODING`**: El formato del archivo de audio, incluyendo códecs sin pérdida (FLAC, LINEAR16) o con pérdida (MP3, OGG_OPUS).
- **`MIN_SPEAKER_COUNT` y `MAX_SPEAKER_COUNT`**: El número mínimo y máximo de hablantes que se espera en el audio.
- **`DLP (Data Loss Prevention)`**: Configuración para enmascarar o proteger la información sensible.

---

### Resumen general

El servicio de Google Cloud para el resumen de conversaciones utiliza un LLM para generar automáticamente resúmenes estructurados a partir de interacciones de voz o texto. Permite tanto el uso de secciones predefinidas como la creación de secciones personalizadas para adaptarse a necesidades específicas. Para su configuración, se utilizan parámetros clave en un entorno de desarrollo como Jupyter, y su eficacia se evalúa con métricas como la precisión y la integridad. Esta funcionalidad busca optimizar el trabajo del agente al ofrecerle información clave de forma rápida y concisa.

---

### Importante:

<a href="https://github.com/GoogleCloudPlatform/specialized-training-content/tree/main/courses/agent_assist">aquí están los notebooks para los labs de summarization</a>

