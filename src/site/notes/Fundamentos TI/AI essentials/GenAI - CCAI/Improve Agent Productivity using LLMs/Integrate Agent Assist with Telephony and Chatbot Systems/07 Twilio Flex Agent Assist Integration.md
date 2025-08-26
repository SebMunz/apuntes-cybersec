---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/07 Twilio Flex Agent Assist Integration/"}
---

# Índice

[[#Integración Agent Desktop]]
[[#Mejoras futuras]]

---

# Integración Agent Desktop

#### **Componentes principales de la integración**

- **Twilio Functions:** Un entorno sin servidor para alojar la interfaz de usuario de Agent Assist (un iframe) y las APIs necesarias para la integración.
- **Twilio Flex Plugin:** El componente del lado del cliente que muestra la interfaz de Agent Assist en el escritorio del agente.
- **UI Connector Backend:** El servicio de Google que gestiona la autenticación, la comunicación en tiempo real y la conexión con el motor de **Conversational Agents** de Agent Assist.

---

### **Detalles de los componentes**

#### **Twilio Functions**

- **Funciones:**
    - Alojan el documento HTML (la interfaz de Agent Assist).
    - Manejan los métodos de la API para usar Agent Assist.
    - Proporcionan la verificación de usuarios, tokens para el servicio de chat y la interfaz de Agent Assist.
- **Beneficio:** Evita la necesidad de alojar la interfaz en un servidor externo.
#### **Twilio Flex Plugin**
- **Funciones:**
    - Permite construir una experiencia de usuario personalizada para los agentes.
    - Muestra la **consola de Agent Assist** dentro de la aplicación de Twilio Flex.
- **Flujo de datos:** El plugin envía parámetros al backend de **Twilio Functions**, que a su vez retorna la solución de iframe para la interfaz del agente.
- **Parámetros de consulta (Query parameters):**
    - `conversation profile`
    - `channelType` (voz o chat)
    - `features` (las funcionalidades de Agent Assist que se quieren activar)
    - `conversation SID` (ID de la conversación)
    - `agent identity` (para verificar que el agente pertenece a la organización

#### **UI Connector Backend**

- **Funciones:**
    - **Autenticación:** Utiliza un método de autenticación personalizado para los escritorios de agentes.
    - **Generación de JWT:** Crea tokens web temporales (JSON Web Tokens o **JWT**) para validar las solicitudes.
    - **Conexión WebSocket:** Establece una conexión en tiempo real con el escritorio del agente para enviar eventos de Agent Assist.
    - **Manejo de eventos:** Recibe y envía notificaciones de eventos desde y hacia el escritorio del agente.

---

### **Configuración y despliegue**

#### **Requisitos**

- **CLI de Twilio:** Con los plugins `serverless` y `Flex plugin` instalados.
- **Variables de entorno:** Se deben configurar antes de realizar el despliegue.

#### **Despliegue**

- Se utilizan dos scripts `npm` para desplegar la solución:
    - `deploy plug-in`: Despliega el componente del frontend.
    - `deploy functions`: Despliega dos APIs para la autenticación y la interfaz de usuario.

#### **Configuración de voz**

- Se usa el conector **SIP** del Marketplace de Twilio.
- Se puede configurar en **Twilio Studio**.
- El conector SIP necesita un parámetro llamado `conversation` que tiene un valor compuesto por el ID del proyecto y el ID de la conversación de Twilio.

---

# Mejoras futuras

#### **1. Despliegue y configuración mejorados**

- **Despliegue con un solo clic:** Permite un despliegue rápido con una configuración predeterminada.
- **Integración de CI/CD:** Posibilidad de usar **GitHub Actions** para el despliegue continuo en múltiples entornos, con una configuración mínima.
- **Variables de entorno:** Serán gestionadas a través de una **interfaz de administración (Admin UI)** en lugar de archivos de configuración. Esto centraliza la configuración.
- **Gestión de secretos:** Se pueden generar secretos para cada entorno (`Twilio secret`) para gestionar credenciales de manera segura.

#### **2. Funcionalidades en la interfaz de usuario (UI)**

- **Manipulación del UI de Twilio Flex:** La integración permitirá manipular la interfaz del agente de Twilio Flex.
- **Eventos del UI:** Se podrán utilizar los eventos de la interfaz para crear una solución más robusta y reaccionar a las acciones del agente.
- **UI de administración:**
    - Permite probar la conexión al backend en la nube.
    - Permite habilitar o deshabilitar funcionalidades de Agent Assist.
    - Permite seleccionar diferentes versiones de los modelos de Agent Assist.

#### **3. Mejoras en funcionalidades específicas de Agent Assist**

- **Respuestas inteligentes (Smart Reply):** Las sugerencias aparecerán en un contenedor debajo de la caja de mensajes, permitiendo al agente editar la respuesta antes de enviarla.
- **Resumen de la conversación (Conversation Summary):** Se podrá activar la generación automática de resúmenes al finalizar la conversación.
- **Asistencia de conocimiento (Knowledge Assist):** Se mostrará en el lado derecho de la pantalla del agente para dar soporte a la conversación.

#### **4. Despliegue en múltiples entornos**

- **Soporte multi-entorno:** El sistema está diseñado para funcionar en múltiples entornos de forma sencilla (ej. desarrollo, producción).
- **Gestión de secretos por entorno:** Se pueden configurar secretos específicos para cada entorno para una mayor seguridad.