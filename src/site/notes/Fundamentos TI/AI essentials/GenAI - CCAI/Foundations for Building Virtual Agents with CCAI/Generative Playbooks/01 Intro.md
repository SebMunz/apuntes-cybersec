---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Generative Playbooks/01 Intro/"}
---

# Índice

[[#Playbooks en Conversational Agents]]
[[#La arquitectura ReAct y los Playbooks]]

---

# Playbooks en Conversational Agents

**Playbooks** es una característica que permite a los desarrolladores crear experiencias de chat y voz usando **lenguaje natural**. En lugar de definir flujos, páginas e intenciones, se usa un lenguaje de instrucciones para construir soluciones.

#### **Ventajas de usar Playbooks**

- **Desarrollo rápido y flexible:** Al usar instrucciones en lenguaje natural, se elimina la necesidad de un desarrollo manual largo, lo que acelera la creación de prototipos.
- **Orquestación de la IA generativa:** Permite definir flujos de trabajo de principio a fin, lo que hace que los agentes sean más flexibles y adaptables.
- **Uso de herramientas:** Los _Playbooks_ pueden acceder a **APIs** y bases de datos para realizar operaciones como Crear, Leer, Actualizar y Borrar (CRUD).
- **Menor equipo de desarrollo:** Su rapidez y flexibilidad permiten trabajar con equipos más pequeños, lo que es ideal si los recursos son limitados.
- **Iteración rápida:** Facilitan ciclos de desarrollo y prueba más cortos, permitiendo mejoras continuas en los flujos.

#### **Casos de uso ideales para Playbooks**

- **Asistencia creativa:** Como la creación de historias, donde la flexibilidad es clave.
- **Resolución de problemas (`troubleshooting`):** Permiten un proceso orgánico y menos estructurado, ya que los usuarios pueden haber probado diferentes soluciones.
- **Asistentes conversacionales:** Para tareas como ordenar comida en un _drive-thru_, planificar viajes o dar asesoría financiera.
- **Requisitos de _statefulness_ flexible:** Cuando el orden de las operaciones no es tan estricto y las interacciones pueden ser más conversacionales.

#### **Casos de uso NO apropiados para Playbooks**

- **Reglas de negocio estrictas:** No son ideales para casos que requieren respuestas con una redacción exacta o que tienen un impacto legal (ej. términos y condiciones). Para esto, es mejor usar **Flujos**.
- **Procedimientos muy rígidos:** Cuando la conversación debe seguir una secuencia de pasos exacta sin desviaciones. Los **Flujos** ofrecen un mayor control.
- **Funciones fuera de las capacidades de los LLMs:** No están diseñados para cálculos matemáticos complejos, entender eventos actuales o realizar un etiquetado de voz (`SSML`). Para estas tareas, es mejor usar funciones o APIs externas.

---
# La arquitectura ReAct y los Playbooks

La transcripción explica cómo funciona el patrón de diseño **ReAct (Reasoning and Action)** y cómo es implementado por los **Playbooks** de Google Cloud.

#### **¿Qué es ReAct?**

ReAct es una técnica de **ingeniería de _prompts_** que permite a los Modelos de Lenguaje Grandes (**LLMs**) resolver problemas al combinar el **razonamiento** y la **acción**. En lugar de dar una respuesta final de inmediato, el modelo sigue un ciclo repetitivo:

1. **Thought (Pensamiento):** El LLM razona internamente sobre cómo abordar la tarea o la pregunta.
2. **Action (Acción):** El LLM decide qué hacer para conseguir la información o realizar la tarea. Esto implica interactuar con un sistema externo, como una API.
3. **Observation (Observación):** El LLM recibe la respuesta del sistema externo (la acción) y la analiza.

Este ciclo de **pensamiento -> acción -> observación** se repite hasta que el LLM tiene la información necesaria para formular una respuesta final.

#### **Aplicación de ReAct en Conversational Agents**

- En **Conversational Agents**, el modelo que sigue el ciclo ReAct es el **Playbook**.
- Para conectar un _Playbook_ a un sistema externo (como una base de datos o una API), se utiliza una **Playbooks Tool**.
- Esta herramienta se define usando el formato **OpenAPI**, que describe la estructura del _endpoint_ de la API externa.
- De esta manera, un _Playbook_ puede, por ejemplo, hacer una "acción" para consultar una base de datos de productos (que sería el "sistema externo") y luego usar la información (la "observación") para responder al usuario.

En resumen, los **Playbooks** usan la arquitectura **ReAct** para actuar de forma inteligente. No solo "piensan", sino que también realizan "acciones" en el mundo real (fuera de su modelo de lenguaje) para dar respuestas más precisas y útiles, como si estuvieran siguiendo un plan paso a paso.

---

