---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Introduction to CES and Conversational Agents/02 Conversational Agents/"}
---

# Índice

[[#¿Qué es?]]
[[#Agente conversacional]]
[[#Arquitectura y consola]]

---

# ¿Qué es?

- Una plataforma para crear interfaces conversacionales.
- Combina **Flujos** (NLU) y **Playbooks** (LLM).
- Se puede integrar en _apps_ móviles, sitios web, sistemas IVR, etc.
- Usa IA generativa para entender el lenguaje natural y dar respuestas rápidas.
- Es escalable, segura y confiable.

---

#### **Tipos de agentes y canales**

- **Tipos de agentes:**
    - **Informativos:** Dan información y responden preguntas frecuentes (FAQ).
    - **Transaccionales:** Ayudan a completar tareas (ej. hacer citas, procesar órdenes).

- **Canales de usuario final:**
    - **Texto/Chatbot:** Interacción por texto (web, SMS, WhatsApp). Puede incluir respuestas ricas (botones, _links_).
    - **Voz:** Interacción en tiempo real por teléfono.
    - **Personalizado/Multimodal:** Para experiencias complejas (mezcla de texto, voz, imágenes).

---

#### **Tecnologías de NLP**

Hay 4 opciones para implementar un agente, según la necesidad:
1. **Basado en intenciones:** Muy determinista. Usa frases de entrenamiento para conversaciones simples (como Siri o Alexa).
2. **Basado en máquina de estado e intenciones:** Controla los caminos de la conversación de forma determinista. Permite un entendimiento más matizado.
3. **Máquina de estado, intenciones y IA generativa:** Combina el control de la máquina de estado con funciones de IA generativa para tareas complejas.
4. **Basado en instrucciones (LLM):** Usa un marco como **ReAct** para que el agente complete una tarea siguiendo instrucciones.

---

# Agente conversacional

#### **¿Qué es un agente conversacional?**

- Aplicación que usa lógica para lograr un objetivo.
- Se basa en 3 componentes principales:
    - **Orquestación:** Configura los pasos, la lógica y mantiene el estado.
    - **Modelos:** La "inteligencia" del agente; razonan sobre objetivos y generan respuestas.
    - **Herramientas:** Conectan el agente a APIs o servicios externos para obtener datos o hacer acciones.

---

#### **Tipos de agentes**

Se puede elegir entre agentes deterministas, parcialmente generativos o totalmente generativos.

- **Agentes totalmente generativos:**
    - Basados en **Playbooks**.
    - Usan **LLMs de Vertex AI** para entender la intención y generar respuestas.
    - Son flexibles y rápidos de desarrollar.
    - Ideales para manejar errores de ortografía, variaciones en el lenguaje, y casos de uso con muchas idas y venidas.
    - Los **Playbooks** se crean con instrucciones en lenguaje natural. Se define un objetivo principal y los pasos a seguir.
    - Usan **Playbook tools** (como OpenAPI) para conectarse a APIs externas. También pueden usar **Funciones** si el cliente final debe ejecutar la acción.
        
- **Agentes deterministas:**
    - Basados en **Flujos**.
    - Tienen caminos y acciones predefinidas, lo que da mayor control y predictibilidad.
    - Requieren más tiempo de diseño, pero son buenos para situaciones que necesitan respuestas exactas (ej. por cumplimiento).
    - Son efectivos para lógicas claras y paso a paso.

---

#### **Agentes híbridos y capacidades generativas**

- Se pueden combinar **Playbooks** y **Flujos** en un solo agente para crear una solución flexible.
- Puedes llamar un flujo desde un _Playbook_, o viceversa.
- **Características generativas para agentes deterministas:**
    - **Generators:** Permiten que los _Flujos_ usen LLMs para generar respuestas en tiempo real. Útiles para resúmenes o para generar texto que se envía a _webhooks_.
    - **Generative Fallback:** Permite que el agente use un _prompt_ para responder cuando no hay una coincidencia de intención. Útil para saludos o para pedirle que repita algo.
- **Data stores (RAG):**
    - Permiten que los **Flujos** y **Playbooks** usen datos externos (sitios web, BigQuery, Cloud Storage) para dar respuestas más precisas y contextualizadas.
    - Es una implementación simplificada de la técnica **Retrieval Augmented Generation (RAG)**.

---

# Arquitectura y consola

#### **Arquitectura y capacidades**

- **Escalabilidad y confiabilidad**: La plataforma es escalable de forma elástica en la nube. Está gestionada por Google, lo que garantiza seguridad, resiliencia y un acuerdo de nivel de servicio (SLA).
- **Manejo de intenciones**:
    - Para preguntas que **sí** coinciden con una intención, un **Flujo** puede usar respuestas programadas o _webhooks_ para obtener datos.
    - Para preguntas que **no** coinciden, se usan soluciones de IA generativa.
- **Soluciones de IA generativa**:
    - **Data Stores**: Se conectan a los documentos o sitios web de la empresa. Permiten a los agentes encontrar respuestas en los propios datos de la organización, como las FAQ.
    - **Generators**: Se usan en un **Flujo** para generar texto o resúmenes de conversación en tiempo real.
    - **Generative Fallback**: Responde cuando la conversación se desvía de la ruta o si el usuario no sigue la conversación como se esperaba.
    - **Playbooks**: Se usan para crear agentes con herramientas para acceder a _data stores_ o aplicaciones externas.
- **Agentes híbridos**: Puedes combinar **Flujos** con **Playbooks** para manejar escenarios complejos.
- **Funciones de voz**: La plataforma tiene herramientas integradas de _speech-to-text_ y _text-to-speech_ para mejorar las experiencias de voz.
- **Integración**: Los agentes se pueden integrar con tecnología de centros de contacto de Google o de terceros para transferir la llamada a un agente humano.

---

#### **Consola de Conversational Agents**

- **Acceso**: Se puede acceder desde la consola de Google Cloud (en **AI Applications**) o directamente en la **consola de Conversational Agents**.
- **Punto de entrada**: Al crear un agente, se elige un **Playbook** (para casos de uso generativos) o un **Flujo** (para casos de uso deterministas) como punto de inicio.
- **Características**:
    - **Consola integrada**: Permite orquestar conversaciones con **Flujos**, **Playbooks** y **Herramientas**.
    - **Visualización unificada**: Un simulador e historial de conversación unificados para ambos tipos de agentes.
    - **Diseño amigable**: Un panel de menú a la izquierda y una barra de menú en la parte superior derecha.
    - **Control de agente**: Más de 77 opciones de configuración disponibles.
    - **Edición simultánea**: Puedes editar recursos relacionados lado a lado, reduciendo la necesidad de cambiar de vista.
- **Vista consolidada**: Hay 5 funciones en una sola vista: previsualización de la conversación, historial, editor de ejemplos, casos de prueba y renderizado de contenido enriquecido.

