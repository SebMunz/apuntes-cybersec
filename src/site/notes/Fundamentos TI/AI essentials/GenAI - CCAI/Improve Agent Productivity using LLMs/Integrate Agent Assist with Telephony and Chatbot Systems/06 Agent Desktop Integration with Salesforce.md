---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/06 Agent Desktop Integration with Salesforce/"}
---

# Índice

[[#Lightning Web Components (LWC)]]
[[#Proceso de Integración de Agent Assist LWC]]
[[#Configurar el cliente de Chat y LWC]]

---

# Lightning Web Components (LWC)

### **Arquitectura de la Integración**

- **Tres Componentes Principales:**
    1. **Google Cloud:** Alberga la infraestructura backend de Agent Assist (UI Connector, APIs).
    2. **Salesforce Instance:** Donde trabajan los agentes. Contiene los **Agent Assist UI Modules** empaquetados en un **Lightning Web Component (LWC)** personalizado.
    3. **Web Client:** Donde los usuarios finales chatean con los agentes (usando Messaging for In-App and Web de Salesforce).
- **Flujo de Comunicación:**
    - Los **UI Modules** dentro de Salesforce interactúan con la plataforma de chat de Salesforce (Omni Channel Messaging).
    - El chat client de Salesforce se integra con los UI Modules y se comunica con el **UI Connector** alojado en Google Cloud.

---

### **Ejemplo de Funcionamiento (Demo)**

1. **Vista del Agente:** El agente ve la transcripción de la conversación y los módulos de Agent Assist en su escritorio de Salesforce.
2. **Smart Reply:** Cuando un usuario escribe "hi", el agente recibe **sugerencias de respuesta** (Smart Reply).
3. **Generative Knowledge Assist (GKA):** Cuando un usuario pregunta por un tema específico (ej: "deductible"), el agente recibe un **artículo de conocimiento sugerido** (GKA) que puede copiar y pegar en el chat.
4. **Summarization (Resumen):** El agente puede triggerear un resumen manualmente con un botón, o se genera automáticamente al finalizar el chat. El resumen incluye campos editables: situación, acción, resolución y satisfacción del cliente.
5. **AI Coach:** Proporciona sugerencias proactivas basadas en la conversación (ej: recordar verificar la dirección del cliente).

---

### **¿Qué son Lightning Web Components (LWC)?**

- **Definición:** Un framework **moderno de JavaScript** (similar a React, Angular, Vue) para construir componentes en Salesforce.
- **Ventajas:**
    - **Seguridad Fuerte:** Basada en los últimos estándares web y un entorno de ejecución JavaScript sandboxed (Lightning Web Security - LWS).
    - **Arquitectura Simple:** No need de alojar los UI Modules externamente. Los componentes se pueden arrastrar y soltar en apps y páginas de Salesforce.
    - **Integración Fácil:** Al estar definidos como código, es fácil clonar un repositorio, modificar su configuración y desplegarlo en la instancia de Salesforce.
- **Uso para Agent Assist:** Se usa un **LWC personalizado** que envuelve los **Agent Assist UI Modules**, permitiendo añadir features como Summarization y Smart Reply al desktop de Salesforce.

---

### **Prerrequisitos para la Integración**

**En el Entorno de Desarrollo Local:**

1. **NodeJS:** Versión 18 (usar NVM para gestionar versiones).
2. **Salesforce CLI:** Instalar globalmente con `npm install -g @salesforce/cli`. Permite interactuar con la org de Salesforce desde la terminal.
3. **Google Cloud CLI (`gcloud`):** Seguir la documentación de instalación del SDK.
4. **Credenciales de Salesforce:** Loggearse en la instancia de Salesforce y anotar:
    - **My Domain URL**
    - **Organization ID**

**En Google Cloud:**  
5. **Agent Assist Integration Backend:** Tener una instalación funcional del backend de integración (disponible en GitHub junto al código LWC). Seguir las instrucciones del `README.md`.

---

### **Proceso de Configuración**

1. **Configurar Variables de Entorno:** Conectar el backend con la org de Salesforce estableciendo variables como:
    - `AUTHORIZATION_OPTION=SalesforceLWC`
    - `SALESFORCE_DOMAIN` (tu dominio personalizado)
    - `SALESFORCE_ORG_ID` (tu organization ID)
2. **Ejecutar Script de Despliegue:** Ejecutar un script para desplegar toda la infraestructura de Google Cloud automáticamente.

**Resultado:** El componente LWC de Agent Assist estará integrado en el desktop de Salesforce, mostrando sugerencias en tiempo real dentro de la interfaz familiar del agente.

---

# Proceso de Integración de Agent Assist LWC

### **Flujo de Integración**

**1. Clonar y Preparar el Repositorio**
- Clonar el repositorio de GitHub de Agent Assist (si no se hizo durante la configuración del backend).
- Navegar al directorio del proyecto LWC (`lightning-web-component/`).
- Ejecutar `npm install` para instalar las dependencias, incluyendo los archivos JS de los UI Modules que se desplegarán en Salesforce.

**2. Configurar la Instancia de Salesforce (Desde la UI)**
- **Habilitar Omni-Channel:**
    - Ir a **Setup -> Omni-Channel Settings**.
    - Marcar **`Enable Omni-Channel`**.
    - Seleccionar **`Automatically log agents into Omni-Channel in the new window or tab`**.
    - Guardar.
- **Habilitar Experience Workspaces:**
    - Ir a **Setup -> Digital Experiences -> Settings**.
    - Marcar **`Enable Experience Workspaces`**.
    - Guardar.

**3. Autenticar y Desplegar con Salesforce CLI**
- **Login:** Ejecutar `npm run login` en la terminal para autenticar la CLI con las credenciales de Salesforce.
- **Desplegar:** Ejecutar `npm run deploy` para desplegar el LWC en la organización de Salesforce.

**4. Crear y Configurar una "Connected App" en Salesforce**

- **Propósito:** La LWC usa el flujo **OAuth 2.0 Client Credentials** para autenticarse. Una Connected App habilita este flujo.
- **Pasos:**
    1. Ir a **Setup -> App Manager -> New Connected App**.
    2. **Configuración Básica:**
        - **Connected App Name:** Nombre identificativo (ej: "Agent Assist LWC").
        - **API Name:** Se auto-completa.
        - **Contact Email:** Email del administrador.
    3. **Configuración de OAuth:**
        - Marcar **`Enable OAuth Settings`**.
        - **Callback URL:** `http://localhost:1717/OauthRedirect` (o la URL relevante para producción).
        - **Selected OAuth Scopes:** Añadir `api` y `refresh_token`.
        - Marcar **`Enable Client Credentials Flow`**.
    4. **Establecer el "Run User":**
        - Ir a **Manage Connected Apps** -> Seleccionar la app creada -> **Edit Policies**.
        - En **Client Credentials Flow -> Run As**, seleccionar el usuario bajo cuyos permisos se ejecutará la app (ej: un usuario de servicio o un admin).
        - Guardar.
    5. **Obtener las Credenciales:**
        - En **App Manager**, buscar la app, hacer clic en **View -> Manage Consumer Details**.
        - Verificar por email y copiar el **Consumer Key** (Client ID) y **Consumer Secret**. Guardarlos de forma segura.
    6. **Habilitar CORS para OAuth:**
        - Ir a **Setup -> Buscar "CORS" -> Edit**.
        - Marcar **`Enable CORS for OAuth endpoints`**.
        - Guardar. _(Es crucial para que la LWC pueda alcanzar los endpoints de autenticación)_.

---

### **Recursos Adicionales de Salesforce**

- Para información detallada, consultar la documentación oficial de Salesforce:
    - "Configure Basic Connected App Settings"
    - "Configure a Connected App for the OAuth 2.0 Client Credentials Flow"

**Resultado:** Tras completar estos pasos, la Connected App estará configurada y el LWC estará desplegado, permitiendo que el componente se autentique y se comunique de forma segura con los servicios de backend de Agent Assist. El siguiente paso sería configurar las variables de entorno en el backend con el `Consumer Key` y `Consumer Secret`.

---

# Configurar el cliente de Chat y LWC

#### **Componente Agent Assist LWC**

- **¿Qué es?** Es un componente web (Lightning Web Component) que se puede arrastrar y soltar en Salesforce para integrar Agent Assist.
- **Configuración:** Se establecen variables para conectarlo al backend de Agent Assist y a un perfil de conversación de Dialogflow.
- **Funcionalidades:** Se pueden activar funciones como:
    - **Resúmenes:** Genera un resumen de la conversación.
    - **Asistencia de conocimiento (Knowledge Assist):** Ayuda a los agentes a encontrar información.
    - **Respuestas inteligentes (Smart Reply):** Sugiere respuestas.
    - **Guía para agentes (Agent Coaching):** Orienta al agente con pasos predefinidos.

#### **Configuración de Messaging for In-App and Web (cliente de chat de Salesforce)**

1. **URL de confianza (Trusted URLs):** Configura las URLs que Salesforce puede usar para comunicarse con las APIs de Google y servicios de Cloud Run.
    - **UI_connector:** URL del servicio Cloud Run.
    - **salesforce_domain:** URL del dominio de Salesforce.
2. **Cola (Queue):** Se crea una cola para enrutar las conversaciones.
    - **Nombre:** `Messaging_Queue`.
    - **Objetos soportados:** `Messaging User`, `Messaging Session`.
3. **Conjunto de permisos (Permission Set):** Permite a los agentes estar “en línea”.
    - **Nombre:** `Messaging Agents Permission Set`.
    - Se le otorgan los permisos para los estados "Busy" y "Online - Messaging".
    - Se asigna al usuario.
4. **Canal de mensajería (Messaging Channel):** Conecta el cliente de chat con la cola.
    - **Nombre:** `Messaging Channel`.
    - Se configura para usar `Omni-Queue` y la cola `Messaging Queue`.
5. **Despliegue de servicio integrado (Embedded Service Deployment):** Permite probar la configuración del chat como usuario final.
    - **Nombre:** `Messaging Embedded Service Deployment`.
    - Se usa para obtener un widget de chat para pruebas.
6. **Widget de conversación mejorada (Enhanced Conversation widget):** Se agrega a la página de la sesión de mensajería para ver la transcripción del chat.

#### **Pruebas y validación**

- Se inicia una conversación de prueba.
- El agente se pone en línea (`Online - Messaging`) para aceptar la conversación.
- Se valida la configuración del chat al poder responder al mensaje.
- Se prueba cada funcionalidad de Agent Assist (Smart Reply, GKA, etc.) durante la conversación.