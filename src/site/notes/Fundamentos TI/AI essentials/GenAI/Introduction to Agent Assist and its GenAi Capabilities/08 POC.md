---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/Introduction to Agent Assist and its GenAi Capabilities/08 POC/"}
---

### Requisitos para una Prueba de Concepto (POC) de Agent Assist

Una Prueba de Concepto (POC) para Agent Assist es un paso crucial para demostrar el valor de la herramienta antes de una implementación a gran escala. Para que sea exitosa, requiere una planificación cuidadosa que abarca desde la calificación de la oportunidad hasta la definición de métricas claras.

#### 1. Calificación de la Oportunidad
El primer paso es asegurar que la oportunidad de negocio se alinea con las capacidades de Agent Assist.
- **Objetivos del cliente:** El cliente debe buscar una mejora en la experiencia del cliente y la eficiencia del agente. Específicamente, quieren proporcionar asistencia rápida para manejar más conversaciones con alta calidad.
- **Definición de éxito:** Es fundamental definir **métricas de éxito** claras y medibles desde el principio para demostrar el valor de la POC.

#### 2. Requisitos de Datos por Funcionalidad
Los requisitos de datos varían según la funcionalidad de Agent Assist que se desee probar.
- **Para Smart Messaging (Smart Reply/Compose) y Resumen de Conversaciones:**
    - **Mínimo:** 100,000 conversaciones.
    - **Ideal:** 200,000 conversaciones.
    - **Datos requeridos:** Las conversaciones deben incluir los **roles del hablante** (agente, cliente, chatbot) y las **marcas de tiempo (timestamps)** de los mensajes.
- **Para Resumen de Conversaciones (adicional):**
    - **Metadatos:** Se necesita metadatos para filtrar conversaciones de baja calidad, como la resolución de problemas, el nivel de habilidad del agente, o el puntaje de satisfacción del cliente (CSAT).
    - **Resúmenes:** Se requieren 2,000 notas de resumen de alta calidad, emparejadas con las transcripciones.
    - **Alternativa a los resúmenes:** Si el cliente no tiene resúmenes, se pueden usar 2,000 transcripciones anotadas internamente o 150 transcripciones etiquetadas por tema. Si un tercero realiza el etiquetado, el cliente debe aprobar el acceso a sus datos y proporcionar las políticas de resumen.

**Importante:** Todos los datos deben ser revisados para **excluir cualquier Información Personal Identificable (PII)** antes de compartirlos con Google. Además, los mensajes deben estar ordenados cronológicamente.

#### 3. Equipo para la POC

Para una POC exitosa, se necesita un equipo multifuncional:
- **Equipo de ejecución (`Delivery Team`):** Liderado por un **Delivery Lead**, incluye ingenieros de IA, un equipo de etiquetado, un arquitecto de integración telefónica y un ingeniero de integración de UI.
- **Equipo administrativo (`Administrative Team`):** Incluye roles como el Gerente Técnico de Cuentas, el Gerente de Programa Técnico y el Representante de Ventas.

#### 4. Articulación del Valor de Negocio

El valor de la solución debe ser claramente comunicado:
- **Visión:** Agent Assist es una herramienta que proporciona sugerencias y resúmenes a los agentes.
- **Objetivo:** Usar la inteligencia artificial para automatizar tareas repetitivas, permitiendo a los agentes enfocarse en un soporte al cliente de mayor calidad.
- **Ventaja:** La herramienta proporciona un soporte **proactivo** y relevante en el contexto de la conversación, lo que aumenta la productividad y la efectividad de los agentes.

#### 5. Declaración de Trabajo (Statement of Work - SOW)

El SOW formaliza el acuerdo y los criterios de éxito de la POC.
- **Sección 1: Descripción del Proyecto:** Detalla los objetivos del cliente, los resultados esperados (ej. aumentar una aplicación existente con enlaces a FAQ) y el valor de negocio (ahorros en costos operativos, mayor satisfacción).
- **Sección 2: Criterios de Éxito:** Define los resultados técnicos y de negocio que marcan el éxito. Esto incluye la implementación de modelos e integraciones, la resolución de puntos débiles y el logro de las métricas objetivo.

**Métricas comunes para la POC:**

- **AHT** (Average Handle Time).
- **Tasa de Edición** en resúmenes.
- **First Call Resolution**.
- **Puntuaciones de QA** (Control de Calidad).
- **Precisión** de los resúmenes y de las sugerencias de GKA/PGKA.
- **Word Error Rate** (en caso de transcripción).

El objetivo final de la POC es cumplir estos criterios para formular un plan (`Go-Forward-Plan`) que guíe la implementación de la solución en un entorno de producción.