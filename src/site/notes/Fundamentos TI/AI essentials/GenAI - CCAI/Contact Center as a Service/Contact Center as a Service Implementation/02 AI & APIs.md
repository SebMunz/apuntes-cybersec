---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Contact Center as a Service/Contact Center as a Service Implementation/02 AI & APIs/"}
---

# Índice
- [#Agent Assist - Casos de uso y mejores prácticas]
- [#Implementación con Virtual Agent]
	- [#Guía de Implementación de Agente Virtual (Dialogflow CX) en CCAI-P (Long)]
	- [#Integración de Agentes Virtuales (Dialogflow) en CCAI Platform (Short)]
- [#API]
	- [#Mensajería SMS Saliente (Outbound) vía API en CCAI Platform]
	- [#Configuración y Uso de las APIs]
	- [#Configuración y Uso de las APIs]
	- [#APIs de CCAI Platform Manager API y Apps API]

---

# Agent Assist - Casos de uso y mejores prácticas

Utiliza la inteligencia artificial para mejorar la eficiencia y la calidad en los centros de contacto. Su objetivo es proporcionar asistencia en tiempo real a los agentes, lo que se traduce en una mejor experiencia tanto para ellos como para los personas.

#### Beneficios Clave

- **Reduce costos:** Los agentes pueden gestionar hasta un **28% más** de conversaciones, lo que disminuye los costos operativos y el tiempo de espera promedio.
- **Mejora la satisfacción del cliente (CSAT):** Al ofrecer respuestas consistentes y de alta calidad, aumenta la satisfacción en un **10%** y simplifica el proceso de entrenamiento para los nuevos agentes.
- **Aumenta la velocidad de respuesta:** Con funcionalidades como **Smart Reply** y el acceso a una base de conocimiento centralizada, se logra un tiempo de respuesta **15% más rápido**, reduciendo la tasa de chats abandonados.
- **Aumenta la satisfacción del agente:** Al reducir la carga de trabajo manual y repetitiva, los agentes se sienten más cómodos y pueden enfocarse en ofrecer un servicio de mayor calidad.

---

### Funcionalidades Principales

Agent Assist ofrece un conjunto de herramientas inteligentes para optimizar cada aspecto de la interacción con el cliente.

- **Respuestas Recomendadas:** Sugiere automáticamente las próximas mejores respuestas basándose en las frases clave del consumidor. El modelo aprende de las conversaciones de los agentes de alto rendimiento para ofrecer sugerencias precisas.
- **Búsqueda en Base de Conocimiento:** Sugiere automáticamente artículos, páginas web y documentos relevantes mientras la conversación progresa. Un **punto azul** en la interfaz del agente indica que hay un artículo disponible.
- **Transcripción en Vivo:** Utilizando Google Insights, transcribe las llamadas en tiempo real. Esto permite que el agente consulte la conversación durante y después de la llamada, eliminando la necesidad de tomar notas manuales.
- **Análisis de Sentimiento:** Esta función, también impulsada por Google Insights, evalúa el sentimiento del cliente en tiempo real a partir de las palabras clave. Notifica a los supervisores cuando detecta un sentimiento negativo o frases de riesgo, permitiendo una intervención proactiva.
- **Resumen Automático:** Combina la transcripción y el análisis de sentimiento para generar un resumen conciso de la interacción. Incluye la situación, la acción del agente, la calificación de satisfacción del cliente y la resolución del problema.

---

### Casos de Uso por Industria

La versatilidad de Agent Assist le permite adaptarse a las necesidades específicas de distintas industrias:

- **Soporte Técnico:** La herramienta busca automáticamente artículos en la base de conocimiento para problemas o modelos de hardware específicos, lo que agiliza la resolución de problemas técnicos.
- **Finanzas:** Proporciona a los agentes información relevante sobre préstamos, documentación, estrategias de inversión y otras herramientas para resolver consultas de forma eficiente.
- **Recursos Humanos (HR):** Cuando un Agente Virtual no puede resolver una consulta y la escala a un agente humano, Agent Assist analiza la interacción y sugiere automáticamente artículos relevantes sobre temas como seguros, días de vacaciones y beneficios.

---

# Implementación con Virtual Agent

### Guía de Implementación de Agente Virtual (Dialogflow CX) en CCAI-P (Long)

Implementar un agente virtual en la plataforma de CCAI-P requiere una configuración cuidadosa que va más allá de simplemente conectar los servicios. Un plan bien estructurado asegura que el agente cumpla su función correctamente, ya sea como punto de entrada de autoservicio o como asistente en una tarea específica.

#### Parte I: Planificación y Configuración en Google Cloud Platform (GCP)
Antes de la integración, es crucial tener el agente de **Dialogflow CX** completamente diseñado, con un claro entendimiento de sus flujos y los puntos de escalamiento.
1. **Crea una Cuenta de Servicio y una Clave JSON en GCP:**
    - En la consola de GCP, crea una **`Service Account`**.
    - Asigna a esta cuenta el rol de **`Dialogflow API Admin`**.
    - Genera una **clave JSON** para la cuenta. Este archivo es la credencial de autenticación que usarás más adelante, así que guárdalo de forma segura.
2. **Crea/Actualiza un Conversation Profile en Agent Assist:**
    - Ve a la consola de **Agent Assist** y selecciona **`Conversation Profiles`**.
    - Crea un nuevo perfil o edita uno existente.
    - Activa e integra el agente virtual: selecciona el agente de Dialogflow CX específico en la sección correspondiente. Es importante recordar que debe existir una relación **1:1** entre un agente virtual y un `conversation profile`.
    - Guarda el perfil.

---

#### Parte II: Conexión y Configuración en CCAI Platform

Estos pasos conectan tu proyecto de GCP con la plataforma de CCAI-P y permiten que el agente virtual sea reconocido.
3. **Conecta la Plataforma en Developer Settings:**
    - En CCAI-P, navega a **`Settings` > `Developer Settings`**.
    - En la sección **`Virtual Agent Platforms`**, crea un nuevo perfil de plataforma.
    - Sube la clave JSON generada en el paso 1.
4. **Configura el Virtual Agent en CCAI-P:**
    - Ve a **`Settings` > `Virtual Agent`**.
    - Selecciona el tipo de agente:
        - **`Customer Support`:** Para autoservicio.
        - **`Task Assistant`:** Para ser invocado por un agente humano.
    - **Configura los detalles:**
        - Asigna un nombre.
        - En el campo `Workflow`, selecciona el perfil de plataforma (Paso 3) y el `Conversation Profile` (Paso 2).
        - Elige el canal (**`Voz`** y/o **`Chat`**). Ten en cuenta que debes configurar un agente **separado** en CCAI-P para cada canal, incluso si usan el mismo agente de Dialogflow.
        - Selecciona los idiomas soportados y activa el soporte para **`DTMF`** si es necesario.
    - **Guarda y activa el toggle** en la lista principal de `Virtual Agents` para que el agente quede operativo. **¡Este es un paso crítico!**

---

#### Parte III: Uso y Gestión del Agente

5. **Gestiona Configuraciones Adicionales:**
    - En **`Operation Management`**, puedes decidir si las interacciones con el agente virtual generarán un registro en el CRM y si se grabarán. **Advertencia:** las grabaciones del agente virtual **no están redactadas**, lo que representa un riesgo de seguridad con información sensible.
    - **Parámetros de datos:** Se pueden configurar a nivel de cola (para los agentes de tipo `Customer Support`) para pasar información del sistema al agente virtual y viceversa. Los valores pueden ser fijos o dinámicos.
6. **Asigna el Agente a una Cola (Solo para Customer Support VA):**
    - Ve a **`Settings` > `Queue`** y selecciona el canal adecuado.
    - En la configuración de la cola, en la sección **`Assign virtual agent`**, selecciona el agente virtual que creaste.
    - Define su disponibilidad (24/7 o según el horario de la cola) y configura una tecla de escape (`*` o `#`) para que los clientes puedan saltar el autoservicio si lo desean.

---
### Integración de Agentes Virtuales (Dialogflow) en CCAI Platform (Short)

El objetivo de esta integración es establecer una conexión segura entre CCAI Platform y los agentes conversacionales de **Dialogflow**, permitiendo que la IA maneje interacciones antes de escalarlas a agentes humanos. El proceso consta de cuatro pasos principales.

#### Paso 1: Configuración de la Autenticación (en Google Cloud Platform)
Para que CCAI Platform pueda comunicarse con tu agente virtual en Dialogflow, se requiere una cuenta de servicio con permisos adecuados.
1. Ve a la consola de Google Cloud del proyecto donde se encuentra tu agente de Dialogflow.
2. Navega a **`IAM & Admin` > `Service Accounts`**.
3. Crea una nueva cuenta de servicio. Asigna un nombre y, en la sección de roles, otorga el rol **`Dialogflow API Admin`**.
4. Genera una clave JSON para esa cuenta de servicio. Es crucial guardar este archivo JSON en un lugar seguro, ya que contiene las credenciales de acceso y será necesario para vincular el agente a CCAI Platform.

#### Paso 2: Vincular GCP a CCAI Platform

Ahora, debes utilizar la clave JSON para conectar tu proyecto de Google Cloud con la plataforma de CCAI.

1. En CCAI Platform, ve a **`Settings` > `Developer Settings`**.
2. Desplázate hasta el panel **`Virtual Agent Platforms`**.
3. Haz clic en **`Add Platform`**, asígnale un nombre, selecciona el servicio **`Dialogflow`** y sube el archivo de la clave JSON que guardaste en el paso 1.
4. Una vez creada la plataforma, asegúrate de que el `toggle` de activación esté en **`On`**.

#### Paso 3: Crear el Agente Virtual en CCAI Platform

Con la conexión establecida, puedes crear la instancia del agente virtual dentro de CCAI Platform.

1. Ve a **`Settings` > `Virtual Agent`** y haz clic en **`Add Virtual Agent`**.
2. **Elige el tipo de agente:**
    - **`Customer Support`:** Para interacciones de autoservicio o derivación antes de pasar a un agente humano.
    - **`Task Assistant`:** Para ser invocado por el agente humano durante una llamada para tareas específicas (ej. procesar un pago).
3. **Configura el agente:**
    - Asigna un nombre.
    - Selecciona la plataforma (el proyecto de GCP) que creaste en el paso 2.
    - Elige el agente de Dialogflow específico.
    - Selecciona el canal (`Voz` para IVR o `Chat` para Web/Mobile SDK). **Importante:** Se requiere una instancia separada en CCAI Platform para cada canal, incluso si se trata del mismo agente en Dialogflow.
    - Selecciona los idiomas que soporta el agente.
4. **Guarda y Activa:** Guarda el agente y asegúrate de que el `toggle` de activación en la lista esté en **`On`**. Este es un error muy común.
#### Paso 4: Asignar el VA a una Cola

El paso final es asociar el agente virtual a una cola específica para que pueda interactuar con los clientes.
1. En CCAI Platform, ve a **`Settings` > `Queue`** y selecciona el canal deseado (ej. `IVR` o `Mobile`).
2. Elige la cola específica a la que quieres asignar el agente virtual.
3. En la configuración de la cola (panel derecho), asigna el agente virtual que creaste en el paso 3.

---

### Solución de Problemas Comunes

- **El agente no aparece en la lista de CCAI:** A menudo, esto se debe a la falta de un **Conversation Profile** en **Agent Assist**. La solución es ir a la consola de **Agent Assist**, crear o editar un perfil, habilitar las funciones necesarias, y luego habilitar y seleccionar el agente de Dialogflow.
- **El agente escala inmediatamente a un humano:** Esto puede ser causado por el uso de etiquetas **`SSML`** que no son compatibles con CCAI. La solución es crear una copia del agente de Dialogflow sin estas etiquetas y usar esa copia para la integración en CCAI Platform.


---


### Asistente Virtual de Tareas (Virtual Task Assistant) en CCAI
El **Asistente Virtual de Tareas** es una herramienta diseñada para gestionar tareas de autoservicio específicas, como pagos o consultas de saldo, de manera segura y automatizada. Su principal propósito es manejar interacciones que involucran **información personal identificable (PII)** o que requieren el cumplimiento de normativas como **PCI DSS**, lo que no puede ser manejado directamente por un agente humano.

#### Integración y Configuración
La clave de este asistente es su integración con **Dialogflow**, lo que permite a las empresas crear asistentes virtuales para tareas sin salir de la plataforma de CCAI. El proceso de configuración se divide en dos partes:

**1. Configuración del Proyecto y Agente:**
- Ve a **`Settings` > `Developer Settings`** para validar que las claves de servicio del proyecto de GCP, donde está alojado el agente de Dialogflow, sean correctas.
- En **`Settings` > `Virtual Agent`**, haz clic en **`Add Virtual Agent`** y selecciona **`Task Assistant`** (no "Customer Support").

**2. Configuración del Asistente:**
- Asigna un nombre al asistente.
- Selecciona el proyecto de GCP y el canal de comunicación (`Chat` o `Voz`).
- Define los idiomas disponibles.
- Configura los **parámetros de datos de sesión** para que la información se transfiera de forma segura entre el asistente y el agente humano a través de metadatos del CRM.
Visualmente, los Asistentes de Tareas tienen un **código de color diferente** a los Agentes Virtuales de soporte estándar, lo que facilita su identificación.

---
### Caso de Uso en Vivo y Beneficios

Imagina un escenario donde un agente humano está en una llamada telefónica con un cliente que quiere realizar un pago. Por regulaciones como **PCI DSS**, el agente no puede recibir los datos de la tarjeta de crédito. Aquí es donde interviene el Asistente Virtual de Tareas.
- El agente, desde su panel de `Smart Actions`, invoca al Asistente Virtual de Tareas.
- El agente humano queda en espera.
- El asistente virtual de Dialogflow toma el control de la llamada y guía al cliente a través del proceso de pago de forma segura, recibiendo los datos sensibles a través de tonos DTMF o voz.
- Una vez que el pago se completa, el asistente devuelve la llamada al agente humano, quien puede continuar con la conversación.
Este flujo de trabajo es **seguro**, cumple con las **normativas** y libera al agente de la carga de manejar información sensible.

#### Datos y Seguimiento
Toda la interacción con el Asistente Virtual de Tareas se registra de manera detallada:
- Se registra en el **`feed de actividad`** del CRM.
- Se capturan **variables de sesión** clave, como el resultado de la transacción o los errores.
- La **transcripción completa** de la interacción con el asistente virtual también está disponible, a menos que se haya enmascarado con una solución de DLP.
Toda esta información es invaluable para el análisis posterior a la llamada, la auditoría y la elaboración de resúmenes de la interacción.

---

# 🤫

1. El propósito principal de entender lo que el cliente necesita es demarcar el viaje del consumidor y los agentes van a manejar para asegurar una construcción correcta de los caminos (a la larga, entender qué hará para saber qué hacer)
2. Cómo deben ser los artículos preparados antes de subirlos a la base de conocimiento? en HTML guardado en forma local
3. Agent Assist reduce costos operacionales logrando que los agentes puedan manejar más conversaciones al mismo tiempo haciéndolos más eficientes en horas peak
4. Lo que hay que considerar antes de habilitar las grabaciones en el CRM para las interacciones que manejan los agentes virtuales: las grabaciones no están redactadas así que pueden traer información sensible.
5. Asegurarse de estar trabajando en el proyecto correcto en la consola de agent assist
6. El sentiment analysis de agent assist se usa para detectar los sentimientos del consumidor usando frases y palabras claves (y agregando un score de magnitud)
7. Integrar dialogflow a un CRM agrega valor al incluir insights para las interacciones DFCX (dialogflow customer experience) y los pasa a los resultados del CRM
8. Al crear una nueva base de conocimiento hay que proveer del nombre y el idioma
9. Para el summary generado por agent assist se incluye la situación, la acción tomada por el agente, el CSRT y la resolución.

---

# API

### Mensajería SMS Saliente (Outbound) vía API en CCAI Platform

El objetivo de la mensajería SMS saliente en CCAI Platform es permitir el envío automatizado de mensajes a los consumidores. Esto se puede lograr de dos maneras distintas, y la elección de una u otra depende del propósito de la comunicación.
#### Dos Métodos Principales

1. **SMS con Sesión (Session-Based SMS):**
    - **Comportamiento:** Al enviar el mensaje, se crea una **sesión de chat activa** en la plataforma. Si el consumidor responde, la plataforma lo enruta automáticamente a un agente humano, permitiendo una conversación bidireccional inmediata.
    - **Caso de uso ideal:** Es la opción perfecta cuando el mensaje inicial tiene una **llamada a la acción** que podría requerir una interacción de seguimiento con un agente, como notificar que un pedido está listo para ser recogido con la opción de responder con preguntas.
2. **SMS sin Sesión (Sessionless SMS):**
    - **Comportamiento:** Este método envía el mensaje de forma unidireccional y **no abre ni reserva una sesión** en la plataforma.
    - **Caso de uso ideal:** Se utiliza para mensajes **puramente informativos** que no requieren una respuesta o una conversación posterior. Algunos ejemplos incluyen:
        - Códigos de verificación (`OTP`).
        - Recordatorios de citas.
        - Confirmaciones de pago.
        - Resúmenes de una interacción con un agente virtual.

---

### Configuración y Uso de las APIs

Ambos métodos se configuran de manera similar y requieren credenciales API para la autenticación.

#### Configuración Común
- **Generar Credenciales API:** En la plataforma de CCAI, navega a **`Settings` > `Developer Settings` > `API Credentials`**. Aquí se crea una credencial que genera un **nombre de usuario (`username`)** y una **clave (`key`)** que actúa como contraseña.
- **Autenticación:** La autenticación es de tipo **Básica (`Basic Auth`)**, donde la `username` es el nombre de la credencial y la `password` es la clave generada.

#### Ejemplos de Uso con Postman

- **Para SMS sin Sesión:**
    - **URL:** Se utiliza el endpoint `.../apps/api/v1/sessionless_sms`.
    - **Cuerpo (JSON):** Se especifican el número de origen (`from_phone`), un array con los números de destino (`to_phones`) y un array con el mensaje (`messages`).
    - **Uso Típico:** Se invoca comúnmente desde un CRM o una función en la nube (`Cloud Function`) para enviar notificaciones automatizadas.

```JSON
{
  "from_phone": "+15558675309", // Número asignado al tenant (que envía)
  "to_phones": ["+1234567890"], // Array con número(s) destino (formato E.164)
  "messages": ["Este es un recordatorio de su cita."] // Array con el mensaje
}
```

- **Para SMS con Sesión:**
    - **URL:** El endpoint es `.../apps/api/v1/outbound_sms`.
    - **Cuerpo (JSON):** Se requiere el número de destino (`end_user_number`) y el número de origen del tenant (`outbound_phone_number`) que debe ser capaz de recibir mensajes entrantes.
    - **Respuesta:** La respuesta de la API es mucho más detallada, ya que incluye un ID de sesión, el tipo y el estado, reflejando que se ha reservado una sesión completa.

```JSON
{
  "end_user_number": "+1234567890", // Número destino (formato E.164)
  "outbound_phone_number": "+15558675309" // Número del tenant capaz de recibir SMS
}
```

**En conclusión**, la elección entre `Session-Based` y `Sessionless` depende del **objetivo de la comunicación**. Si se busca iniciar una conversación con un agente, se utiliza el método con sesión. Si el propósito es únicamente informativo, el método sin sesión es la opción correcta.

---

### APIs de CCAI Platform: Manager API y Apps API

Las APIs de CCAI Platform son la base para la automatización, personalización e integración profunda con otros sistemas. Se dividen en dos tipos principales, cada una con un propósito distinto.

#### 1. Tipos de APIs y su Propósito

- **Manager API:** Su función es **consultar información** sobre el estado y la configuración del centro de contacto. Es una API de lectura, ideal para crear reportes, monitorear el estado de los agentes y colas, o verificar los horarios de operación.
- **Apps API:** Esta API se utiliza para **ejecutar acciones** y funcionalidades. Es una API de escritura y acción que permite, por ejemplo, gestionar usuarios, generar llamadas salientes o consultar el tiempo de espera estimado (EWT).

---

#### 2. Casos de Uso Comunes

Estas APIs potencian la automatización y la eficiencia del centro de contacto de diversas maneras.

**Manager API:**
- **Reporting:** Permite crear dashboards de inteligencia de negocio (BI) que consolidan información de múltiples clientes o `tenants`.
- **Enrutamiento Inteligente:** Un agente virtual puede consultar la API para verificar si el centro de contacto está abierto y tomar una decisión de enrutamiento en tiempo real (escalar a un agente humano o a un buzón de voz).
- **Auditoría:** Se pueden consultar configuraciones de colas para identificar rápidamente problemas de enrutamiento o errores de configuración.

**Apps API:**

- **Gestión de Usuarios:** Simplifica la administración de un gran número de agentes y equipos mediante la importación o edición masiva.
- **Comunicación Saliente:** Permite generar sesiones salientes de llamadas, chats o SMS (con o sin sesión, según el tipo).
- **Optimización del IVR:** Un agente virtual puede consultar el tiempo de espera estimado (`EWT`) de una cola y comunicárselo al cliente, mejorando la experiencia y reduciendo la tasa de abandono.
- **Campañas Outbound:** Facilita la configuración y gestión de campañas de comunicación saliente.

---

#### 3. Autenticación

Para usar las APIs, se requiere un **API Token** que se genera en **`Settings` > `Developer Settings` > `API Credentials`**.

- Este token funciona como la contraseña para la autenticación de tipo `Basic Auth`.
- El token debe usarse solo en el campo de `password`, dejando el campo de `username` vacío.
- **Advertencia:** Si regeneras el token, cualquier configuración o integración existente que lo utilice dejará de funcionar.

---

#### 4. Cómo Usar las APIs (Ejemplo con Postman)

El uso de las APIs es intuitivo, especialmente con herramientas como Postman.

1. **Importar Documentación:** Utiliza los enlaces de la documentación oficial para importar la colección de endpoints en Postman.
2. **Configurar Endpoint:** Selecciona un endpoint (ej., `GET Menu List` de la Manager API). Reemplaza el `subdomain` y `domain` en la URL por los del `tenant` del cliente.
3. **Autenticación:** En la sección de `Authorization`, selecciona `Basic Auth` y pega el API Token en el campo de `password`.
4. **Enviar y Ver Resultados:** Al enviar la solicitud, la respuesta contendrá la información detallada de todas las colas configuradas.

#### 5. Documentación y Recursos Clave

Las APIs son una herramienta poderosa y la documentación es clave para su uso. Puedes encontrar información detallada en los enlaces proporcionados, así como en la sección de Webhooks, que es esencial para que un agente virtual pueda hacer consultas a las APIs.

<a href="https://cloud.google.com/contact-center/ccai-platform/docs/manager-api">Manager API</a>
<a href="https://cloud.google.com/contact-center/ccai-platform/docs/apps-api">Apps API</a>
<a href="https://cloud.google.com/contact-center/ccai-platform/docs/reporting-api">Reporting API</a>
<a href="https://cloud.google.com/dialogflow/cx/docs/concept/webhook">Webhooks</a>

---
# 🤫🤫

1. Uso común de la API de Manager es rutear llamadas basado en las horas de operación
2. Se requiere acceso de admin o desarrollador para generar una API Token
3. Un SMS sessionless se usa generalmente para informaciones
4. La documentación API para el manager y las Apps está en la documentación de cloud contact center
5. Para configurar API requests de SMS en sesión, se necesita el número del usuario, número de teléfono de salida que pueda recibir SMS de entrada y el mensaje
6. Los dos tipos de SMS de salida son basado en sesión y sin sesión
7. Para implementar llamadas API se necesita acceso de admin o desarrollador para generar una API token

