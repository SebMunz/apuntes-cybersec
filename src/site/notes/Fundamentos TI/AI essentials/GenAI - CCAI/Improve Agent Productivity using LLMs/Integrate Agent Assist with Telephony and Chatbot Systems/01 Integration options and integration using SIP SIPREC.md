---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/01 Integration options and integration using SIP SIPREC/"}
---

# Índice

[[#Opciones de Integración de Agent Assist]]
[[#Integración con la Suite de `Customer Engagement` (SIP/SIPREC)]]

---

# Opciones de Integración de Agent Assist

El objetivo principal de Agent Assist es proporcionar ayuda en tiempo real a los agentes humanos. Para lograrlo, debe integrarse sin problemas con las soluciones de `Customer Engagement` existentes. Las decisiones de arquitectura clave se centran en cómo se envían los datos a Agent Assist y cómo se presentan las respuestas.

---

### Panorama General de la Integración

Una solución completa de `Customer Engagement` tiene varias capas:
- **Autoservicio:** Un agente virtual atiende las consultas iniciales.
- **Asistencia en tiempo real:** **Agent Assist** se integra con el escritorio del agente para ofrecer sugerencias en vivo durante las conversaciones de voz o chat.
- **Análisis post-llamada:** **`Conversational Insights`** analiza los datos de la conversación para mejorar las operaciones.
- **Omnicanalidad:** Se unifica el soporte a través de diversos canales.
- **Capa de API:** Todas estas funcionalidades se conectan con otros sistemas, como un CRM, a través de una capa de APIs.

Las decisiones de integración cruciales incluyen:

- **Qué funciones de Agent Assist usar:** Esto depende de los objetivos del negocio.
- **Cómo enviar los datos a Agent Assist:** Para **chat**, se hace una llamada a la API `AnalyzeContent`. Para **voz**, se transmite el audio usando `gRPC` o `SIPREC`.
- **Cómo mostrar las respuestas:** Esto depende de si el _desktop_ del agente soporta la integración de `widgets` o `iframes`.
- **Integración con otros servicios de Google Cloud:** Se pueden requerir servicios como **`Cloud Storage`** para guardar audios o **`Cloud DLP`** para enmascarar información sensible.

---

### Integración para Chat (Flujo de la API)

El flujo de integración para el chat es relativamente simple:

1. Un cliente envía un mensaje a través de un chat.
2. El mensaje es recibido por el _backend_ del cliente.
3. El _backend_ hace una llamada a la API de Agent Assist (`AnalyzeContent`).
4. Agent Assist procesa el mensaje y devuelve **transcripciones y sugerencias**.
5. El _backend_ del cliente envía esta información al escritorio del agente.

---

### Integración para Voz: Dos Enfoques

La integración de voz es más compleja, con dos métodos principales.

#### 1. Usando SIPREC (Método Preferido)

Este método es el más recomendado porque simplifica el proceso de desarrollo.

- **Flujo:** El `Session Border Controller` (SBC) del cliente hace una copia del audio (`forking`) y la envía al `Google Telephony Platform` (GTP).
- **Proceso:** El GTP se encarga de gestionar el ciclo de vida de la conversación automáticamente y de reenviar el audio a Agent Assist.
- **Resultado:** Agent Assist transcribe el audio en tiempo real y genera sugerencias. La transcripción y las sugerencias se envían al agente a través de **mensajes `Pub/Sub`**.

#### 2. Usando gRPC (Mayor Esfuerzo)

Este método requiere más trabajo manual y es menos común para voz.

- **Flujo:** Es similar al de chat, donde la comunicación se canaliza a través del _backend_ del cliente.
- **Proceso Manual:** El desarrollador debe crear un cliente `gRPC` para iniciar manualmente la conversación, definir los roles de los participantes y transmitir el audio en _streams_.
- **Desventaja:** Requiere un mayor esfuerzo de desarrollo para manejar todo el ciclo de vida de la conversación.

En resumen, si el cliente tiene la opción, **`SIPREC` es el método preferido para la integración de voz**, ya que maneja la complejidad subyacente de la conversación y reduce el esfuerzo de desarrollo.

---

# Integración con la Suite de `Customer Engagement` (SIP/SIPREC)

El objetivo de esta integración es habilitar la inteligencia conversacional de Google, como los agentes virtuales y Agent Assist, sin la necesidad de que el cliente construya una solución de `gRPC` desde cero. Esto se logra mediante el uso de protocolos estándar como SIP y SIPREC para manejar las conversaciones.

---

### Panorama de la Integración

La integración se basa en el **`Google Telephony Platform` (GTP)**, que actúa como un puente. Desde el **`Session Border Controller` (SBC)** del cliente se establece una conexión con GTP, y este convierte automáticamente el audio y la señalización (`SIP`/`SIPREC`) a un formato `gRPC` que la suite de Google entiende. Esto elimina la complejidad de construir y mantener un cliente `gRPC` propio, lo que ahorra tiempo y dinero.

Requisitos de Señalización
- **Etapa de Agente Virtual** - Se requiere **SIP** para audio bidireccional.
- **Etapa de Agent Assist** - Se requiere **SIPREC** para recibir el audio de forma unidireccional.

---

### Configuración en la `Customer Engagement Suite`

La configuración se realiza a través de la API en el **`Conversation Profile`**, ya que aún no hay una interfaz de usuario disponible.
- **`create_conversation_on_the_fly`:** Debe estar activado para que Agent Assist cree una conversación automáticamente.
- **`allow_virtual_agent_interaction`:** Si se configura como **`True`**, el cliente interactuará primero con un agente virtual. Si es **`False`**, la llamada se dirige directamente a Agent Assist.
- **`inactive_start`:** Si se configura como **`True`**, el audio no se envía a Google hasta que se conecte un agente humano, lo que **reduce los costos**.
- **`keep_conversation_running`:** Es crucial para el escalamiento. Si se configura como **`True`**, la conversación del agente virtual puede ser retomada por Agent Assist.
![](https://i.imgur.com/jS4hDbx.png)

---

### Provisionamiento de Números Telefónicos

Para que las llamadas lleguen a la plataforma, debes solicitar números a GTP a través de la API con el mensaje **`PhoneNumberSpec`**. Estos números se asocian al **`Conversation Profile`** correspondiente.
![](https://i.imgur.com/RGCi6DD.png)

---

### Configuración del `Session Border Controller` (SBC) del Cliente

- **Conectividad:** La conexión es segura a través de **`TLS 1.2+`** con conjuntos de cifrado específicos.
- **SIP Trunk:** Se debe crear un `SIP Trunk` para los `hostnames` de Google. Los `SIP Trunks` se comparten entre todos los proyectos de un cliente.
- **Firewall:** Es esencial permitir las IP y los puertos específicos de Google en el firewall del cliente para que el tráfico pueda fluir.
![](https://i.imgur.com/ujWe5wT.png)

---

### Configuración de Encabezados SIP

Para que la plataforma identifique la conversación, el **`SIP INVITE`** debe contener uno de los siguientes encabezados, que tienen un **`payload` en forma de URL** con el ID del proyecto, el ID de la conversación y el propósito:
- **`Call-Info header`**
- **`User-to-User` (UUI) `header`** (con el `payload` codificado en hexadecimal).

**Notas Importantes:**
- El `conversation_id` debe empezar con una letra y tener 64 caracteres o menos.
- Los encabezados UUI pueden usarse para enviar **metadatos**, pero **nunca datos personales (`PII`)**.
- Los valores de estos encabezados **no son accesibles** de forma nativa en un agente virtual. Para usarlos, se debe llamar a un **`webhook`** que obtenga el objeto de conversación y los pase como parámetros de sesión.
- Para llamadas salientes, se debe invertir el orden de los participantes usando el parámetro opcional `roles` en la URL del encabezado SIP.

<iframe width="560" height="315" src="https://www.youtube.com/embed/nkxTki6yK1s?si=pMi0jZKc9E55NnrL" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>