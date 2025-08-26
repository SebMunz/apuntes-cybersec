---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/04 UI Integration/"}
---

# Índice

[[#Integración de la UI de Agent Assist en el Dashboard del Agente]]
[[#Integración Backend - Pub/Sub]]
[[#Configuración de Pub/Sub para Integración de Agent Assist]]
[[#Despliegue de la Integración de Agent Assist en Google Cloud]]

---
# Integración de la UI de Agent Assist en el Dashboard del Agente

La integración de la UI de Agent Assist en el `dashboard` del agente es crucial para mejorar la eficiencia y la calidad del servicio. Al mostrar las sugerencias directamente en el escritorio del agente, se elimina la necesidad de buscar información manualmente y se brinda **contexto inmediato** para resolver las consultas del cliente.

---

### Opciones y Arquitectura de Integración

Agent Assist ofrece dos enfoques predefinidos para la integración de la UI: **`UI Components`** (para integraciones más simples) y **`Custom Pub/Sub Based Integration`** (para soluciones más personalizadas). Ambos se encargan de la comunicación con las APIs de Google y del renderizado de las sugerencias, lo que facilita el trabajo del desarrollador.

El **flujo de datos** funciona de la siguiente manera:
1. **Escucha y Transcripción:** Agent Assist "escucha" la conversación en vivo, la transcribe en tiempo real y analiza el texto.
2. **Análisis y Emparejamiento:** El módulo de procesamiento de lenguaje natural (`NLU`) de Agent Assist empareja el texto con `intents` y bases de conocimiento.
3. **Sugerencias:** Las sugerencias se envían al escritorio del agente a través de una API.
4. **Feedback:** El agente proporciona `feedback` sobre la utilidad de las sugerencias, lo que permite que el modelo mejore continuamente.
---

### Enfoques de Integración de la UI

Se pueden elegir dos enfoques principales para integrar la UI de Agent Assist, dependiendo del nivel de personalización y el tipo de aplicación que se use.

1. **`Managed Container` (Contenedor Gestionado)**:
    - Este es el enfoque **recomendado para la mayoría de las integraciones**.
    - Es un **componente único** que renderiza todas las funcionalidades de Agent Assist en un panel unificado.
    - Maneja de forma automática la mayoría de las tareas y es ideal para integrarse en plataformas de terceros como **`LivePerson`** o **`Genesys Cloud`**.
    - Se implementa simplemente agregando una etiqueta `<script>` en el HTML y utilizando el componente principal `<agent-assist-ui-modules-container>` con parámetros de configuración.
2. **`Individual Components` (Componentes Individuales)**:
    - Este enfoque ofrece la **máxima flexibilidad** y es ideal para **aplicaciones personalizadas**.
    - Permite importar cada componente y conector de forma independiente, lo que significa que puedes mostrar cada funcionalidad de Agent Assist en diferentes partes de la página.
    - Requiere un mayor esfuerzo de desarrollo, ya que cada módulo debe importarse y configurarse manualmente.

Ambos enfoques ofrecen `snippets` de código de ejemplo en la documentación de "Recursos adicionales" para facilitar la integración con un `conversation profile`. La elección entre ellos dependerá de la arquitectura del escritorio del agente y del nivel de control que se necesite sobre la UI.

---

# Integración Backend - Pub/Sub
### Componentes Clave

1. **Cloud Pub/Sub:** Es una **cola de mensajes** que recibe notificaciones de Agent Assist y las transfiere al servicio `Cloud PubSub Interceptor`.
2. **Cloud PubSub Interceptor:** Un microservicio que recibe mensajes de Pub/Sub y los escribe en una caché de Redis.
3. **Memorystore Redis:** Una **caché** en memoria que actúa como un sistema de sincronización temporal de eventos. Utiliza su propia funcionalidad de _pub/sub_ para notificar al **conector de interfaz de usuario** (`UI Connector`) sobre nuevos eventos.
4. **UI Connector Service:** Es el _backend_ de la interfaz de usuario de Agent Assist. Mantiene conexiones **WebSockets** con el _frontend_ del agente para enviar eventos en tiempo real. También actúa como **_proxy_** para las solicitudes que van del escritorio del agente a los servidores de Agent Assist.
5. **Agent Assist UI Service:** Proporciona las páginas HTML que se integran en el _desktop_ del agente a través de un **`iFrame`**.
6. **Secret Manager:** Almacena de forma segura las credenciales y claves utilizadas por los servicios.
7. **Cloud Run & Load Balancer:** Gestionan la escalabilidad automática de los servicios.

---

### Flujos de Trabajo Principales

#### 1. Autenticación (Registro de JWT)

El escritorio del agente envía un **token personalizado** (por ejemplo, de Salesforce) al `UI Connector`. Este valida el token y, si es correcto, genera y devuelve un **JWT temporal** que se usa para autenticar todas las solicitudes y conexiones posteriores.

#### 2. Manejo de Eventos (Event Handling)

1. Cuando Agent Assist genera una nueva sugerencia, publica un evento en un **_topic_ de Pub/Sub**.
2. El **`PubSub Interceptor`** lo recibe y lo escribe en un canal de **Memorystore Redis**.
3. El **`UI Connector`**, que está suscrito a ese canal, recibe el evento.
4. Finalmente, el `UI Connector` envía la sugerencia al _frontend_ del agente a través de la **conexión WebSockets**.

#### 3. Procesamiento de Solicitudes (Proxy)

El `UI Connector` también actúa como un **_proxy_**. El agente envía solicitudes (como _feedback_ sobre una sugerencia) al `UI Connector` usando el JWT temporal. El conector valida el JWT y luego reenvía la solicitud a los servidores de Agent Assist.

![](https://i.imgur.com/VJ6yHUg.png)


---
# Configuración de Pub/Sub para Integración de Agent Assist

### **Tipos de Eventos de Pub/Sub**

Agent Assist publica tres tipos de eventos en topics de Pub/Sub diferentes, configurados en el `ConversationProfile`:

1.  **Suggestion Event (`HumanAgentAssistantEvent`):**
    *   **Contiene:** Las **sugerencias** generadas por Agent Assist (ej: respuestas de Smart Reply, artículos de Knowledge Assist, resúmenes).
    *   **Topic:** `suggestions`

2.  **New Message Event (`ConversationEvent`):**
    *   **Contiene:** **Nuevos mensajes** o utterances que aparecen en la conversación (transcripciones en tiempo real).
    *   **Topic:** `new-messages`

3.  **Lifecycle Event (`ConversationEvent`):**
    *   **Contiene:** Eventos del **ciclo de vida** de la conversación (ej: inicio, fin, transferencia).
    *   **Topic:** `lifecycle`

---

### **Pasos de Configuración**

1.  **Crear los Topics de Cloud Pub/Sub:**
    *   Crear tres topics separados en Google Cloud Pub/Sub para cada tipo de evento (suggestions, new-messages, lifecycle).
    *   *Instrucciones detalladas disponibles en el documento "Additional resources".*

2.  **Configurar el Conversation Profile (Método Recomendado - Consola):**
    *   En la **Agent Assist Console**, navegar al `Conversation Profile` que se desea integrar.
    *   En la sección de configuración de **Cloud Pub/Sub**, pegar los **Topic IDs** de los topics creados en el paso anterior en sus secciones designadas:
        *   Pegar el ID del topic para sugerencias en el campo correspondiente.
        *   Pegar el ID del topic para nuevos mensajes en su campo.
        *   Pegar el ID del topic para ciclo de vida en su campo.

3.  **Entender el Formato del Mensaje:**
    *   El **contenido del mensaje** de Pub/Sub varía según el evento que lo triggereará.
    *   Es **crucial** familiarizarse con el formato JSON de los mensajes `HumanAgentAssistantEvent` y `ConversationEvent` para poder procesarlos correctamente en el backend.
    *   *Consultar los ejemplos y schemas en el documento "Additional resources".*

4.  **Configuración Avanzada (Alternativa via API):**
    *   El `ConversationProfile` también puede configurarse mediante **APIs**, aunque la consola es el método recomendado.

---

### **Flujo de la Integración**

1.  **Publicación:** Agent Assist publica automáticamente los eventos en los topics de Pub/Sub configurados.
2.  **Recepción:** Un servicio backend personalizado (como el `PubSub Interceptor` de la arquitectura compleja) se suscribe a estos topics para recibir los mensajes.
3.  **Procesamiento:** Este servicio procesa los mensajes y los reenvía al Agent Desktop en tiempo real (usando WebSockets o otra tecnología) para mostrárselos al agente.

**Conclusión:** Esta configuración es el **primer paso fundamental** para construir una integración backend en tiempo real. Establece la canalización de datos que luego debe ser conectada al frontend del agente desktop mediante servicios personalizados.

---

# Despliegue de la Integración de Agent Assist en Google Cloud


### **Prerrequisitos**

1.  **Google Cloud CLI:** Instalar y configurar la línea de comandos de Google Cloud.
2.  **Recursos de Conversational Agents:**
    *   Habilitar la **Conversational Agents API** en el proyecto de Google Cloud.
    *   Tener un **Conversation Profile** creado y configurado con las features deseadas de Agent Assist (usando la consola es lo recomendado).
    *   Habilitar las **notificaciones de Cloud Pub/Sub** en ese perfil (configurando los topics para suggestions, new-messages, lifecycle).

---

### **Proceso de Despliegue**

1.  **Configurar Variables de Entorno:** Definir las variables necesarias para el despliegue (ej: PROJECT_ID, región de Cloud Run).
2.  **Ejecutar un Script Bash de Despliegue:**
    *   El repositorio de la solución proporciona un **script bash** que automatiza el despliegue.
    *   Este script realiza las siguientes tareas de forma automática:
        *   **Configuración de Google Cloud CLI:** Asegura que la CLI esté correctamente configurada.
        *   **Habilitación de Servicios de Google Cloud:** Habilita las APIs necesarias (Cloud Run, Pub/Sub, etc.).
        *   **Creación de Recursos y Asignación de Permisos:** Crea los recursos necesarios (como una service account) y asigna los permisos correctos (IAM).
        *   **Despliegue en Cloud Run:** Despliega los servicios (UI Connector, PubSub Interceptor) en **Cloud Run**.

---

### **Resultado Final**

*   Tras una ejecución exitosa del script, la **aplicación frontend** (Agent Assist UI Service) estará desplegada y disponible.
*   Esta aplicación estará alojada en una URL de **Cloud Run** y podrá ser embebida en el agent desktop usando un **iFrame**.