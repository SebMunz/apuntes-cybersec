---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/01 GenAI w Cloud/"}
---

Une modelos fundacionales con Vertex AI Agent builder para las organizaciones.

Vertex AI Conversation es un tipo de AI que simula conversación humana. Usa NL processing.
Responde preguntas complejas sin mayores configuraciones y agrega capacidades transaccionales como conversaciones multiturno que aprenden del contexto y completar transacciones API

Vertex AI Search es un servicio Cloud que permite construir rápidamente buscadores con GenAI.

Vertex AI es una plataforma end-to-end de ML que permite manejar modelos fundacionales según criterios del usuario.
Vertex AI Agent Builder permite el desarrollo.

---

# Casos de Uso

**Externo** para servir clientes externos a la empresa como eCommerce, Media Serving, Customer Service Support.

**Funcional** para servir aplicaciones internas y soluciones verticales como intranets, bases de conocimiento, repositorios de documentos, etc.

**Técnico** para servir información generada por máquina y automatización de sistemas (Logging, reportes, etc).

---

# Tipos de producto

Hay dos tipos principales de productos:
De consumo y para empresas.

#### Consumo
- Google AI Studio (Maker Suite), Gemini app (bard)
- Ambos usan Gmail como login y lo que le entregues le pertenece a google y usado para mejorar el modelo.
- Usan modelos entrenados en volúmenes grandes de datos, por lo que podrían no ser compatibles con lo que necesita una empresa.

#### Empresas
- Los datos no son recolectados ni usados por Gemini.
- Puedes elegir el tamaño del modelo y sus características

---

# Diferencias

#### GenAI Support in Vertex AI

Entrega APIs que proveen soporte end-to-end
Model Garden
	Entrega variedad de APIs, modelos fundacionales y modelos Open Source que llaman a modelos pre-entrenados para resolver problemas rápidamente
Prompt design y prompt tuning
Ajuste de parámetros y deployment de modelos fundacionales usando interfaz web simple
Se pueden entrenar y ajustar los modelos fundacionales
#### Vertex AI Agent Builder
Provee rápidamente el deployment de agentes con modelos listos, multimodales y ajustables.
Search:
- Google out-of-the-box search
- ajustable
- multimodal
- conversacional
Conversación:
- Single turn
- Multi turn
- Busca información
- Transaccional
- Control de flujo

Si se puede solucionar rápidamente con una solución pre-hecha, usar Agent builder. Si no, y se necesita ajustar y refinar una solución ajustada: usar GenAI Support.

---

# Vertex AI Agent Builder
Para búsquedas y recomendaciones.

Tiene tres elementos principales:
- Search
	- Para construir un search engine con tus propios datos e integrar una barra de búsqueda en la aplicación o página
- Personalized self-serve customer experience
	- Como construir un engine de recomendaciones basado en el usuario y tus propios datos
- Agents
	- complementan DialogflowCX con un chatbot basado en LLM, entrenado en enlaces o documentos para que los usuarios puedan conversar sobre el contenido.

Hay 4 aplicaciones clave:
- Genérico:
	- búsqueda, recomendar sitios web, datos estructurados y no-estructurados (como documentos)
	- ayuda a entender mejor lo que el usuario pretend buscar. mejor que el uso de keywords ya que usa NLP.
- Media:
	- buscar y recomendar contenido multimedia como música, podcast y videos.
	- optimizado para algoritmos según popularidad, engagement, duración, puntaje, etc.
- Retail:
	- capacidades de búsqueda para tiendas online
	- Está tuneado específicamente para predecir ingresos monetarios vs clicks o conversión. además de integrar recomendaciones, búsqueda personalizada, etc.
- Healthcare:
	- buscar información en el formato FHIR (Fast healthcare interoperability resources)
	- a través de FHIR y la API de healthcare, integra recursos relacionados a salud, medicamentos, estudios, observaciones, procedimientos a pacientes, etc. Los usuarios finales no deben usarlo o se estará violando normativas como [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Otras normativas e información susceptible#HIPAA\|HIPAA]]
	- destinado a resumir y buscar información, para nada más, dada la naturaleza de los LLM y GenAI.
