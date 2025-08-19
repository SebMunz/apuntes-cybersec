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

