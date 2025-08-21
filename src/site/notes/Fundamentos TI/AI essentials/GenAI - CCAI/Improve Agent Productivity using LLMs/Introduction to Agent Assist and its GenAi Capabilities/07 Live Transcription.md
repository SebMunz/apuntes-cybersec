---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Introduction to Agent Assist and its GenAi Capabilities/07 Live Transcription/"}
---

### Transcripción en Vivo (Live Transcription)

La transcripción en vivo es una funcionalidad de **Agent Assist** que captura y transcribe en **tiempo real** la conversación entre un agente y un cliente. Esta herramienta es fundamental para el monitoreo y el análisis de las interacciones. Una de sus características más importantes es la **redacción de PII** (Información de Identificación Personal), lo que garantiza la privacidad y el cumplimiento de las normativas de seguridad de datos.

Existen dos tipos de transcripción:

- **Transcripción Final (Final Transcription):** Es el resultado completo y definitivo de la conversación. Es en esta transcripción donde se aplica la redacción de PII para proteger la información sensible.
- **Transcripción Intermedia (Intermediate Live Transcription):** Proporciona resultados interinos (palabra por palabra) a medida que la conversación avanza, permitiendo al agente obtener un contexto inmediato. A diferencia de la transcripción final, esta **no incluye la redacción de PII**, ya que su propósito es ofrecer una visualización instantánea y fluida del diálogo.

---

### Configuración y Seguridad

Para implementar la transcripción en vivo en un entorno de centro de contacto, se requiere una **integración de telefonía (SIP/SIPREC)** con Google. El flujo de datos es el siguiente: el proveedor de telefonía del cliente se conecta a los Agentes Conversacionales, el audio fluye hacia Agent Assist, se transcribe automáticamente y se visualiza en la interfaz de usuario del agente.

La habilitación de la transcripción intermedia se realiza en el **Conversation Profile** de Agent Assist. Para que funcione correctamente, es necesario configurar las notificaciones de resultados de reconocimiento en **Cloud Pub/Sub**, a través del tema **"New recognition result notifications"**.

En cuanto a la **seguridad**, la redacción de datos sensibles (como números de tarjetas de crédito o direcciones) se configura en los **Security Settings** del Conversation Profile. Esta función utiliza una plantilla de **Cloud DLP** (Data Loss Prevention) para inspeccionar y desidentificar la información en la **transcripción final**.

![](https://i.imgur.com/cAqSVmf.png)

---

### Traducción en Vivo (Live Translation)

La traducción en vivo es una herramienta complementaria que permite la **traducción bidireccional en tiempo real**. Su objetivo es facilitar la comunicación entre clientes y agentes que hablan idiomas diferentes, eliminando la barrera del idioma y garantizando que las interacciones se desarrollen sin problemas. El sistema traduce automáticamente las palabras del cliente para el agente y viceversa, permitiendo una comunicación fluida.

#### Características Clave y Flujo de Trabajo

Esta funcionalidad no solo traduce, sino que también incluye características adicionales que mejoran la calidad de la interacción:
- **Corrección Automática:** Realiza correcciones gramaticales y ortográficas en los mensajes para asegurar que la traducción sea lo más precisa posible.    
- **Detección de Idioma:** Es capaz de detectar automáticamente el idioma hablado o escrito, soportando más de **100 idiomas**.

El flujo de trabajo es intuitivo y transparente para el usuario final y el agente:
1. El **cliente** se comunica en su idioma nativo, por ejemplo, **francés**.
2. El sistema de Agent Assist detecta el francés y traduce el mensaje al idioma del agente, por ejemplo, **inglés**.
3. El **agente** lee el mensaje traducido en su interfaz, responde en **inglés** de forma natural.
4. El sistema vuelve a traducir la respuesta del agente al **francés** y se la envía al cliente.

Este ciclo de traducción continua permite que la conversación fluya de manera fluida y sin interrupciones.

---

### Resumen del Módulo de Transcripción y Traducción

Como lo mencionan tus apuntes, la traducción en vivo es parte de un módulo más amplio que incluye la transcripción. En conjunto, estas funcionalidades ofrecen un sistema robusto para manejar interacciones multilingües:

1. **Live Transcription:** Genera una transcripción completa de la conversación en tiempo real. Para proteger la privacidad, la **Información de Identificación Personal (PII)** se redacta en la transcripción final.
2. **Intermediate Transcription:** Para una retroalimentación más rápida, se ofrecen transcripciones intermedias (palabra por palabra) que no contienen redacción de PII, facilitando el contexto inmediato para el agente.
3. **Configuración:** La integración de estos servicios se realiza mediante una **integración telefónica SIP/SIPREC**, que envía el audio de la llamada a Agent Assist para su procesamiento. La transcripción intermedia se habilita a través de **Cloud Pub/Sub**.
4. **Live Translation:** Complementa la transcripción, permitiendo la traducción bidireccional automática para superar las barreras idiomáticas.

En esencia, este módulo convierte una llamada o chat multilingüe en una experiencia fluida, donde el agente y el cliente pueden comunicarse como si estuvieran hablando el mismo idioma.


projects/qwiklabs-gcp-04-8e3c66a30880/locations/global/conversationProfiles/8lsOa1JtS_qVKKbhFlNT3g