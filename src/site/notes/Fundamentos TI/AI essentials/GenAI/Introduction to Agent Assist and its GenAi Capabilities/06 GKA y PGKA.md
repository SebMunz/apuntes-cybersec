---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/Introduction to Agent Assist and its GenAi Capabilities/06 GKA y PGKA/"}
---

### Asistencia basada en conocimiento (GKA y PGKA)

En el contexto de la asistencia a agentes, existen dos funcionalidades clave que aprovechan el conocimiento para mejorar la interacción:

- **Generative Knowledge Assist (GKA):** Este asistente se activa cuando el agente humano formula una pregunta. Su función es buscar, sintetizar y presentar información relevante de los documentos proporcionados, junto con datos de la conversación y del cliente. Es una herramienta **reactiva**.
- **Proactive Generative Knowledge Assist (PGKA):** Este asistente es **proactivo**. Monitorea la conversación en tiempo real y, de forma automática, sugiere búsquedas o respuestas relevantes basadas en el contexto de la interacción. Actúa como un compañero inteligente que anticipa las necesidades del agente.

Ambas funcionalidades se basan en **Data Store Agents**, que son agentes de IA configurados para buscar y recuperar información de bases de datos o repositorios específicos.

---

### Prerrequisitos y bases de conocimiento

Para que GKA y PGKA funcionen, es fundamental contar con lo siguiente:

- **Conocimiento de Data Store Agents:** Es necesario comprender cómo se configuran y utilizan estos agentes para acceder a las fuentes de datos.
- **Fuentes de datos:** Se requiere una colección de documentos, ya sean públicos o privados, de los cuales el asistente pueda obtener información.

Los **tipos de almacenes de datos (Data Stores)** pueden ser:

- **Públicos:** Repositorios de datos accesibles en internet, como sitios web, páginas de preguntas frecuentes (FAQs) o documentación pública.
- **Privados:** Bases de datos internas de la empresa, manuales de productos, políticas internas, documentos de soporte, etc.

---

### Mejores prácticas para preparar los datos

La calidad de las sugerencias y respuestas de GKA y PGKA depende directamente de la calidad de los datos de origen. La preparación de los documentos es un paso crítico.

**1. Calidad del Contenido:** El contenido de los documentos debe ser:

- **Preciso y exacto:** La información debe ser correcta para evitar respuestas erróneas.
- **Bien estructurado:** Organizar la información con títulos, subtítulos y listas facilita la búsqueda y comprensión.
- **Actualizado:** Se debe asegurar que los datos estén al día. La información obsoleta puede llevar a malas experiencias para el cliente.
- **Conciso y relevante:** Los documentos deben ir al grano, eliminando información innecesaria.

**2. Estructura y Formato del Documento:** La forma en que se estructuran los documentos impacta la calidad de las "snippets" (fragmentos de texto) que se muestran en los resultados:

- **Contenido al inicio:** Las primeras líneas de un documento son cruciales, ya que suelen aparecer como fragmentos de sugerencia. Deben contener la información más vital. Hay que eliminar elementos irrelevantes como fechas o barras de navegación al principio.
- **Prioridad al texto:** Aunque los asistentes pueden procesar varios formatos, es mejor priorizar los documentos basados en texto plano. Los archivos pesados en imágenes, audio o video pueden ser menos eficientes para el análisis.
- **Dividir documentos largos:** Para mejorar la precisión de las sugerencias, se recomienda dividir los documentos que superen las 1,000 palabras en fragmentos más pequeños y manejables.

**3. Relevancia y Mantenimiento:** Mantener la base de conocimiento es un proceso continuo:

