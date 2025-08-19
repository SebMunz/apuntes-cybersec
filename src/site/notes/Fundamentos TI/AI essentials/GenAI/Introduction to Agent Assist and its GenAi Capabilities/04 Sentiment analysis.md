---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/Introduction to Agent Assist and its GenAi Capabilities/04 Sentiment analysis/"}
---

Feature que analiza los mensajes entre un agente humano y el usuario final para determinar: emotional intent, sea este positivo, neutro o negativo.

Además puede extraer entidades, clasificarlas y proveer información adicional.

Esto debe activarse al crear un agente nuevo o al editarlo.

También se puede hacer desde la Agent Assist console:
1. Settear `enableSentimentAnalysis` a `true` en el `MessageAnalysisConfig`
2. Enviar un `createConversation` request usando `ConversationProfile`
3. Los resultados retornan en `AnalyzeContentResponse.message.sentimentAnalysis`
4. Si existe integración Cloud Pub/sub en el agent assist, también aparecen en `NewMessagePayload`

Las magnitudes fluctuan desde:

| Puntaje      | Sentimiento |
| ------------ | ----------- |
| -1 ~ -0.25   | Negativo    |
| -0.25 ~ 0.25 | Neutro      |
| 0.25 ~ 1     | Positivo    |
