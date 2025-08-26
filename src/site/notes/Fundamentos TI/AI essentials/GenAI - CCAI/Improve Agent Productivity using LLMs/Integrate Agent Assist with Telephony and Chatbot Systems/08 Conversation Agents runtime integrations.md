---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/08 Conversation Agents runtime integrations/"}
---

# Integraciones

#### **Propósito de la integración**

- Permite integrar datos de servicios como **Agent Assist** y **Conversational Agents** en **Conversational Insights**.
- Al habilitar la integración, las conversaciones creadas en Agent Assist y Conversational Agents son visibles en Conversational Insights para su análisis.

#### **Pre requisitos de configuración**

1. **Habilitar APIs:**
    - Cloud Storage
    - Speech-to-Text
    - Conversational Agents
    - Insights
2. **Cuenta de servicio:**
    - Crear una cuenta de servicio.
    - Descargar el archivo de clave privada JSON.
    - Otorgar el rol de `Conversational Agents API Admin` a la cuenta de servicio.
3. **Habilitar la función de exportación:**
    - Activar la función de exportación de `Conversational Insights`.

---

### **Opciones de integración (casos de uso)**

#### **1. Crear una conversación en Agent Assist y verla en Conversational Insights**

- **Paso 1:** Crear un perfil de conversación en la consola de Agent Assist.
    - **Importante:** No habilitar la opción `Conversational Agents`.
- **Paso 2 (opcional):** Probar el perfil con el simulador de Agent Assist (ej. para una conversación de Smart Reply).
- **Paso 3:** Manejar las conversaciones mediante llamadas directas a la API (no se puede hacer desde la consola de Agent Assist).
    - **Importante:** Solo las conversaciones completadas son visibles en Conversational Insights.
- **Paso 4:** Navegar a la consola de Conversational Insights y ver la conversación. El nombre de la conversación en Insights coincide con el de Agent Assist.

#### **2. Crear una conversación en Conversational Agents y verla en Insights (usando un perfil)**

- **Paso 1:** Crear un agente de **Conversational Agents** (y opcionalmente importar datos de muestra).
- **Paso 2:** Crear un perfil de conversación, pero esta vez **habilitar la opción `Conversational Agents`** para que el perfil pueda usar el agente recién creado.
- **Pasos siguientes:** Similar al caso anterior, usar las APIs para manejar la conversación y luego verla en la consola de Conversational Insights.

#### **3. Crear una conversación en la consola de Conversational Agents y verla en Insights**

- **Paso 1:** Crear un agente de Conversational Agents.
- **Paso 2:** En la configuración del agente, habilitar el registro de interacción (`interaction logging`) y adjuntar la configuración de seguridad (`security setting`) de los prerrequisitos.
- **Paso 3:** Probar al agente directamente en la consola para crear una conversación de prueba.
- **Paso 4:** Navegar a la consola de Conversational Insights y la conversación de prueba estará visible en el historial.