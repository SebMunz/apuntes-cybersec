---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/04 Building a Custom Model/"}
---

#### **Detalles importantes del modelo**

- **Arquitectura:** Se utiliza **LongT5**, un modelo robusto que maneja tareas complejas de lenguaje.
- **Longitud del input:** El modelo puede procesar hasta 4,000 _tokens_ de entrada.
- **Prácticas recomendadas para los datos de entrenamiento:**
    - Los _inputs_ deben ser de menos de 4,000 _tokens_ y los _outputs_ de menos de 120.
    - Los resúmenes no deben contener **PII** ni lenguaje tóxico.
    - Los resúmenes de entrenamiento deben ser de conversaciones reales.
- **Distribución de datos:** La distribución de los datos de entrenamiento debe ser lo más parecida posible a la del tráfico en vivo.
- **Calidad de STT (Speech-to-Text):** Si se usa data de voz, es crucial que la transcripción sea precisa.
- **Cantidad de datos:** Se recomiendan más de 1,000 ejemplos de entrenamiento para una buena calidad.
- **Reglas de escritura:** La consistencia en cómo se escriben los resúmenes es clave para entrenar un modelo preciso.

#### **Pasos para construir el modelo**

1. **Crear un proyecto en GCP.**
2. **Redactar los datos PII** (asegurar la privacidad).
3. **Adquirir conversaciones:**
    - Objetivo: 500 a 2,000 conversaciones con resúmenes de alta calidad.
    - Almacenarlas en un bucket de **GCS** (Google Cloud Storage).
4. **Etiquetar los datos** siguiendo las mejores prácticas.
5. **Revisar los datos** para asegurar que cumplen con los requisitos.
6. **Copiar los datos** a un almacenamiento de Google con controles de seguridad e IAM.
7. **Entrenar el modelo** y realizar una evaluación interna.
8. **Evaluar los resultados.**

#### **Uso de la consola de Agent Assist (UI)**

- **Configuración inicial:**
    - Apuntar a la ruta de Cloud Storage donde se encuentra la data de entrenamiento.
    - Elegir el tipo de conversación (Chat o Voz), el nombre del modelo y el idioma.
    - La data debe estar en formato JSON.
- **Entrenamiento:**
    - Se puede proporcionar data de evaluación.
    - Se inicia el entrenamiento con el botón `Begin Training`.
- **Evaluación del modelo:**
    - Se usa la métrica **ROUGE-L** (Recall-Oriented Understudy for Gisting Evaluation).
    - **ROUGE-L** mide la superposición entre el resumen generado por la máquina y los resúmenes humanos.
    - Un puntaje de **ROUGE-L > 40%** se considera bueno para un modelo de resumen personalizado.
- **Asignación del modelo:**
    - Una vez que el modelo está finalizado, se asigna a un perfil de conversación para su uso.
    - Se puede obtener el `Profile ID` del modelo recién entrenado para vincularlo.

---

#### **Modelos personalizados para necesidades específicas**

- **Cuándo se necesitan:** Cuando el modelo estándar entrenado a través de la consola de Agent Assist no cumple con los requisitos complejos del cliente, como manejar transcripciones con un tamaño de _tokens_ superior a lo habitual.
- **Proceso de entrenamiento:**
    - Este tipo de entrenamiento especializado es raro.
    - Se realiza a través de **X-Manager**, una plataforma para empaquetar, ejecutar y hacer seguimiento de experimentos de _machine learning_.
- **Recursos de apoyo:**
    - Un documento detallado para "Entrenar un modelo a través de X-Manager".
    - Un documento de auto-servicio sobre el "Proceso de soporte de modelos personalizados de resumen".
    - El "Data Preparation Colab" para procesar datos y ejecutar trabajos de entrenamiento personalizados.

#### **Perfil de conversación**

- **¿Qué es?** Es el _blueprint_ o la hoja de ruta de una conversación.
- **Función:** Define cómo se procesa y se entiende cada interacción.
- **Configuración:**
    - Solo se necesita crear un perfil una vez por cada configuración que se desee.
    - Se puede crear en la consola de Agent Assist o a través de la API.
    - El perfil de conversación es donde se vincula el modelo de resumen personalizado para su uso.

