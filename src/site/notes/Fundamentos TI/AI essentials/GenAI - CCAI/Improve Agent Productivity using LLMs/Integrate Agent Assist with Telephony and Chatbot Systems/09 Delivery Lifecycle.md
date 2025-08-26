---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/09 Delivery Lifecycle/"}
---

# Índice

a

---
# Discovery phase

### Apuntes sobre el ciclo de vida de una implementación de Agent Assist

#### **Fases de implementación (POC o completa)**
1. **Fase de Descubrimiento**
2. **Fase de Diseño**
3. **Implementación y Pruebas**
4. **Despliegue y Post-lanzamiento**

---

### **Fase 1: Descubrimiento**

- **Paso 1: Comprender los requisitos del negocio**
    - Identificar los requisitos y las funcionalidades de Agent Assist que se necesitan (ej. resúmenes, PGKA, Smart Reply).
    - Evaluar el canal (voz, chat, etc.) donde se implementará.
    - Determinar si se requiere **personalización del modelo**. Es crucial investigarlo a tiempo para adaptar la implementación.
    - Identificar el **ecosistema tecnológico actual:**
        - **Proveedor de telefonía:** Evaluar la viabilidad de su integración con **Conversational Agents**.
        - **Escritorio del agente o CRM:** La integración varía según el proveedor; algunos tienen soluciones listas, otros requieren implementación personalizada.
- **Paso 2: Acceso a datos históricos**
    - Determinar cómo se puede acceder a los datos históricos y en qué formato se encuentran.
    - El audio sin procesar (`raw audio`) debe convertirse a texto (`Speech-to-Text`, `STT`) o a archivos JSON que coincidan con el formato de respuesta de STT.
    - Esta información es clave para **mejorar o ajustar los modelos** subyacentes de Agent Assist.
- **Paso 3: Configuración de Google Cloud**
    - Verificar que el entorno de Google Cloud esté correctamente configurado.
    - Asegurar que se tenga acceso a todos los recursos necesarios (ej. Conversational Agents, Agent Assist, Speech-to-Text, PubSub, Cloud Storage).
    - Considerar la arquitectura: las herramientas de Conversation AI pueden estar en un proyecto, mientras que los datos de conversaciones y documentos en otro.
    - Asegurar que el equipo de negocio tenga el acceso adecuado para desplegar los módulos de backend.
- **Paso 4: Evaluación de la experiencia técnica del equipo**
    - **Integración de la UI:** Verificar si el equipo de implementación tiene la experiencia para integrar los módulos de UI de Agent Assist en su escritorio de agente o frontend.
        - Si no tienen la experiencia, el proveedor de servicios puede ayudar con la integración de telefonía y Salesforce.
    - **Módulos de backend:** Verificar si el equipo puede configurar los módulos de backend de Agent Assist en su entorno.
        - El despliegue del backend requiere componentes adicionales como el **UI connector** y **PubSub Interceptor**.
        - Si no tienen la experiencia, el proveedor de servicios puede ayudar a configurar los módulos de backend predeterminados en el entorno de Google Cloud del cliente.

---

# Design Phase

#### **Arquitectura típica de una implementación**

- **Usuario final y agente:**
    - El usuario llama desde su dispositivo.
    - El agente usa el **Agent Desktop Client** para responder.
- **Proveedor de telefonía:**
    - Conecta al usuario final y al agente.
- **Conversational Agents Telephony Gateway:**
    - Transmite el audio de la conversación de voz a **Agent Assist** como un _stream_.
- **Eventos de Agent Assist:**
    - Son eventos generados por Agent Assist (ej. sugerencias de respuestas, resúmenes).
    - Estos eventos se envían a **Pub/Sub topics**.
- **Módulos de Backend (Backend Modules):**
    - Procesan los eventos recibidos de los _topics_ de Pub/Sub.
    - Funcionan como un _proxy_ para **Conversational Agents** en nombre del escritorio del agente.
    - Envían los eventos procesados al **Agent Desktop** a través de una conexión **Websocket** para una comunicación en tiempo real.
- **Exportación de conversaciones:**
    - Es posible exportar conversaciones desde **Agent Assist**.
    - Las conversaciones se descargan en un bucket de **Cloud Storage**.

---

# Implementation and Testing

- **Visión general:** Una vez que el equipo tiene la arquitectura diseñada, se pasa a esta fase. El enfoque es probar y garantizar que cada función de **Agent Assist** esté configurada correctamente.
- **Herramienta clave:** El **simulador** de Agent Assist simplifica las pruebas.
- **Ejemplos de evaluación de funcionalidades:**
    - **Evaluación de transcripciones:**
        - Simular conversaciones de voz.
        - Evaluar la calidad del texto transcrito generado por el simulador.
    - **Evaluación de Generative Knowledge Assist (GKA):**
        - Usar un conjunto de consultas predefinidas.
        - Calificar las respuestas generadas por GKA.
        - Verificar los documentos y enlaces asociados que se usaron para generar las respuestas.
        - Asegurarse de que las respuestas cumplan con los estándares del cliente.
    - **Evaluación de resúmenes (`Summarization`):**
        - Ejecutar la función de resumen en 30-50 conversaciones históricas.
        - Pedir al cliente que califique los resúmenes.
        - El sistema de calificación debe incluir métricas como **precisión, integridad y corrección**.
- **Pruebas de integración de extremo a extremo (`end-to-end` testing):**
    - Se realizan para asegurar que toda la integración, incluyendo la telefonía, la interfaz de usuario (UI-UX), el escritorio del agente y el backend de Agent Assist, funcione como se espera.
    - Se simulan varias rondas de conversaciones para verificar que cada funcionalidad se comporte de acuerdo con lo esperado.

---

# Deploy and Post-Launch

- **Paso 1: Preparación para la producción**
    - Una vez que las funcionalidades de Agent Assist han sido probadas, es el momento de moverlas al entorno de producción.
    - Si se usaron **modelos personalizados**, estos deben ser migrados del entorno de desarrollo o prueba al de producción.
    - Se debe validar que los modelos funcionen correctamente con un conjunto inicial de conversaciones.
- **Paso 2: Configuración del perfil de conversación** 
    - El perfil de conversación también debe ser replicado en el entorno de producción.
    - Se debe asegurar que todas las configuraciones estén correctas, especialmente la configuración de **Pub/Sub** si se aplica.
- **Paso 3: Monitoreo de la integración de extremo a extremo** 👀
    - Se debe monitorear la integración completa, tanto para la telefonía como para la interfaz de usuario (UI/UX).
    - Se recomienda un **despliegue gradual** del tráfico:
        - Empezar con un **1%** del tráfico para monitorear el rendimiento.
        - Escalar gradualmente a **10%**, **20%** y así sucesivamente.