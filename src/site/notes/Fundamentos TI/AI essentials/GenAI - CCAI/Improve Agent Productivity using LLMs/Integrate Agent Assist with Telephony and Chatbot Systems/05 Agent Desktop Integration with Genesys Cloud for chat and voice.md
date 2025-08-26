---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/05 Agent Desktop Integration with Genesys Cloud for chat and voice/"}
---

# Índice

[[#Integración Chat]]
[[#Integración Voz]]

---

# Integración Chat
### **Módulos UI de Agent Assist Disponibles**

Agent Assist ofrece módulos pre-construidos que se pueden integrar en Genesys Cloud de dos formas:

1. **Container (Contenedor Unificado):** Un panel central que agrupa múltiples features.
2. **Módulos Individuales:** Implementar features específicas de forma separada.

**Features Soportadas:**

- **Generative Knowledge Assist (GKA):** Sugiere artículos de conocimiento relevantes.
- **Proactive Generative Knowledge Assist (PGKA):** Genera respuestas con IA basadas en el contexto de la conversación.
- **Smart Reply:** Sugiere respuestas rápidas a preguntas comunes.
- **Conversation Summarization:** Genera resúmenes automáticos de la conversación.
- **Live Transcription:** Muestra el historial de la conversación transcrito.
- **Sentiment Analysis:** Analiza la intención emocional del cliente.

---

### **Proceso de Integración para CHAT**

**Paso 1: Desplegar Servidores**

- Desplegar un **application server** para renderizar la UI.
- Desplegar un **backend server** para manejar interacciones con APIs y gestión de datos.

**Paso 2: Configurar Autenticación OAuth en Genesys Cloud**

- **Crear un OAuth Client:** En la configuración de Genesys Cloud, crear un nuevo cliente OAuth.
- **Grant Type:** Seleccionar **`Implicit Grant (Browser)`**. (Es crucial).
- **Authorized redirect URIs:** Añadir la URL de la aplicación (a donde Genesys redirigirá tras la autenticación).
- **Token Duration:** Establecer la duración del token en **3600 segundos** (1 hora) para sincronizarlo con el token de la API de Dialogflow.
- **Copiar el Client ID:** Tras crear el cliente, copiar el `Client ID` y añadirlo a las variables de entorno del application server (`OAUTH_CLIENT_ID` y `REDIRECT_URI`). Luego, re-desplegar el servidor.

**Paso 3: Configurar el Canal de Chat**

- Usar **Messengers** (recomendado) sobre **Web Chat V2** por sus funcionalidades mejoradas.

**Paso 4: Integrar con el Interaction Widget de Genesys**

- **Variables de Entorno:** Configurar en el application server el `Client ID`, la región de Genesys Cloud y la URL del proxy server.
- **Interaction Widget URL:** Configurar la URL del widget, asegurándose de incluir _placeholders_ para valores dinámicos como el `conversation ID` y el `host origin`.
- **Opciones del iFrame:** Ajustar la configuración de `Iframe Sandbox Options` y `Iframe Feature and Permissions Policies` para asegurar el funcionamiento correcto.

**Paso 5: Pruebas**

- Usar las **herramientas de desarrollador de Genesys Cloud** para probar las integraciones con Web Messenger y Web Chat V2.
- Asegurarse de que el agente esté en estado **"On Queue"** para recibir chats de prueba.
- Verificar que todas las features se muestren correctamente.

---
# Integración Voz

### **¿Qué es el Genesys Cloud Voice Connector?**

- **Función:** Tecnología que **captura streams de audio en tiempo real** desde el contact center de Genesys Cloud.
- **Cómo Funciona:** Utiliza la **API Audiohook** de Genesys Cloud para establecer una **conexión persistente WebSocket**.
- **Flujo:** Este audio se transmite mediante **gRPC** al backend de integración de Agent Assist para su análisis.
- **Beneficio:** Actúa como un puente para llevar las capacidades de IA y Machine Learning de Google Cloud a las interacciones de voz.

---

### **Flujo de Audio y Análisis**

1. **Captura:** El monitor **AudioHook** de Genesys captura el stream de audio de una llamada entrante.
2. **Procesamiento:** El **Voice Connector** recibe este audio y lo envía a **Dialogflow** para su análisis en tiempo real.
3. **Análisis:** Dialogflow realiza:
    - **Transcripción** (Speech-to-Text)
    - **Análisis de Sentimiento**
    - **Detección de Intenciones**
4. **Resultados:** Los resultados del análisis se envían de vuelta al **agent desktop** a través del **Agent Assist Integration Backend**, proporcionando insights valiosos al agente en tiempo real.

---

### **Pasos de Despliegue (Resumen)**

**Prerrequisito:** Completar los pasos 1-6 de la integración de Genesys Cloud para Chat (módulo anterior).

1. **Clonar y Preparar el Repositorio:**
    - Clonar el repositorio de la solución en un nuevo directorio: `git clone [URL]`
    - Cambiarse a la rama `audiohook` y navegar al directorio `audiohook/`.
2. **Configurar Variables de Entorno:**
    - Ejecutar un comando para extraer variables clave en un archivo `.env.extracted`.
    - Copiar el archivo de ejemplo `.env.sample` a `.env`.
    - **Actualizar las siguientes variables críticas en el archivo `.env`:**
        - `CONVERSATION_PROFILE_NAME`: Usar el mismo valor del despliegue del application server.
        - `SERVICE_REGION`: La región donde se desplegó el servicio Cloud Run.
        - `GCP_PROJECT_ID`: El ID único de tu proyecto de GCP.
        - `REDIS_INSTANCE_ID`: Usar el mismo valor que en el backend de integración.
        - `UI_CONNECTOR`: El nombre de dominio del servicio Cloud Run del backend.
        - `SERVICE_ACCOUNT`: La cuenta de servicio para el connector (el script la creará si no existe).
        - `VPC_CONNECTOR_NAME`: Usar el mismo valor que en el backend de integración.
        - `API_KEY`: Generar una API key en la integración del monitor AudioHook (ver documentación).
        - `VOICE_INTERCEPTOR_SERVICE`: Elegir un nombre para el servicio Cloud Run del interceptor de voz.
    - **Añadir** el contenido del archivo `.env.extracted` al archivo `.env`.
3. **Instalar el AudioHook Monitor:**
    - Instalar el monitor **AudioHook** desde el **Genesys AppFoundry**.
4. **Ejecutar el Script de Despliegue:**
    - Ejecutar el script `deploy.sh` en el directorio `audiohook/` para desplegar automáticamente los servicios en Cloud Run.
5. **Configurar la Integración en Genesys Cloud:**
    - En la consola de Genesys Cloud, configurar la integración del monitor **AudioHook**, estableciendo parámetros como el canal de audio y la URI de conexión.

---
