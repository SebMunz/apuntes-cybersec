---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/01 Data Ingestion/"}
---

# Índice

[[#Flujo de ingesta de datos en Conversational Insights]]
[[#Ingesta individual de datos]]

---

# Flujo de ingesta de datos en Conversational Insights

El flujo de trabajo para la ingesta de datos en **Conversational Insights** implica varios pasos, desde la preparación de los archivos de origen hasta la ingesta final en la plataforma.

---

### **1. Preparación de los datos**

1. **Creación de un _Cloud Storage bucket_:** Debes crear un bucket para almacenar tus archivos de audio o transcripciones. Es vital que el bucket se ubique en la **misma región** que los otros servicios que usarás, como el **Vertex AI Workbench**.
    
2. **Validación del formato:** Es un proceso manual que asegura que los archivos cumplan con los formatos requeridos.
    
    - **Audio:** Archivos de alta calidad y de **dos canales**.
        
    - **Chat:** Debe seguir una estructura JSON específica, incluyendo campos como `conversation_info` para metadatos y `entries` con la transcripción, el rol y la marca de tiempo de cada mensaje.
        

---

### **2. Procesamiento de los datos**

1. **Transcripción (solo para audio):** Utiliza la **API de Speech-to-Text** para convertir los archivos de audio en transcripciones de texto. Las transcripciones deben tener el mismo formato que la respuesta de esta API.
    
2. **Enmascaramiento de PII:** Usa el servicio de **Sensitive Data Protection** (anteriormente **Cloud DLP**) para detectar y enmascarar información personal identificable (PII), como nombres o números de tarjetas de crédito.
    
    - Se configura qué tipos de información sensible se deben enmascarar.
        
    - El enmascaramiento se realiza reemplazando los caracteres sensibles con otros, como asteriscos (`*`).
        
    - Para transcripciones JSON, se usan **transformaciones de registro** para mantener la estructura del archivo mientras se enmascara el contenido de texto.
        

---

### **3. Configuración del entorno y ejecución**

1. **Habilitar APIs:** Como requisito previo, debes habilitar las APIs necesarias en tu proyecto de Google Cloud, como Cloud Storage, Speech-to-Text, DLP, BigQuery y la API de Conversational Insights.
    
2. **Crear un _Vertex AI Workbench_:** Se recomienda usar un **cuaderno de Jupyter gestionado por el usuario** para ejecutar el _pipeline_. La instancia del cuaderno debe crearse en la **misma región** que tu bucket de almacenamiento para evitar movimientos de datos entre regiones.
    
3. **Configuración del ambiente Python:** En el JupyterLab, debes crear un archivo `requirements.txt` e instalar los paquetes de Python necesarios para el procesamiento de los datos.
    
4. **Ejecutar el _pipeline_:** Dentro del cuaderno de Jupyter, puedes ejecutar el código para llamar a las APIs de Speech-to-Text y Sensitive Data Protection, y finalmente subir la transcripción ya procesada al Cloud Storage.
    

---

### **4. Ingesta final**

Una vez que los datos están completamente procesados (validados, transcriptos y sin PII), se ingieren en **Conversational Insights** a través de su API.


---

# Ingesta individual de datos

Para ingerir una conversación de forma individual, debes hacer una llamada a la API de Conversational Insights.

1. **URL de la API:** Define la URL del _endpoint_ `conversations`, reemplazando `{project_id}` con el ID de tu proyecto.
    
2. **Autenticación:** Obtén un **token de autenticación** usando `google.auth.default()` con el ámbito de `Cloud Platform`. Este token se incluye en el encabezado de la solicitud.
    
3. **Cuerpo de la solicitud:** Crea un diccionario con los datos.
    
    - En el campo `data_source`, especifica `gcs_source` y la `transcript_uri` que apunta a la ubicación de tu transcripción en **Cloud Storage**.
        
    - Opcionalmente, puedes añadir un diccionario de `labels` para incluir metadatos de la conversación.
        
4. **Llamada a la API:** Envía una solicitud `POST` a la URL con los encabezados y datos preparados. Si la ingesta es exitosa, la API devolverá la URI de la transcripción.
    

Una vez ingerida, puedes ver la conversación en la **Consola de Conversational Insights**. El **Conversation Hub** te permite ver y filtrar conversaciones, y si haces clic en una, puedes ver los detalles, metadatos y la transcripción.

---

### **Importación masiva (`Bulk import`)**

La importación masiva es una función que permite ingerir múltiples archivos (transcripciones o audios) con un solo comando `curl`, sin necesidad de scripts de Python para cada paso.

- **Prerrequisitos:** La cuenta de servicio de Conversation AI debe tener acceso a los objetos en Cloud Storage.
    
- **Parámetros de la API:**
    
    - `gcs_source`: La ubicación del bucket de Cloud Storage.
        
    - `bucket_object_type`: `2` para audio o `1` para transcripciones de chat.
        
    - `medium`: El tipo de conversación (ej., `PHONE_CALL` o `CHAT`).
        
    - `agent_channel` y `customer_channel`: `1` o `2` para identificar los canales del agente y del cliente.
        
- **Comportamiento y limitaciones:**
    
    - La API devuelve un **ID de operación** que puedes usar para monitorear el progreso.
        
    - Solo se permite **una operación de importación masiva a la vez**.
        
    - No se pueden establecer metadatos o etiquetas personalizadas (`labels`) a nivel de conversación.
        
    - La misma configuración de **Speech-to-Text** y **DLP** se aplica a todos los archivos en la operación.
        
    - La importación masiva no admite la **redacción de transcripciones** en este momento, y la configuración de redacción solo funciona para archivos de audio.

---

<iframe width="560" height="315" src="https://www.youtube.com/embed/Q69askwtn2Y?si=KeSzD2P6OEvwTGt8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
