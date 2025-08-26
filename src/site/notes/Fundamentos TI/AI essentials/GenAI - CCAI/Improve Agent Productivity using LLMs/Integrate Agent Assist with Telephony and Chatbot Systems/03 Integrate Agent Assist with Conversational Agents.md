---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/03 Integrate Agent Assist with Conversational Agents/"}
---

# Inicio

[[#Escalación de agente conversacional al humano]]
[[#Integración de Agente Conversacional con Perfil de Agent Assist]]

---

# Escalación de agente conversacional al humano
### **Flujo de Escalación**

1. **Interacción con el Agente Virtual:** Un usuario final interactúa con un agente conversacional (bot) que intenta resolver todas sus consultas.
2. **Escalación a Agente Humano:** Si el agente virtual **no puede resolver** el issue, la conversación debe escalarse a un agente humano.
3. **Agent Assist Entra en Acción:** Una vez la conversación es transferida al agente humano, **Agent Assist** se activa para ayudar al agente en tiempo real con sugerencias.

---

### **Configuración en Dialogflow (Conversational Agents Console)**

La transferencia se configura en la interfaz de usuario de Dialogflow (Conversational Agents).

- **Paso 1: Crear una Ruta de Transferencia (En la Start Page):**
    - En el flujo del agente, se debe crear una **ruta** (ej: llamada "Agent Transfer").
    - Se debe definir un **intent** con el mismo nombre (ej: "Agent Transfer") que activará esta ruta.
- **Paso 2: Configurar el Intent de Transferencia:**
    
    - **Training Phrases:** Añadir frases de entrenamiento que indiquen la necesidad de hablar con un humano (ej: "I want to talk to a human agent", "I want to cancel my reservation", "Quiero hablar con una persona").
    - **Fulfillment (Respuesta del Agente):** Configurar la respuesta que dará el bot antes de transferir.
        - **Respuesta Simple:** En el campo "Agent response" se puede poner un mensaje como "Let me connect you with a human agent".
        - **Respuestas Enriquecidas:** Usar **custom payloads** o código (if/else) para respuestas condicionales.
    - **Acción Clave:** Incluir el **`live agent handoff` payload** en el fulfillment. Esto es lo que **desencadena físicamente la escalación** al agente humano.
    - **Transición:** Especificar la página a la que se transicionará tras la escalación (ej: una página "Agent Transfer" que gestiona la conexión).

---

### **Resumen del Proceso de Configuración**

1. **Diseñar el Agente:** El agente virtual debe estar diseñado para reconocer intents que requieran escalación.
2. **Crear Intent de Handoff:** Crear un intent específico con frases de entrenamiento relacionadas con la necesidad de un agente humano.
3. **Configurar Fulfillment:** En el fulfillment de ese intent, configurar una respuesta amable y, crucialmente, **incluir el payload de handoff**.
4. **Definir Transición:** Dirigir el flujo a una página que maneje la transferencia.

**Resultado:** Cuando un usuario diga una frase que coincida con el intent de transferencia, el bot responderá y luego pasará automáticamente la conversación a un agente humano, momento en el cual Agent Assist comenzará a proveer asistencia.

---
# Integración de Agente Conversacional con Perfil de Agent Assist

El objetivo es crear un flujo donde un agente virtual de Dialogflow (un `bot`) atienda al cliente primero, y si es necesario, transfiera la conversación a un agente humano, momento en el que Agent Assist se activa para ayudar.

---
### Dos Flujos Posibles

Hay dos maneras de configurar la interacción entre el cliente y el agente.

- **Con Agente Conversacional (Recomendado para autoservicio):** El cliente interactúa con el **bot** primero. Si el bot no puede resolver el problema, escala la conversación a un **agente humano**. Agent Assist se activa en ese momento para ofrecer sugerencias basadas en la conversación previa con el bot.
- **Sin Agente Conversacional:** El cliente es enviado directamente a un **agente humano**. Agent Assist opera desde el principio de la conversación, ofreciendo asistencia en tiempo real.

La elección del flujo se define en el **`Conversation Profile`**.

---

### Pasos para la Integración

1. **Crea o selecciona un agente virtual:** El primer paso es tener un agente conversacional listo en la consola de Dialogflow.
2. **Crea un `Conversation Profile` en Agent Assist:** Este perfil es fundamental, ya que define **qué** sugerencias se muestran y **cuándo**.
    - **Nombre:** Asígnale un nombre único e identificable.
    - **Tipos de sugerencias:** Selecciona las funciones de Agent Assist que deseas usar, como `Smart Reply` o `FAQ Assist`, y vincúlalas a un modelo o a una base de conocimiento, respectivamente.
    - **Configuración de las sugerencias:** Ajusta el número máximo de sugerencias y el umbral de confianza para filtrar las sugerencias irrelevantes.
3. **Configura el flujo con el bot:**
    - Activa **`Enable Conversational Agent`**.
    - Vincula el agente de Dialogflow que creaste en el paso 1.
    - **Configuraciones opcionales:** También puedes activar el análisis de sentimiento para monitorear las emociones en la conversación o las notificaciones de `Cloud Pub/Sub` para recibir mensajes.

---

### Pruebas con el Simulador

El simulador es una herramienta invaluable para probar el rendimiento de las sugerencias antes de implementarlas.

- **Requisito:** Debes tener un `Conversation Profile` configurado.
- **Proceso:** El simulador te permite simular la conversación de un cliente. Cuando el cliente envía un mensaje que activaría el escalamiento, el simulador muestra la interfaz de un **agente humano** con las **sugerencias** de Agent Assist en tiempo real.
- **Ajustes:** Si los resultados no son los esperados, puedes modificar los parámetros en el `Conversation Profile` o en las bases de conocimiento asociadas.

Esta integración crea una experiencia fluida donde la inteligencia del bot se une a la asistencia en tiempo real para agentes humanos, lo que se traduce en una mayor eficiencia y satisfacción del cliente.