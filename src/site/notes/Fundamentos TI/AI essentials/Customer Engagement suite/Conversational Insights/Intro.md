---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Customer Engagement suite/Conversational Insights/Intro/"}
---

# Intro

Conversational Insights es un asset para manejar contact centers y extraer información de la interacción.

Utiliza LLM de google.

Los archivos de audio pasan por el pipeline de Speech-to-Text (STT) y Data Loss Prevention (DLP) para convertir las grabaciones a transcripciones con [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Otras normativas e información susceptible#Datos regulados\|PII]] redactados.
Puede extraer componentes como temas, highlights, preguntas y resúmenes, también puede extraer metadatos, satisfacción del cliente y la calidad del agente.

Basado en esto, puede realizar coaching del agente, bots mejorados y workflows mas eficientes.

==Se ingresa el input (llamada o transcripción) con PII redactados -> Insights extrae componentes útiles y métricas.
Esto puede ser exportado a BigQuery para integrarlo con Looker.==

# Insights

El módulo de insights extrae la información y esta puede ser exportada a BigQuery/Looker para visualizaciones. 

1. Crear data pipeline:
	- Traer los datos de cloud storage, redactarlo y otorgar metadatos.
	- Estos metadatos se ven en Insights como **labels**
2. Construir y evaluar los modelos personalizados.
	- Esto incluye modelamiento de tópicos, involucrar expertos en temas específicos, crear destacadores personalizados, etc.
3. Extraer valor:
	 - Usar esta información para darle un significado.

Hay 3 personas a las cuales podrían usar esta información:
1. Experience Leader:
	- Objetivo: mejorar la experiencia de usuario
	- Puntos de dolor: Entrenamiento del agente y rotación. entender el historial de clientes
	- Deseos: Nuevos usos para la GenAI, análisis de conversaciones
2. Contact Center Operations Manager:
	- Objetivo: Predecir fuerza laboral necesaria. Asegurar que todo esté en orden (trabajadores y herramientas) para manejar objetivos y carga laboral.
	- Puntos de dolor: predicción y programar tiempos
	- Deseos: Usar la IA para asegurar que se manejan bien las conversaciones y se cumplen objetivos
3. Supervisor de Agentes:
	- Objetivo: Asegurar que los agentes manejan las conversaciones efectivamente y cumplen los objetivos.
	- Puntos de dolor: Entendimiento en tiempo real del performance de los agentes y coaching personalizado, también el burnout del agente.
	- Deseos: usar información personalizada para ayudar a los agentes individuales y mejorar la satisfacción del trabajo

==Insights puede ayudar al contact center management para preparar los datos para análisis, desarrollar taxonomía de temas, resumiendo las conversaciones, monitoreo de problemas de clientes, inspecciones QA, exportar y visualizar datos, generar FAQS.==

