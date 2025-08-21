---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Contact Center as a Service/Contact Center as a Service Implementation/01 Contact Center as a Service Fundamentals/"}
---

# Índice
- [[#Queues]]
	- [[#Casos de Estudio Estructuras de Colas Avanzadas en CCAI-P]]
	- [[#Creación de Colas Multi-idioma en CCAI Platform]]
	- [[#Personalización de Idiomas y Mensajes para Colas]]
- [[#Idiomas]]
	- [[#Configuración de Idiomas y Localización para Agentes]]
	- [[#Resultado y Monitoreo]]
	- [[#Idiomas y mensajes]]
- [[#Llamadas y redireccionamiento]]
	- [[#Puntos de Acceso Directo (DAPs) en CCAI Platform]]
	- [[#Configuración de un DAP para IVR]]
		- [[#Configuración básica (tipo "Número de Soporte")]]
	- [[#Opciones de Desvío de Llamadas en CCAI Platform 📞]]
	- [[#Desvíos (Deflections) en Google CCAI Platform]]
		- [[#Habilitación y Configuración]]
	- [[#Configuración Global]]
		- [[#Configuración por Cola (Nivel Específico)]]
	- [[#Enlaces de Desvío Externo y Redirección Automática]]
		- [[#Desvíos Enlaces Externos y Redirección Automática]]
		- [[#Configuración]]
	- [[#Resumen General]]
- [[#Mensajería SMS en CCAI Platform]]
- [[#🤫]]

---

## A saber antes de comenzar: 

Para conectarse a la plataforma CCAI se puede usar SSO con:
Standard SAML, Azure, Idaptive, Okta, OneLogin, Ping, Google Workspace
<a href="https://cloud.google.com/contact-center/ccai-platform/docs/sso">Referencia</a>

También se deben agregar usuarios de forma manual.
<a href="https://cloud.google.com/contact-center/ccai-platform/docs/add-edit-user">Referencia</a>

---

## Queues
### Casos de Estudio: Estructuras de Colas Avanzadas en CCAI-P

El enrutamiento tradicional de un centro de contacto a menudo se queda corto ante la complejidad de las operaciones modernas. Los siguientes casos de estudio demuestran cómo se pueden usar las colas en CCAI-P de manera creativa para resolver desafíos como menús de desvío, repetición de opciones, colas en cascada y selección de idioma.

#### Caso 1: Múltiples Opciones de Desvío a Nivel de Cola

Aunque por defecto CCAI-P solo ofrece una opción de desvío directa por cola, se puede crear un menú de desvío complejo utilizando sub-colas.
- **Problema:** Una cola se desvía por sobrecapacidad (`Overcapacity Deflection`). En lugar de enviarlos a un solo destino, el cliente necesita ofrecer varias opciones.
- **Solución:** La cola principal se desvía a una **cola-menú**. Esta cola ofrece opciones como dejar un correo de voz o ser redirigido a un grupo de colegas. Cada opción es una sub-cola que tiene habilitado el `auto-redirect` hacia su destino final (buzón de voz, otra cola, etc.). Este mismo método se aplica a los desvíos por horarios fuera de servicio (`after-hours deflection`).
![](https://i.imgur.com/pUEtdj2.png)
![](https://i.imgur.com/uIfat11.png)   
#### Caso 2: Repetir Menús

Para permitir que los clientes repitan un menú, se puede utilizar una opción de redireccionamiento dentro de la propia cola.
- **Solución:** Dentro de la lista de opciones de una cola, se añade una que redirige al usuario de vuelta a la cola principal (`top-level`). Esto permite al cliente escuchar el menú nuevamente, en lugar de ser forzado a seguir un camino que no desea.
![](https://i.imgur.com/rMcds3d.png)

#### Caso 3: Colas en Cascada (Overflow Queues)

Las colas en cascada son útiles para gestionar la disponibilidad de agentes que trabajan en diferentes horarios, como en equipos globales.

- **Funcionamiento:**
    1. Se crea una serie de colas, cada una con su propio horario de operación.
    2. El desvío por horario (`after-hours deflection`) de cada cola apunta a la siguiente cola en la secuencia horaria.
    3. Se asigna un único **Número de Acceso Directo (DAP)** a la primera cola.
    4. Cuando el horario de una cola termina, el flujo se desvía automáticamente a la siguiente cola en la cadena, asegurando una cobertura continua. Si la llamada llega fuera del horario de la última cola, se redirige a un buzón de voz general.
![](https://i.imgur.com/slkJa77.png)


#### Caso 4: Selección de Idioma mediante Colas

Este método ofrece una alternativa a la selección de idioma en el IVR inicial, permitiendo que el cliente elija su idioma en cualquier punto del flujo de llamadas.

- **Funcionamiento:**
    1. Se crean colas específicas que le piden al cliente seleccionar un idioma.
    2. Según la opción seleccionada, la cola utiliza `auto-redirect` para enviar la llamada a una sub-cola configurada en ese idioma (ej. portugués).
    3. Estas sub-colas contienen todo el flujo de trabajo específico para ese idioma, de forma aislada de los demás.
- **Ventaja:** Esta estructura permite que la selección de idioma se adjunte a cualquier **Punto de Acceso Directo (DAP)**, dándole una gran flexibilidad al sistema.   
![](https://i.imgur.com/mmxGHzu.png)
![](https://i.imgur.com/zMf1rnC.png)
![](https://i.imgur.com/roTlZsW.png)

En conclusión, la flexibilidad en la configuración de las colas de CCAI-P permite diseñar soluciones creativas y adaptadas para el enrutamiento, horarios, menús y soporte multi-idioma.

---

### Creación de Colas Multi-idioma en CCAI Platform

El soporte multi-idioma es fundamental para expandir el alcance de un centro de contacto y mejorar la experiencia de consumidores internacionales. La plataforma CCAI soporta más de 20 idiomas, y su configuración se realiza mediante una serie de pasos secuenciales y bien definidos.

#### 1. Estructura de Colas Base

El primer paso para habilitar colas multi-idioma es construir la estructura base en un idioma principal, típicamente el inglés. Esto asegura que la lógica de enrutamiento y las relaciones entre colas queden establecidas antes de añadir las traducciones.
- **Acceso a la configuración:** Inicia sesión en la plataforma CCAI y navega a `Settings` -> `Queue` -> Selecciona el canal `IVR`.
- **Creación de la estructura:** Utiliza el botón `Edit` para crear las colas y sub-colas. Para anidarlas, simplemente usa la tecla `Tab` después de escribir el nombre.

Un ejemplo de estructura podría ser:
- Cola de nivel superior (`Top Level Queue`)
    - Sub-cola (`Sub Queue`)
        - Sub-cola final 1 (`Sub Leaf 1`)
        - Sub-cola final 2 (`Sub Leaf 2 (FR)`)

#### 2. Adición y Personalización de Idiomas

Una vez que la estructura base está lista, puedes añadir los idiomas adicionales y personalizar los nombres de las colas.
- **Añadir un idioma:** Ve a `Settings` -> `Languages and Messages`, haz clic en `Add a language` y selecciona el idioma deseado (por ejemplo, francés).
- **Personalizar colas:** Haz clic en `Customized queues` junto al idioma recién añadido. Aquí podrás ver la estructura base y escribir los nombres de las colas directamente en el nuevo idioma. La cola específica para el nuevo idioma (ej. "Sub Leaf 2 (FR)") debe ser activada añadiéndole agentes.
#### 3. Asignación de Agentes y Mensajes

El paso final es vincular a los agentes a las colas y configurar los mensajes de voz.
- **Asignar agentes:** En la configuración de cada cola, tanto en el idioma base como en los personalizados, debes asignar manualmente a los agentes. Para ello, selecciona `Human agent`, haz clic en `Edit`, añade los nombres de los agentes y guarda.
- **Configurar mensajes:** Es crucial que todos los mensajes de voz estén correctamente configurados para cada cola e idioma. Visita la sección `Languages and Messages` para verificar que los mensajes estén habilitados y traducidos.

Este proceso permite implementar colas en múltiples idiomas, proporcionando una solución de enrutamiento flexible y efectiva para un centro de contacto global. La documentación técnica online de Google Cloud sirve como una referencia detallada para cualquier consulta adicional durante la configuración.

---

### Personalización de Idiomas y Mensajes para Colas

Para configurar soporte en un nuevo idioma en CCAI Platform, el proceso se divide en la adición del idioma y la posterior personalización de los mensajes y la estructura de colas. La ubicación principal para estas configuraciones es **`Settings` > `Languages & Messages`**.

#### 1. Añadir y Personalizar un Nuevo Idioma
Primero, debes añadir el idioma a tu configuración.
1. Haz clic en **`Add Language`**.
2. Selecciona el idioma deseado de la lista (ej., **Alemán / German**).
3. Una vez añadido, el sistema te pedirá que personalices dos aspectos clave: los mensajes (`Customize messages`) y las colas (`Customize queues`).

Finalmente, haz clic en **`Go Live`** para activar el idioma en la plataforma.

#### 2. Personalización de Mensajes Audibles

Los mensajes audibles son aquellos que se reproducen para los clientes. Estos se configuran en la sección **`Audible Messages`** y se organizan por idioma y canal (ej., IVR).
- **Selección:** Utiliza los menús desplegables para elegir el idioma (ej., German) y el canal (ej., IVR).
- **Alcance:** Los mensajes audibles se utilizan tanto en el IVR como en aplicaciones móviles.
- **Ejemplos de configuración:** Puedes editar mensajes predefinidos como **`Ask Permission to Record`** para la grabación de llamadas o **`Over Capacity Deflection`** para el desvío por sobrecapacidad. La plataforma proporciona un valor predeterminado usando texto a voz (TTS), que puedes editar o usar como plantilla para tus propias grabaciones.

#### 3. Creación de Colas en el Nuevo Idioma

Una vez configurados los mensajes, debes adaptar la estructura de colas para el nuevo idioma.
1. Ve a **`Settings` > `Queue`** y selecciona el canal de tu interés (ej., **Mobile**).
2. Haz clic en **`Edit`** junto a **`Mobile Menu Structure`**.
3. Desplázate a la sección del nuevo idioma (ej., German support).
4. Para añadir una cola, haz clic en la última cola existente, presiona **`Enter`** para crear una nueva y nómbrala. Confirma los cambios haciendo clic en **`Done`** en la parte superior.
5. **Configuración de la cola:**
    - En **`Queue Menu Settings`**, selecciona el idioma (`German`) en el menú desplegable.
    - En **`Mobile Menu Structure`**, selecciona la cola que acabas de crear.
    - Configura los ajustes que aparecen a la derecha, incluyendo los ajustes de canal y la asignación de agentes, para que la cola cumpla con los requisitos.

---

## Idiomas
### Configuración de Idiomas y Localización para Agentes

El objetivo de este proceso es asegurar que la interfaz de usuario que ven los agentes esté configurada en su idioma predeterminado, mejorando su experiencia y eficiencia. Esto se logra asignando una "localización" a cada agente.

#### 1. Añadir una nueva localización

Primero, debes crear la configuración de localización que incluirá la ubicación y el idioma deseado.
- Ve al menú **`Settings`** y selecciona **`Operation Management`**.
- Desplázate hasta la sección **`Localization`** y haz clic en **`Manage Location Setting`**.
- En la página de Localización, haz clic en **`Add Location`**.
- Introduce un nombre para la ubicación (ej. "Madrid") y selecciona el idioma asociado (ej. "Español").
- Haz clic en **`Save`**. La nueva localización aparecerá en la lista y estará disponible para su asignación.

---

#### 2. Asignar la localización a un agente

Una vez que la localización está creada, puedes asignarla a usuarios específicos.
- Ve a **`Settings`** y selecciona **`Users & Teams`**.
- Busca al agente deseado utilizando la barra de búsqueda en la sección **`All Users`**.
- Haz clic en el ícono de lápiz (editar) que se encuentra junto al nombre del agente.
- En el cuadro de diálogo de edición, busca el menú desplegable **`Location`** y selecciona la localización que creaste previamente.
- **Guarda** los cambios.

---

#### Resultado y Monitoreo

Una vez que el agente se ha asignado a una localización:
- La próxima vez que inicie sesión, su interfaz de usuario (`adaptador de UI`) se cargará automáticamente en el idioma por defecto asociado a esa localización.
- Desde el **dashboard** de la plataforma, puedes acceder a la página de **monitoreo de agentes**, donde podrás ver y filtrar a los agentes por la localización que se les ha asignado. Esto facilita la gestión de equipos multilingües y distribuidos.

---

### Idiomas y mensajes

Múltiples idiomas pueden ser activados y usados en los canales.
<a href="https://cloud.google.com/contact-center/ccai-platform/docs/customizing_languages_recordings_messages">Doc de referencia</a>

Existe una forma para monitorear las llamadas sin que el agente se entere.
<a href="https://cloud.google.com/contact-center/ccai-platform/docs/Call_and_Chat_Settings#UUID-b1c9ad4f-7040-f07d-7285-149986354846_id_900007077563_id_h_01F5FYXEP2NQPKK0N1RGR5KH1M">Doc con guía</a>

---

## Llamadas y redireccionamiento
### Call and chat routing design

<a href="aqui va un enlace">referirse al pdf</a>

---

### Puntos de Acceso Directo (DAPs) en CCAI Platform

Un **Punto de Acceso Directo (DAP)** es una entrada configurada en una cola específica que **omite el menú principal** para los consumidores. Su propósito es simplificar la navegación y acelerar el enrutamiento, permitiendo a los clientes llegar a la cola correcta de forma más rápida y eficiente.

Los DAPs son herramientas muy útiles para:
- Gestionar múltiples unidades de negocio.
- Ofrecer distintos puntos de contacto o idiomas.
- Simplificar la navegación en estructuras de colas complejas.
- Proporcionar mensajes de bienvenida personalizados por punto de acceso.
- Permitir el enrutamiento personalizado desde un CRM o una API externa.

Existen varios tipos de DAPs que se pueden usar de forma individual o combinada en un mismo canal, y tienen un orden de operación predeterminado que se debe considerar.

#### Ejemplos de uso de DAP

1. **DAP de Segmento de Usuario (`User Segment DAP`)** Este tipo de DAP se usa para enrutar clientes basándose en su segmentación en un CRM.
    - **Caso de uso:** Enviar clientes "en riesgo" a un equipo de retención especializado.
    - **Configuración:** Requiere habilitar la opción `allow CRM access` en los ajustes de `Operation Management`. Luego, se crea una cola específica para estos clientes y se asigna un DAP que busca un valor concreto en el CRM del usuario, como `my_risk = true`.

2. **DAP de Número de Soporte (`Phone Number DAP`)** Este DAP permite enrutar a los clientes basándose en el número de teléfono que marcan.
    - **Caso de uso:** Asignar números de teléfono distintos para diferentes idiomas o secciones de negocio. Por ejemplo, un número para inglés que rutea directamente al flujo en inglés con un mensaje de bienvenida único, y otro para español.
    - **Ventaja:** Proporciona flexibilidad y un enrutamiento más rápido, ya que el cliente no tiene que navegar por un menú de idioma.

3. **DAP de API (`API DAP`)** Este DAP se conecta a una API externa para obtener información en tiempo real y enrutar la llamada basándose en la respuesta recibida.
    - **Caso de uso 1:** Enrutar la llamada a una cola específica dependiendo de un valor devuelto por la API. Por ejemplo, si la API devuelve el valor `ESD` para la clave `business`, la llamada se enruta a la cola corporativa `ESD`.
    - **Caso de uso 2:** Utilizar una base de datos externa para determinar el agente asignado o el idioma preferido de un usuario, y luego enrutar la llamada correctamente.

Los DAPs ofrecen una gran flexibilidad para diseñar puntos de entrada a la medida, adaptándose a las necesidades de enrutamiento más complejas de un centro de contacto. La documentación técnica de Google Cloud ofrece más detalles sobre su configuración y uso.

---

### Configuración de un DAP para IVR

Un **Punto de Acceso Directo (DAP)** en el canal IVR es una herramienta clave para mejorar la experiencia del cliente, ya que le permite conectarse automáticamente a la cola correcta **sin tener que navegar por un menú largo**. Esto acelera el proceso de contacto y mejora la satisfacción del usuario.
#### Configuración básica (tipo "Número de Soporte")
Este ejemplo se centra en la configuración de un DAP que utiliza un número de teléfono específico como punto de entrada.
- **Navegación:** En la plataforma de CCAI, navega a **`Settings`** -> **`Queue`** -> selecciona la sección **`IVR`** y haz clic en **`Edit/View`**.
- **Selección de la cola:** Navega por la estructura de colas y selecciona la sub-cola de destino a la que deseas que el DAP dirija a los clientes (ej., `Sales and Marketing` > `Become a Partner`).
- **Creación del DAP:** Dentro de la configuración de la cola, busca la sección **`Access Point`** y haz clic en **`Create direct access point`**.
- **Configuración del DAP:**
    - **Tipo de Punto de Acceso (`Access Point Type`):** Selecciona **`Support Phone Number`**.
    - **Nombre del Punto de Acceso (`Access Point Name`):** Asigna un nombre descriptivo (ej., "Becoming a Partner").
    - **Número de Teléfono (`Support Phone Number`):** Introduce el número de teléfono que será el punto de entrada directo a esta cola.
    - **Mensaje de Bienvenida (`Greeting Message`):** Elige la opción **`Text-to-speech`** y escribe un mensaje personalizado que el cliente escuchará al llamar a ese número.
- **Crear:** Haz clic en **`Create`** para finalizar.

**Resultado:** A partir de ahora, cualquier cliente que llame a ese número específico será dirigido directamente a la cola `Become a Partner`, escuchando el mensaje de bienvenida personalizado, sin pasar por el menú principal del IVR.

#### Utilidad avanzada
Además de los números de teléfono, existen otros tipos de DAPs que ofrecen una mayor flexibilidad:
- **DAP de Segmento de Usuario (`User Segment`):** Para enrutamiento basado en datos de CRM.
- **DAP de API (`API Response`):** Para enrutamiento basado en información de APIs externas.
- **DAP de Campaña (`Campaign`):** Para enrutamiento de clientes que provienen de campañas de marketing específicas.

Los DAPs no se limitan a los canales de voz (IVR), también se pueden usar en canales web y móviles para enrutar a los clientes basándose en la página o pantalla en la que se encuentran.

---

Call Channel y telephony:
<a href="">referirse a guía</a>

---

### Opciones de Desvío de Llamadas en CCAI Platform 📞

Las opciones de desvío son mecanismos para gestionar el flujo de llamadas de manera eficiente y evitar que los clientes cuelguen por la espera. La plataforma ofrece varias soluciones, cada una con un propósito específico.

#### 1. Desvío por Fuera de Horario (After Hours Deflection)

Este desvío se activa cuando un cliente llama fuera del horario de operación de una cola. Se configuran horarios específicos para cada cola, y las llamadas pueden ser gestionadas de la siguiente manera:
- **Mensaje:** Se reproduce un mensaje predefinido o personalizado informando sobre los horarios de atención, y la llamada finaliza.
- **Redirigir a otra cola:** La llamada se transfiere a una cola interna diferente.
- **Redirigir a un número externo:** La llamada se deriva a un número de teléfono externo, como un servicio de contestación de terceros.
- **Buzón de voz:** La llamada se dirige a un correo de voz para que el cliente deje un mensaje.

#### 2. Desvío por Sobrecapacidad (Overcapacity Deflection)

Este desvío se activa cuando la cola de espera de una cola de agentes está saturada. Incluye todas las opciones del desvío por fuera de horario, más dos adicionales.
- **Devolución de llamada (Callback):** El cliente puede colgar y conservar su lugar en la cola. Un agente le devolverá la llamada cuando esté disponible.
- **Esperar en cola:** El cliente espera en la cola. Se le puede informar periódicamente sobre los tiempos de espera estimados.

#### 3. Desvío a SMS (Pre-session SMS Deflection)

Esta es una estrategia avanzada que permite ofrecer al cliente la opción de transferir la conversación a un canal de SMS.
- **Ventaja:** Los agentes pueden manejar múltiples conversaciones de chat simultáneamente, lo que aumenta la capacidad del centro de contacto para gestionar altos volúmenes de llamadas.
- **Configuración:** Se habilita globalmente en **`Settings` > `Call`** y se personaliza a nivel de cola, seleccionando la cola de SMS que gestionará las interacciones transferidas y las condiciones bajo las cuales se activará la oferta de desvío.

#### 4. Desvío a Agentes Virtuales (Virtual Agents)

Este es el método más efectivo para gestionar la sobrecapacidad. Las llamadas se desvían a agentes virtuales (`Dialogflow`) para que el cliente pueda resolver sus dudas a través del autoservicio.
- **Integración:** La plataforma CCAI se integra con **Dialogflow** para enrutar las llamadas de manera fluida.
- **Beneficio:** Un agente virtual puede desviar más del 50-60% de las llamadas, liberando a los agentes humanos para que se concentren en consultas más complejas. Si el agente virtual no puede resolver la consulta, escala la llamada a una cola de agentes humanos.

---

### Desvíos (Deflections) en Google CCAI Platform

El propósito de los desvíos es mejorar la experiencia del cliente y la eficiencia del centro de contacto, ya que reducen los tiempos de espera y la carga de trabajo de los agentes. En lugar de hacer que un cliente espere indefinidamente, se le ofrecen opciones de ayuda alternativas.

Los tipos de desvíos disponibles varían según la licencia, pero generalmente incluyen:
- `Pre-Session Smart Actions`
- `Overcapacity` (Sobrecapacidad)
- `External Deflection Links`
- `Automatic Redirection`
- `Virtual Agent Deflection and Escalation`
- `After-Hours Deflection`
- `Per Queue/Per Channel Deflections`

A continuación, se detalla la configuración de dos de los desvíos más comunes.

---

### 1. Pre-Session Smart Actions

Esta función ofrece al cliente opciones de autoservicio antes de que se conecte con un agente, como solicitarle que envíe una foto o un video para que el agente tenga más contexto al inicio de la llamada.

#### Habilitación y Configuración

El proceso de configuración tiene dos niveles:

- **Habilitación global:**
    1. Ve a `Settings` > `Operation Management` > `Presession Smart Actions`.
    2. Activa el toggle (`On`).
    3. Define un `Time Limit`, que es el tiempo máximo en segundos que se mostrarán las acciones.
    4. Haz clic en `Save`.

- **Habilitación por cola:**
    1. Ve a `Settings` > `Queue` > `Mobile` (o el canal de tu elección) > `Edit/View`.
    2. Selecciona una cola específica.
    3. Busca la sección `Presession Smart Actions` y activa el toggle.
    4. Puedes configurar un `Time Limit` personalizado para esta cola o usar el global.
    5. `Flow Skip`: Decide si las Smart Actions son opcionales (`Optional`) o si el cliente debe interactuarlas obligatoriamente (`Mandatory`).
    6. `Custom Copy & Feature Enablement`: Personaliza el mensaje y activa acciones específicas como solicitar fotos, videos o texto.

---

### 2. Desvío por Sobrecapacidad (Overcapacity Deflection)

Este desvío se activa cuando la llamada no puede ser atendida por un agente en un tiempo determinado.

#### Configuración Global

- **Ajustes generales:** En `Settings` > `Call` > `Caller Announcements`, configura el intervalo de tiempo en el que se anunciarán los tiempos de espera estimados o los mensajes de desvío.
- **Mensajes:** En `Settings` > `Languages & Messages`, puedes personalizar el mensaje audible que se reproduce en caso de sobrecapacidad.

#### Configuración por Cola (Nivel Específico)

Las opciones de desvío por sobrecapacidad se configuran a nivel de cola. Las colas sin una configuración específica heredarán los ajustes globales del canal `Call`.

1. Ve a `Settings` > `Queue` > `IVR` (o el canal de tu elección) > `Edit/View`.
2. Selecciona una cola específica.
3. Busca `Custom Overcapacity Deflection` y actívalo (`Show`).
4. Selecciona la opción de desvío deseada, que puede variar según el canal:
    - **IVR:** Puedes elegir `Message` para un mensaje simple, o `Queue` para redirigir a otra cola, entre otras opciones.
    - **Web/Mobile:** Las opciones son diferentes ya que la llamada no puede ser redirigida a otra cola.
5. Haz clic en `Save Over Capacity Deflection`.

---

### Enlaces de Desvío Externo y Redirección Automática

Ambas funcionalidades están diseñadas para ofrecer a los clientes alternativas de autoservicio o simplificar el enrutamiento, reduciendo la carga de los agentes y mejorando la eficiencia.

#### 1. Enlaces de Desvío Externo (External Deflection Links)

Estos enlaces ofrecen a los clientes opciones de soporte fuera de la plataforma, como páginas de ayuda, blogs o comunidades. El objetivo es que los clientes encuentren respuestas por sí mismos sin necesidad de hablar con un agente.

**Configuración:**
- **Creación de enlaces:** Los enlaces se configuran globalmente en **`Settings` > `Chat` > `Web & Mobile`**. Se define un **`Identifier`** (nombre interno), un **`Display Name`** (lo que ve el cliente) y una **`Call to Action`** (texto de ayuda). Se pueden crear un número ilimitado de enlaces.
- **Asignación a la cola:** En la configuración de cada cola (`Settings` > `Queue`), puedes asignar los enlaces de desvío externos específicos que deseas mostrar a los clientes.
- **Uso como desvío:** Los enlaces pueden ser el destino de un desvío por **fuera de horario** o por **sobrecapacidad**. Por ejemplo, si los agentes no están disponibles, el cliente puede ser redirigido automáticamente a la página de preguntas frecuentes.

**Experiencia del cliente:**

- **Móvil:** Al hacer clic en el enlace, se abre la aplicación o el sitio web correspondiente. Si el cliente regresa a la sesión en menos de 5 minutos, un mensaje emergente pregunta si su problema ha sido resuelto. Si no, se le muestran las opciones de contacto nuevamente.
- **Web:** El enlace se abre en una nueva pestaña y sigue la misma lógica de mensajes y límite de tiempo.

#### 2. Redirección Automática (Automatic Redirection)

La redirección automática es una función que transfiere a los clientes a un destino predefinido sin que tengan que tomar ninguna acción.

**Comportamiento:**

- Cuando un cliente es transferido a una cola que tiene la redirección automática activa, la llamada o el chat se desvía inmediatamente a la ruta configurada (un mensaje, otra cola, un número externo o un buzón de voz).
- Un desvío por fuera de horario tiene prioridad y puede anular la redirección automática si está activo.
- Solo los agentes que usan el canal **IVR** pueden ver en su interfaz si una llamada está configurada para ser redirigida. Esta visibilidad no está disponible para chat, web o SMS.

**Configuración:**

- La redirección se configura a nivel de cola, en **`Settings` > `Queue`**.
- Se selecciona la cola, se activa la opción **`Automatic Redirection`** y se elige el destino de la redirección.

**Uso común:** Se utiliza frecuentemente para redirigir una sub-cola a una cola en otro idioma o para enviar automáticamente al cliente a un mensaje si la llamada llega fuera del horario de atención.

---
### Desvíos: Enlaces Externos y Redirección Automática

Ambas funcionalidades están diseñadas para ofrecer a los clientes alternativas de autoservicio o simplificar el enrutamiento, lo que reduce la carga de trabajo de los agentes y mejora la eficiencia general del centro de contacto.

#### 1. Enlaces de Desvío Externo (External Deflection Links)

Estos enlaces dirigen a los clientes a recursos externos como **páginas de preguntas frecuentes (FAQs), blogs o comunidades** para que puedan resolver sus problemas por sí mismos, sin necesidad de interactuar con un agente.

##### Configuración

- **Creación:** Los enlaces se configuran en **`Settings` > `Chat` > `Web & Mobile`**. Se definen campos clave como el **`Identifier`** (nombre interno), el **`Display Name`** (lo que ve el cliente) y un **`Call to Action`** (una breve descripción).
- **Asignación a colas:** Una vez creados, los enlaces se asignan a colas específicas en **`Settings` > `Queue`**. Puedes habilitar la opción `External Deflection Links` y seleccionar los enlaces que deseas que estén disponibles para los clientes que contactan a esa cola.
- **Como destino de desvío:** Estos enlaces también pueden ser el destino de desvíos por **fuera de horario** o por **sobrecapacidad** en la configuración de `Web & Mobile Deflection`, lo que permite ofrecer una opción de autoservicio cuando los agentes no están disponibles.

##### Experiencia del Cliente

Cuando un cliente interactúa con estos enlaces en la interfaz web o móvil, es redirigido a la aplicación o sitio web externo. La plataforma cuenta con una lógica inteligente para saber si el cliente resolvió su problema:

- Si el cliente regresa en menos de 5 minutos, aparece un **`popup de resolución`** que pregunta si se resolvió su problema.
- Si la respuesta es "Sí", la sesión se cierra.
- Si es "No", se vuelven a mostrar las opciones de contacto.
- Si el cliente no regresa en 5 minutos, la sesión de contacto se cierra automáticamente.

#### 2. Redirección Automática (Automatic Redirection)

Esta función redirige automáticamente a los clientes a un destino predefinido **sin que tengan que tomar ninguna acción**.

##### Comportamiento

- Cuando una llamada o chat se transfiere a una cola con la redirección automática activa, el sistema la desvía inmediatamente a la ruta configurada (otra cola, un número externo, un mensaje, etc.).
- Es importante notar la **jerarquía**: un desvío por **fuera de horario** tiene prioridad y anulará la redirección automática si ambos están activos.
- La **visibilidad** para los agentes es limitada; solo en el canal **IVR** pueden ver en su interfaz que una llamada transferida será redirigida automáticamente. Esto no aplica para los canales de chat, web o SMS.

##### Configuración

- La redirección se configura a nivel de cola, en **`Settings` > `Queue`**.
- Una vez que se selecciona una cola, se activa la opción `Automatic Redirection` y se elige el destino de la redirección.

##### Usos Comunes

Se utiliza frecuentemente para redirigir sub-colas a colas en otro idioma o para enviar automáticamente a los clientes a un mensaje grabado si llaman fuera del horario de atención.

---

### Resumen General

Tanto los **enlaces de desvío externo** como la **redirección automática** son herramientas para optimizar el flujo de clientes. Los enlaces de desvío priorizan el **autoservicio**, permitiendo que los clientes se ayuden a sí mismos a través de recursos externos. La redirección automática, por otro lado, se enfoca en **automatizar el enrutamiento**, asegurando que el cliente llegue al destino correcto de forma rápida y eficiente, incluso sin intervención del agente.

---

### Mensajería SMS en CCAI Platform

La mensajería SMS es una forma rápida y sencilla de interactuar con los consumidores a través de mensajes de texto. Debido a su accesibilidad y la falta de dependencia de una conexión a internet o de aplicaciones específicas, los SMS suelen tener una tasa de interacción más alta que otros canales.

**Ventajas clave:**
- **Conveniencia:** Los clientes pueden enviar y recibir mensajes rápidamente.
- **Accesibilidad:** Casi todos los usuarios de teléfonos móviles tienen acceso a SMS.
- **Comunicación instantánea:** Permite a las empresas responder consultas y enviar recordatorios en tiempo real.

El servicio de mensajería SMS en CCAI permite:

- Proporcionar una experiencia de chat fluida y en múltiples idiomas.
- Recibir imágenes y videos de los clientes.
- Iniciar conversaciones proactivamente con SMS salientes.
- Enrutar clientes a los agentes correctos con colas flexibles.
- Transferir chats entre agentes.
- Usar múltiples números de soporte para diferentes líneas de negocio.

**Nota:** Para usar las funciones de SMS, es necesario adquirir números SMS específicos.

---

### Tipos de Mensajería SMS en CCAI

La plataforma ofrece varias opciones para la mensajería SMS, cada una adaptada a un caso de uso distinto.

#### 1. Canal SMS (Inbound/Outbound)

Este es el servicio de mensajería de texto estándar. Los consumidores pueden iniciar chats SMS entrantes y los agentes también pueden iniciar chats salientes.

- **Configuración:** Durante la configuración del canal SMS, el equipo de implementación debe asegurarse de que la configuración de chat esté activada antes de añadir los números a las colas. Para permitir que los agentes inicien chats salientes, la cola debe tener un número SMS de salida adjunto y habilitado.
- **Gestión de Agentes:** Los agentes pueden manejar múltiples interacciones SMS simultáneamente, según su nivel de concurrencia de chat.

#### 2. SMS Híbrido o de Tiempo de Espera (`Blended/Wait Time SMS`)

Este servicio permite a los clientes enviar mensajes de texto, fotos, o videos mientras esperan en la cola de llamadas del IVR o durante la conversación telefónica con el agente.

- **Requisitos:** A diferencia del canal SMS, este servicio **requiere una llamada IVR activa**. También se necesita un número de SMS específico para esta función, diferente del número de la cola SMS estándar.
- **Beneficios:** Permite a los clientes enviar información importante (ej. una foto de un producto dañado) de manera proactiva, lo que reduce el tiempo de resolución promedio (`AHT`).

#### 3. Redirección SMS Pre-Sesión (`Pre-Session SMS Redirection`)

Esta función permite ofrecer soporte por chat SMS como una opción alternativa para los clientes que están llamando por IVR, incluso antes de que la llamada se conecte a un agente.

- **Funcionamiento:**
    1. Se configura a nivel de cola del IVR.
    2. Puede activarse bajo ciertas condiciones, como un tiempo de espera estimado elevado.
    3. Los clientes que eligen esta opción reciben un SMS para continuar la sesión por ese canal. La llamada de voz se termina automáticamente al confirmar.
- **Ventaja:** Permite desviar el volumen de llamadas a un canal donde los agentes pueden manejar múltiples sesiones al mismo tiempo, reduciendo los tiempos de espera y de resolución.

#### 4. SMS sin Sesión (`Sessionless SMS`)

Esta es una funcionalidad avanzada que permite el envío de mensajes SMS salientes sin que se abra una sesión de soporte o un ticket de CRM.

- **Propósito:** Es ideal para enviar mensajes puntuales y automatizados.
- **Casos de uso comunes:** Envío de contraseñas de un solo uso, códigos de verificación, recordatorios de citas o enlaces para encuestas de satisfacción.
- **Consideraciones:** No está diseñado para el envío masivo de mensajes.
#### 5. SMS Saliente (`Outbound SMS`)

A diferencia del SMS sin sesión, la API de SMS saliente permite enviar mensajes que, si son respondidos por el cliente, **abren una sesión de soporte**.
- **Propósito:** Es ideal para la comunicación basada en eventos que requiere la posibilidad de una respuesta del cliente.
- **Casos de uso:** Notificar a un cliente que su pedido está listo para recoger y permitirle responder para iniciar una conversación con un agente.

---

# 🤫

1. Mejor opción para agregar multi lenguaje:
	Crear una queue en el idioma base (usualmente inglés) y de ahí agregar otros idiomas como sub queues
2. Para iniciar conversaciones SMS con agentes:
	Se necesita enviar un SMS al teléfono dispuesto a ello
3. Qué es lo mínimo requerido para portear números a CCAI-P:
	Letter of Agency (LOA) firmado, listado de los números a portar, fecha del porte, copia de la cuenta para los números del proveedor
4. Los DAPS tienen un órden de operaciones específicos por defecto
5. Usando el SDK móvil o la web, los agentes pueden usar un deflection link para enviar a los clientes a enlaces externos (usualmente FAQ)
6. Para iniciar SMS de salida, el agente necesita que que el número esté en el panel CRM
7. Los números siempre serán del cliente.

