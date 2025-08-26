---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/00 Telephony integrations for Agent Assist/"}
---

# Índice

[[#Integraciones Telefónicas para Agent Assist]]

---
# Integraciones Telefónicas para Agent Assist

Para que Agent Assist pueda ofrecer sugerencias en tiempo real, necesita una **fuente de audio en vivo** de las conversaciones. Hay dos enfoques principales para integrar el flujo de audio de las llamadas telefónicas.

#### Dos Enfoques Principales de Integración
1. **SIPREC (Session Initiation Recording Protocol):**
	- **Función:** Este es un protocolo estándar para la grabación de llamadas.
    - **Flujo:** El cliente usa su **`Session Border Controller` (SBC)** para enviar una copia del audio de la llamada (`Audio Forking`) al **`Google Telephony Platform` (GTP)**, que actúa como servidor de grabación.
    - **Proceso:** El GTP recibe el flujo de audio SIPREC y lo traduce a un formato **`gRPC`** que la IA conversacional puede entender.
    - **Vinculación:** La llamada se empareja con una sesión en Agent Assist a través de un número dedicado, un número temporal o información en los encabezados SIP.
2. **gRPC (Stream Audio):**
    - **Función:** En este enfoque, los clientes envían el audio **directamente** a los _endpoints_ públicos de la API de IA conversacional.
    - **Proceso de Configuración:** La configuración implica crear un perfil de conversación, iniciar una conversación, definir los participantes (agente, usuario final, agente virtual) y luego transmitir el audio usando el método `StreamingAnalyzeContent`.
    - **Nota:** Solo los participantes de tipo `END_USER` o `HUMAN_AGENT` pueden usar `StreamingAnalyzeContent`.

---

### Flujo Completo con SIPREC (Ejemplo)

1. **Duplicación de Audio:** El SBC del cliente duplica el audio de la llamada y lo envía al `endpoint` SIPREC del GTP.
2. **Transmisión:** El GTP reenvía el audio a los agentes conversacionales y a Agent Assist.
3. **Análisis:** Agent Assist se une a la conversación como un **"oyente pasivo"**. Usa la tecnología de voz a texto (`Speech-to-Text`) para transcribir el audio en tiempo real y analizar el contexto.
4. **Enmascaramiento (opcional):** Las transcripciones pueden pasar por herramientas de Prevención de Pérdida de Datos (`DLP`) para enmascarar información sensible.
5. **Sugerencias:** Las sugerencias se envían al escritorio del agente a través de **APIs REST** o **mensajes Pub/Sub**.

---

### Tipos de Flujos de Integración

La integración puede variar dependiendo de la arquitectura del cliente:

- **SIPREC Directo:** El cliente gestiona su propio SBC y la integración de la interfaz de usuario.
- **Plataforma `CCaaS`:** Un proveedor externo, como Twilio o Five9, facilita la integración.
- **Plataforma `Legacy`:** Se utiliza un conector de IA conversacional para soluciones de `OEM` antiguas.
- **Socio `OEM` Nativo:** Un socio `OEM` tiene una integración optimizada a través de `gRPC`.

---

### Resultados y Almacenamiento

- **Almacenamiento:** El audio original y la transcripción pueden guardarse en **`Google Cloud Storage`**.
- **Análisis:** Se pueden integrar los servicios de **`Conversational Insights`** para proporcionar análisis automatizado.
- **Sugerencias:** La transcripción en tiempo real permite a Agent Assist generar sugerencias basadas en el texto y alimentar paneles de control en tiempo real.

![](https://i.imgur.com/iXQ7JUH.png)


![](https://i.imgur.com/V5glSme.png)

![](https://i.imgur.com/KyYXOcJ.png)
