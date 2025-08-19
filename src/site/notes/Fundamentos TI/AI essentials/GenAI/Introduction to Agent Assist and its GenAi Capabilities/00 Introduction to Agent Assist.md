---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/Introduction to Agent Assist and its GenAi Capabilities/00 Introduction to Agent Assist/"}
---

# Introducción a Agent Assist y Capacidades GenAI

Asistencia generada por un chatbot, especialmente diseñada para **contact centers**.  
Su principal gracia es que puede:
- Generar contenido y respuestas en tiempo real  
- Proponer sugerencias  
- Resumir conversaciones  
- Manejar al cliente antes de pasarlo al agente humano  

---
# Índice
1. [[#Etapas Principales]]
2. [[#Features Principales]]
   3. [[#Etapa 3 – Antes del agente humano]]
   4. [[#Etapa 4 – Durante la asistencia humana]]
5. [[#Detalle de Features]]
   6. [[#Summarization]]
   7. [[#Sentiment Analysis]]
   8. [[#Smart Reply]]
   9. [[#GKA y PGKA]]
   10. [[#Live Transcription]]
11. [[#Regionalización]]
12. [[#Conclusión]]

---
<div class="page-break" style="page-break-before: always;"></div>

# Etapas Principales

1. **Conexión**  
   - El cliente inicia la conversación  

2. **Agente Virtual**  
   - El cliente interactúa con un agente virtual que intenta resolver su consulta  
   - Puede ser bypassed (omitido)  
   - Si no logra resolver → se pasa al agente humano  

3. **Hand-off**  
   - Se transfiere la conversación a un agente humano  

4. **Asistencia de Agente**  
   - Cliente conectado con uno o más agentes humanos  
   - El asistente entrega documentación, sugerencias y respuestas en tiempo real  

5. **Desconexión**  
   - Cierre de la interacción  

> 💡 Para integrarlo en conversaciones de texto se debe usar la **Agent Assist API**.

---
<div class="page-break" style="page-break-before: always;"></div>

# Features Principales

Las funciones clave aparecen en las etapas **3 y 4**.

## Etapa 3 – Antes del agente humano
1. **Summarization**  
2. **Sentiment Analysis**

Sirven para decidir si:  
- Pasar a la **Etapa 4** (resumen para el agente)  
- Terminar en la **Etapa 5** si ya se resolvió  

## Etapa 4 – Durante la asistencia humana
1. **Smart Reply**  
2. **GKA y PGKA**  
3. **Live Transcription**

---
<div class="page-break" style="page-break-before: always;"></div>

# Detalle de Features

## Summarization
- Resumen generado con LLM  
- Disponible en **38 idiomas**  
- Personalizable con templates y estilo  
- UI disponible  
- **Puede extraer entidades**  

## Sentiment Analysis
- Determina la intención emocional: positivo, negativo o neutro  
- Extrae entidades, clasifica y agrega información  
- **Puntaje:** entre -1 y 1  
- **Magnitud:** fuerza de la emoción  

| Sentimiento | Rango de Puntaje |
| ----------- | ---------------- |
| Negativo    | -1.0 ~ -0.25     |
| Neutro      | -0.25 ~ 0.25     |
| Positivo    | 0.25 ~ 1.0       |

## Smart Reply
- Ofrece respuestas sugeridas según la interacción y el entrenamiento  

## GKA y PGKA
- **GKA:** enciclopedia de búsqueda rápida  
- **PGKA:** genera preguntas o respuestas potenciales  
  - *Query Generation:* analiza contexto → queries  
  - *Answer Generation:* entrega respuestas + fuente de corroboración  
- Soporta **bases internas o externas**  
- Es **proactivo, robusto y configurable**  
- Compatible con **38 lenguajes**  

## Live Transcription
- Transcripción en vivo de múltiples idiomas  
- Usa la **API de Google Translate**  

---
<div class="page-break" style="page-break-before: always;"></div>

# Regionalización

- Permite **residencia de datos** para mantenerlos en una región específica  
- Cumple con normativas y mejora latencia en algunos casos  
- No aplica a datos en uso o en tránsito  

**Limitaciones actuales:**  
- Transcripción CES solo soporta datos multi-región en **uso** y en **descanso** (sin Speech Adaptation) en **EU, US y Canadá**  

---
<div class="page-break" style="page-break-before: always;"></div>

# Conclusión

Agent Assist con GenAI representa una capa extra de eficiencia en contact centers:  
- Reduce la carga de los agentes humanos  
- Acelera respuestas con resúmenes y sugerencias inteligentes  
- Aporta información contextual en tiempo real  

Su integración requiere **Agent Assist API** y atención a temas de **regionalización** y **residencia de datos**.