- **Adaptación al objetivo:** La base de conocimiento debe estar alineada con el propósito del asistente. Por ejemplo, un agente de soporte técnico necesita documentos sobre resolución de problemas, mientras que un agente de ventas necesita información sobre productos y promociones.
- **Limpieza proactiva:** Se debe revisar y eliminar regularmente los documentos obsoletos o aquellos a los que se accede con poca frecuencia. Esto evita que la base de conocimiento se "ensucie" y que el modelo genere sugerencias irrelevantes.
![](https://i.imgur.com/lTuSlfA.png)

---

### Generative Knowledge Assist (GKA): Integración y Uso

**Función principal de GKA:**

GKA es una herramienta diseñada para potenciar la capacidad de los agentes humanos. Su función principal es permitirles formular preguntas o buscar información relevante durante una conversación con el cliente. Para ello, GKA utiliza **Data Store Handlers** que recuperan datos de documentos o sitios web previamente seleccionados y organizados (curados).

**Ejemplo de uso práctico:**

Imagina que un cliente contacta a un agente para preguntar sobre descuentos en servicios de internet y televisión. El agente, en lugar de buscar manualmente, utiliza GKA para realizar una consulta específica, como "ofertas para clientes existentes de TV e internet". GKA responde de inmediato, proporcionando enlaces a documentos relevantes que contienen la información. El agente puede entonces usar esta información para dar una respuesta precisa y eficiente al cliente. Esta funcionalidad se puede usar en cualquier momento de la conversación para acceder rápidamente a la documentación necesaria.

**Proceso de Integración:**

La integración de GKA en la plataforma de Agent Assist es un proceso sencillo que se realiza a través de la consola de Google Cloud.

1. **Navegación:** Accede a la **Consola de Agent Assist** y selecciona el proyecto deseado.
2. **Perfiles de conversación:** Dirígete a la sección de **"Conversation profiles"**.
3. **Configuración:** Selecciona un perfil de conversación existente o crea uno nuevo haciendo clic en **"Create"**.
4. **Activación:** Dentro de la configuración del perfil, activa la opción **"Generative knowledge assist"**.
5. **Vinculación:** En el menú desplegable, selecciona el **Data Store Agent** que ya has configurado previamente con tus fuentes de conocimiento.
6. **Guardar:** Finalmente, guarda el perfil de conversación para aplicar los cambios.

---

### Resumen general

GKA es una herramienta reactiva dentro de Agent Assist que facilita la búsqueda de información en tiempo real. Se integra fácilmente a través de la consola de Google Cloud vinculando un perfil de conversación a un Data Store Agent, lo que permite a los agentes acceder rápidamente a bases de conocimiento curadas para responder preguntas de los clientes de manera eficiente.

---

### Proactive Generative Knowledge Assist (PGKA)

**PGKA** es una característica avanzada de **Agent Assist** que va un paso más allá de la asistencia reactiva. Su principal función es sugerir **artículos de conocimiento o respuestas de FAQ** a los agentes en tiempo real y de forma proactiva, basándose en el contexto de la conversación con el cliente. Su objetivo es ayudar al agente a encontrar la mejor respuesta posible de manera instantánea, liberándolo de la tarea de buscar manualmente.

#### Funcionamiento y Beneficios

PGKA actúa como un compañero inteligente que escucha la conversación. Cuando el cliente hace una pregunta, PGKA la analiza, busca en las fuentes de conocimiento configuradas (Data Stores) y presenta al agente un resumen relevante con enlaces de referencia.

**Ejemplo de uso:**

1. Un cliente pregunta al agente sobre la **política de devoluciones**.
2. **PGKA** identifica el tema de la conversación y automáticamente genera un resumen conciso de la política, incluyendo hipervínculos a los documentos fuente.
3. El agente utiliza este resumen para responder al cliente de manera rápida y precisa.
4. Más adelante, si el cliente menciona un tema nuevo, como "penalización por pago tardío", PGKA se activa nuevamente y consulta la documentación relevante para ese tema.

Esto ofrece **ventajas clave** como:

- **Velocidad:** Las sugerencias se generan mucho más rápido de lo que un agente podría buscar o teclear una pregunta.
- **Calidad:** PGKA mejora automáticamente las consultas del agente, transformando frases simples como "Descuento" en preguntas contextualizadas como "¿Qué descuentos hay para clientes de Internet Hogar?". Esto asegura que las respuestas sean más precisas.
- **Automatización:** Al reducir la carga cognitiva del agente, le permite concentrarse plenamente en la conversación con el cliente, mejorando la experiencia de servicio.

#### Opciones y Configuración

Puedes configurar el comportamiento de PGKA en la consola de Agent Assist para adaptarlo a tus necesidades.

**Tipos de sugerencias:**

- **Solo generar preguntas:** Esta opción es más rápida. El sistema sugiere consultas de búsqueda, pero no realiza la búsqueda de la respuesta. Esto puede ser útil para escenarios de prueba o para sistemas donde la búsqueda es manejada por otra herramienta.
- **Generar preguntas y buscar respuestas:** Esta es la opción más completa. El sistema no solo genera la consulta, sino que también busca y presenta la respuesta directamente al agente, incluyendo referencias a las fuentes de datos.

**Para habilitar PGKA, sigue estos pasos en la Consola de Agent Assist:**

1. En la configuración de tu **Conversation Profile**, activa la opción **"Generative knowledge assist"**.
2. Vincula el perfil a un **Data Store Agent** que contenga tus documentos de conocimiento.
3. Opcionalmente, puedes activar **"Show all suggested queries..."** para ver todas las consultas potenciales que el modelo genera, incluso si no encuentra una respuesta. Esto es muy útil para depurar y optimizar el rendimiento.
4. También puedes habilitar **"Load proactive answers asynchronously"**. Esta función generará respuestas conversacionales y enlaces a las fuentes automáticamente en el panel de GKA, liberando al agente de tener que hacer clic para ver la respuesta completa.

En resumen, PGKA es una herramienta dinámica que optimiza el flujo de trabajo del agente al anticipar sus necesidades y proporcionar información precisa y contextualizada de forma automática. Esto se traduce en un servicio más rápido y de mayor calidad para el cliente.

---

## Testeo y Monitoreo de PGKA
*   **Metodología Recomendada:**
    *   Usar un **"golden test set"** de ~20 conversaciones.
    *   Cada conversación debe tener turnos marcados con:
        *   Las preguntas que se espera que PGKA genere.
        *   Las respuestas esperadas.
*   **Herramientas:**
    *   Actualmente **no hay herramientas de testeo** integradas.
    *   Se debe escribir un **script** personalizado para realizar las pruebas.
*   **Solución de Problemas:**
    *   **Opción 1:** Actualizar a las **últimas versiones** de PGKA.
    *   **Opción 2:** Corregir problemas de audio, por ejemplo, ajustando el modelo de **speech-to-text** que se esté utilizando.

---

### GKA/PGKA vs. FAQ Assist/Article Suggestion

La principal diferencia entre estos dos grupos de herramientas radica en la tecnología subyacente y la forma en que procesan y presentan la información. Las herramientas más recientes, GKA y PGKA, utilizan la potencia de la IA generativa, mientras que las anteriores se basaban en el procesamiento del lenguaje natural.

#### GKA y PGKA (Generación con IA)

Estas herramientas representan la nueva generación de asistentes, impulsadas por **Grandes Modelos de Lenguaje (LLMs)** y **embeddings**.

- **Fuente de Datos:** Utilizan **Data Stores** (almacenes de datos).
- **Configuración:** La indexación y configuración de los datos es **rápida**, completándose en cuestión de minutos.
- **Funcionamiento:** Su principal característica es que **generan respuestas** nuevas y contextualizadas a partir de la información de sus fuentes.

#### FAQ Assist y Article Suggestion (NLU Tradicional)

Estas funcionalidades son las predecesoras, basadas en modelos de **Procesamiento del Lenguaje Natural (NLU)**.

- **Fuente de Datos:** Se alimentan de **Bases de Conocimiento (Knowledge Bases)**.
- **Configuración:** El proceso de configuración y entrenamiento es **lento**, pudiendo tardar más de un día.
- **Funcionamiento:** A diferencia de las herramientas GenAI, su función es **sugerir respuestas o documentos ya existentes** que coincidan con la pregunta del cliente.

---

### Descripción de cada herramienta

#### FAQ Assist

FAQ Assist está diseñado para ayudar a los agentes a responder preguntas frecuentes. Su función es sugerir respuestas directas y predefinidas a las consultas más comunes de los clientes.

- **Uso:** Ideal para situaciones donde las preguntas y respuestas son repetitivas y estandarizadas, como horarios de atención o políticas de la empresa.
- **Implementación:** Su uso en tiempo real (runtime) requiere una llamada a una **API**. La consola solo se utiliza para probar la funcionalidad durante la fase de diseño.

#### Article Suggestion

Article Suggestion se enfoca en recomendar documentos completos o artículos relevantes al agente. En lugar de una respuesta corta, sugiere un documento que podría contener la solución o la información detallada que el agente necesita.

- **Modelos:**
    - **Modelo Base (`Baseline`):** Un modelo predefinido por Agent Assist que no requiere entrenamiento con datos específicos de tu empresa.
    - **Modelo Personalizado (`Custom`):** Un modelo que puede ser entrenado con tus propios datos de conversaciones para mejorar la precisión y relevancia de las sugerencias. Para esto, es necesario contactar a Google.
- **Implementación:** Al igual que FAQ Assist, se implementa a través de una **API** para su uso en tiempo de ejecución, mientras que la consola sirve como un entorno de prueba.

---

### Resumen General

GKA y PGKA son herramientas modernas y rápidas que usan IA generativa para crear respuestas a partir de tus datos. FAQ Assist y Article Suggestion son herramientas más tradicionales que utilizan NLU para sugerir respuestas o documentos existentes. GKA y PGKA **generan**, mientras que las herramientas de NLU **sugieren**.

