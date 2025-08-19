---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/Introduction to Agent Assist and its GenAi Capabilities/05 Smart Reply/"}
---

### Asistente de Agente: Smart Reply

Smart Reply es una funcionalidad del asistente de agente diseñada para ayudar a los agentes humanos durante las conversaciones al sugerir respuestas automáticamente. Utiliza un modelo de **Long Short-Term Memory (LSTM)**, un tipo de red neuronal recurrente, que está integrado en Agent Assist. El modelo aprende del contexto de la conversación para proponer respuestas coherentes y de alta calidad, lo que ayuda a reducir los tiempos de respuesta.

Los beneficios clave de Smart Reply son:

- **Reducción del tiempo de manejo promedio (AHT):** Ayuda a los agentes a responder más rápido.
- **Mejora de la satisfacción del agente:** Les facilita el trabajo al proporcionar sugerencias útiles.
- **Aumento potencial de ventas:** La eficiencia y calidad de las respuestas pueden mejorar la experiencia del cliente y, por lo tanto, las conversiones.

En esencia, Smart Reply actúa como un asistente personal para el agente, ofreciéndole la siguiente frase o respuesta más probable en tiempo real.

---

### Prerrequisitos y arquitectura

Para implementar Smart Reply, se requiere una configuración específica en Google Cloud.

**1. Requisitos de Google Cloud:**
- Un proyecto de Google Cloud con los **buckets** y las **APIs** necesarios habilitados.
- Las APIs requeridas son:
    - **Conversational Agents API**
    - **Cloud Storage API**
    - **Data Labeling API** (para etiquetar datos si es necesario)

**2. Permisos de acceso (IAM):**

- El equipo que trabaja en el proyecto debe tener los permisos IAM adecuados.
- Se recomienda otorgar roles de **Project Owner** o, de forma más granular, **Conversational Agents API Admin** (obligatorio) y **Storage Admin** (opcional pero recomendado) para asegurar el acceso a todas las funcionalidades.

### Preparación de datos y entrenamiento

Para que el modelo Smart Reply sea efectivo, necesita ser entrenado con un gran volumen de datos de alta calidad. Se utilizan transcripciones de conversaciones reales para este propósito.

**Requisitos del conjunto de datos (dataset):**

- **Mínimo de transcripciones:** Se requieren al menos **30,000 transcripciones**.
- **Volumen recomendado:** Se aconseja utilizar **200,000 transcripciones** para obtener un rendimiento óptimo.
- **Contenido:** Los mensajes deben ser conversaciones genuinas de un centro de contacto. Mensajes genéricos del sistema, como "la llamada está siendo transferida...", no son útiles.
- **Datos personales (PII):** El contenido no debe contener más de un **2% de PII** para garantizar la privacidad y la seguridad.
- **Formato CSV o JSON**
	- CSV: Cada columna de ser un string válido
	- JSON: Cada llave debe tener su valor propio asociado

![](https://i.imgur.com/rz1Vkel.png)

---

# Data preparation

**Estructura de los datos:** Cada transcripción debe ser un archivo JSON con los siguientes campos:
- **`transcript_id`:** Un identificador único para cada conversación.
- **`role`:** El rol del actor en la conversación (`Agente` o `Cliente`).
- **`content`:** El texto del mensaje.
- **`user_id`:** Un identificador para el hablante (`1` para el cliente, `2` para el agente).
- **`timestamp`:** La marca de tiempo del mensaje.

El proceso de preparación y entrenamiento sigue estos pasos:

1. **Importar los datos:** Las transcripciones en formato JSON se importan desde un bucket de Cloud Storage a la consola de Agent Assist.
2. **Crear el dataset:** Se crea un nuevo conjunto de datos para el entrenamiento.
3. **Conversión de formato:** Los datos se convierten al formato `Text Stream Entry` para que el modelo pueda procesarlos.
4. **Entrenar el modelo:** Se inicia el entrenamiento del modelo Smart Reply con el dataset preparado.
5. **Analizar el modelo:** Se evalúa el rendimiento del modelo entrenado.
6. **Revisar la lista de permitidos (allowlist):** Se verifica y ajusta la lista de respuestas permitidas para las sugerencias.
7. **Configurar y monitorear:** Se integra y se monitorea el rendimiento del modelo en producción.

---

# Resolver problemas comunes

Los 4 pasos recomendados:
1. Revisar las métricas de evaluación del modelo contra el dataset de entrenamiento
2. Revisar la integración
3. Revisar las conversaciones enviadas en el live traffic
4. Correr una evaluación en el modelo Smart Reply contra live traffic

### Solución de problemas comunes

Los problemas de rendimiento con Smart Reply a menudo se deben a fallos en el entrenamiento o la integración. Para resolverlos, se recomienda un enfoque de cuatro pasos:

1. **Revisar las métricas de evaluación del modelo** en el conjunto de datos de entrenamiento.
2. **Verificar la integración** entre la API y el escritorio del agente.
3. **Analizar las conversaciones** en el tráfico en vivo.
4. **Evaluar el modelo** Smart Reply en tráfico en vivo.

A continuación, se presentan algunos problemas comunes y sus soluciones:

**Problema 1: El modelo tiene un CTR (Click-Through-Rate) bajo (<10%).**

- **Causa posible 1: Datos de entrenamiento deficientes.** El modelo no aprende de forma efectiva si los datos son de baja calidad o insuficientes.
- **Solución:** Revisa las métricas de **Recall** y **Message Coverage** en la consola. El Recall debe ser superior al 15% y la cobertura al 10%. Si no lo son, mejora la calidad y el tamaño de tu dataset.
- **Causa posible 2: Problemas de integración.** El modelo podría estar funcionando correctamente, pero las sugerencias no se están mostrando adecuadamente en el escritorio del agente.
- **Solución:** Compara las sugerencias del simulador de API con las que aparecen en la integración del agente. Si son diferentes, es probable que haya un error de integración.

**Problema 2: El formato de los mensajes cambia durante la transmisión.**

- **Causa:** El formato de los datos se altera al ser enviados a la API, lo que confunde al modelo.
- **Solución:** Utiliza la API `ExportMessages` para exportar las conversaciones en vivo y verifica si el formato es consistente. Si no lo es, corrige la integración de la API o reforma los datos y vuelve a entrenar el modelo.

**Problema 3: El modelo Smart Reply está desactualizado.**

- **Causa:** Las conversaciones y el comportamiento del cliente han evolucionado, y el modelo ya no es relevante.
- **Solución:** Usa las conversaciones exportadas para crear un nuevo dataset. Luego, llama a `CreateConversationModelEvaluation` y `ListConversationModelEvaluations` para evaluar las métricas sin conexión. Si el rendimiento es bajo, entrena un nuevo modelo con los datos actualizados.

---

### Resumen general

Smart Reply es una función de Agent Assist que utiliza un modelo LSTM para sugerir respuestas a los agentes en tiempo real. Su implementación requiere la configuración de proyectos en Google Cloud, el uso de grandes conjuntos de datos de transcripciones de conversaciones (al menos 30,000) y una cuidadosa preparación de los datos. El rendimiento del modelo se evalúa a través de métricas como el CTR, el Recall y la Cobertura, y se pueden resolver problemas comunes revisando la calidad del dataset, la integración de la API y la relevancia del modelo.