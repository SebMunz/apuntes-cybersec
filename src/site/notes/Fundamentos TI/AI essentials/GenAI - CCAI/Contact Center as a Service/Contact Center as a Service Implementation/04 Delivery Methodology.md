---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Contact Center as a Service/Contact Center as a Service Implementation/04 Delivery Methodology/"}
---

# Índice

- [[#Delivery Methodology – Initiate Phase]]
- [[#Recopilación de Requisitos y Diseño de la Solución]]
- [[#Fase de Construcción y Configuración]]
- [[#Fase de Ejecución]]
- [[#Cierre del Proyecto y Transición al Soporte]]

---

# Delivery Methodology – Initiate Phase

### Preparación y Lanzamiento de un Proyecto de Implementación

El objetivo de esta fase inicial es establecer una base sólida para el proyecto, asegurando que todas las partes estén alineadas en los objetivos, el alcance y los próximos pasos. Esto minimiza los riesgos y garantiza una ejecución fluida.

---

### 1. Llamada de Transición Interna con el Equipo de Ventas

Antes de hablar con el cliente, es crucial tener una sesión interna para entender el contexto completo del proyecto.

- **Contactos y Alcance:** Identifica a los **contactos clave** del cliente y revisa a fondo el **`Statement of Work` (SOW)** para discutir las actividades **`IN-Scope`** y **`OUT-of-Scope`**. Esto te ayudará a identificar posibles riesgos o desviaciones y a alinear las expectativas.
- **Criterios de Éxito:** Revisa los **criterios de éxito** definidos en el SOW para entender qué define el éxito del proyecto desde la perspectiva del cliente.
- **Pasos Previos:** Coordina con el equipo de ventas para que le notifiquen al cliente quiénes deben asistir a la reunión de lanzamiento (`kick-off`) y para que realicen las **configuraciones previas** necesarias, como la creación de un `tenant` o `sandbox` en CCAI Platform.

---

### 2. Reunión de Lanzamiento (`Kick-off`) con el Cliente

Esta es la primera interacción formal con el cliente. El objetivo es presentar al equipo y alinear los detalles del proyecto.

**Prepara la reunión:**
- **Actualiza el material de presentación** (`Kick-off Deck`) con la información más reciente del proyecto.

**Agenda de la llamada:**

- **Presentaciones y Contactos:** Presenta a los equipos, identifica los roles y define los contactos clave del proyecto.
- **Revisión del SOW:** Revisa los detalles operativos del SOW, incluyendo el número de agentes, su ubicación, y la estrategia para los **números de teléfono** (portabilidad o `Bring Your Own Carrier` - BYOC).
- **Canales:** Confirma qué canales se configurarán (voz, chat, etc.), si se necesita **talento de locución** y qué **solución de CRM** se integrará (ej., Salesforce).
- **Metodología y Hitos:** Comunica las **fechas de lanzamiento** (`go-live`), la **frecuencia de las reuniones** de seguimiento (`cadence calls`) y el **repositorio compartido** para la documentación del proyecto.
- **Próximos Pasos:** Define las tareas inmediatas, como obtener los detalles de configuración de la red y gestionar la portabilidad de los números de teléfono.

---

### 3. Seguimiento y Descubrimiento (`Discovery`)

Después de la reunión de lanzamiento, el enfoque cambia a recopilar los requisitos detallados del proyecto.

- **Comunicación:** Envía un **correo de seguimiento** con un resumen de los acuerdos y la información que necesitas para los siguientes pasos.
- **Sesiones de Descubrimiento:** Programa sesiones dedicadas para recopilar información clave sobre:
    - **Arquitectura:** Comprender la arquitectura tecnológica actual del cliente.
    - **Requisitos:** Capturar los requisitos funcionales, de seguridad, de red y de integración del proyecto.
    - **Reglas de Negocio:** Entender las reglas que guiarán el flujo de las conversaciones.
    - **`Reporting` y `Analytics`:** Definir los requisitos de reportes y análisis.
    - **Infraestructura:** Recopilar información sobre el _software_, _hardware_ y la **configuración de red** del centro de contacto, especialmente para agentes en **teletrabajo** (`Work From Home`).

El objetivo final de esta fase es documentar todos los hallazgos y compartirlos con el cliente, sentando las bases para el diseño y la configuración del proyecto.

---

# Recopilación de Requisitos y Diseño de la Solución 

El objetivo de esta fase es recopilar los requisitos detallados del cliente para diseñar la configuración técnica de CCAI Platform. Esto se logra a través de sesiones de diseño de la solución, que permiten entender los flujos actuales y las mejoras deseadas.

---

### 1. Sesiones de Diseño de la Solución

Antes de las reuniones, el cliente debe prepararse para optimizar el tiempo.

**Pre-work para el cliente:**

- **Diagramas de Flujo:** Deben proporcionar un diagrama de su flujo de llamadas actual y su arquitectura de integraciones.
- **Mejoras Deseadas:** Identificar las 3 a 5 mejoras principales que buscan lograr con la implementación de CCAI Platform.
- **Estructura de Agentes:** Detallar la organización de los agentes, incluyendo ubicaciones, equipos y estructura de liderazgo.
- **Inventario de Números:** Proporcionar una lista de todos los números de teléfono actuales y su uso.
- **Web y Mobile SDKs:** Indicar las páginas web y aplicaciones móviles donde desean implementar el servicio.
- **Integraciones:** Listar las integraciones con terceros que utilizan actualmente, como su CRM.
- **Métricas:** Compartir los indicadores clave de rendimiento (`KPIs`) que esperan mejorar.

**Durante las reuniones:**

- Utiliza una **hoja de trabajo de proyecto** para guiar la conversación y asegurarte de cubrir todas las preguntas de la fase de descubrimiento.
- **Áreas de Configuración:** Cubre todas las áreas de la plataforma, desde la configuración global (ej., `Languages & Messages`, `Developer Settings`) hasta la configuración de canales específicos (`Calls`, `Chats`, `Email`).
- **Diseño de Flujo:** Analiza el diseño actual del cliente y rediseña el flujo para todos los canales en alcance. Identifica dónde se usarán números de teléfono y **puntos de acceso directo** (`DAPs`).

---

### 2. Entregables y Mejores Prácticas

El principal resultado de esta fase es un borrador del **Documento de Diseño Técnico**.

**Mejores Prácticas:**

- **Simplifica:** Pregunta si es posible **consolidar colas** si el cliente tiene demasiadas. Es importante entender el valor que aporta cada una.
- **Optimiza la Experiencia:** Esta fase es una gran oportunidad para **rediseñar la experiencia de la voz** en el IVR, mejorando la redacción o cambiando el talento de voz.
- **Desvío de llamadas:** Pregunta por las 3 razones principales por las que los clientes se contactan para ver si se pueden manejar mejor con una estrategia de **desvío** (`deflection`).

---

### 3. Configuraciones Comunes y Alternativas

La plataforma tiene configuraciones que a veces requieren soluciones alternativas (`workarounds`).

- **Agentes por Niveles (`Tier/Cascade`):** Para emular grupos en cascada, ajusta la **configuración del temporizador de cascada** para que sea más agresiva y la llamada se transfiera más rápidamente.
- **Enrutamiento por Número Marcado (`DNIS`):** Dado que CCAI-P no enruta solo por el `DNIS`, la solución es crear **estructuras de colas separadas** y usar un **DAP** en la parte superior de cada una.
- **Sobrecapacidad por Horario:** No hay una configuración variable por hora para la sobrecapacidad. La alternativa es crear un **menú específico para la sobrecapacidad** con sus propios horarios de operación.
- **Estado del Agente:** Los agentes **no pueden autogestionar** su disponibilidad. Los administradores deben moverlos manualmente entre las asignaciones de colas.

---

# Fase de Construcción y Configuración

El objetivo principal de esta fase es convertir el diseño acordado en un entorno funcional y probado en la plataforma de CCAI. Se trata de implementar todas las configuraciones y las integraciones clave en el `tenant` del cliente.

#### Pasos del Proceso

1. **Configurar el Entorno:**
    - Basándote en la **hoja de trabajo del proyecto** (`project worksheet`) que se llenó en la fase de descubrimiento, empieza por configurar los ajustes globales (`Global Settings`), como el Centro de Soporte, idiomas, y la gestión de operaciones.
    - Después, **crea las colas** (`queues`) y los horarios de operación (`Hours of Operation`), incluyendo horarios generales y personalizados.
2. **Gestionar Mensajes y Grabaciones:**
    - Utiliza la sección **"Greetings & Media Recordings"** de la hoja de trabajo para planificar todos los audios y mensajes necesarios.
    - Define si las grabaciones las realizará un talento de voz profesional, una persona interna del cliente o si se utilizará un motor de texto a voz (`TTS`).
    - Sube los audios finales a la plataforma en **`Languages and messages`** y configura los mensajes de sobrecapacidad (`overcapacity`) y las opciones de _callback_.
    - En la configuración de cada cola (`Queue settings`), asigna los mensajes de opciones de cola, los saludos de los Puntos de Acceso Directo (`DAPs`) y los mensajes de desvío personalizados (`custom deflection`).

3. **Realizar Pruebas Internas:**
    - Antes de presentarle la solución al cliente, haz pruebas rigurosas.
    - **Llama a las colas** para verificar que el enrutamiento (`call flow`) funcione como se diseñó.
    - Confirma que los horarios de operación, los mensajes de desvío y los anuncios se reproduzcan correctamente.
    - Identifica y corrige cualquier error.
4. **Integrar el CRM y Otros Sistemas:**
    - Coordine con el cliente para agendar una sesión con su **administrador de CRM** y configuren juntos la integración. Para esto, es importante seguir la documentación específica de integración.
    - Otras integraciones, como el almacenamiento externo para grabaciones (`Google Cloud Storage`), también deben completarse en esta fase.
    - Las interaciones de **Gestión de la Fuerza Laboral** (`WFM`) o **Gestión de Calidad** (`QM`) suelen implementarse como un paso posterior al lanzamiento.
5. **Revisión de la Configuración con el Cliente:**
    - Agende una llamada con el cliente para **revisar la configuración final**.
    - Explica cómo se implementaron los ajustes y realiza una **llamada de prueba demostrativa** para que vean el flujo en acción.

---

### Mejores Prácticas

- **Autonomía del Cliente:** Siempre que sea posible, guía a los clientes para que utilicen la documentación del Centro de Soporte. Esto los capacita para que puedan realizar ajustes menores por su cuenta después de la configuración inicial, fomentando la autonomía y reduciendo la dependencia.

---

# Fase de Ejecución

El objetivo de esta fase es preparar a los usuarios, realizar las pruebas finales y ejecutar un lanzamiento controlado de la plataforma.

---

### 1. Importación de Usuarios y Equipos

Antes de agregar a los agentes, es importante avisarles que recibirán un **correo de bienvenida** de la plataforma.

- **Método de carga:** Puedes crear los usuarios **manualmente** o mediante **importación masiva** con un archivo CSV, dependiendo del volumen.
- **Involucra al cliente:** Esta es una excelente oportunidad para que el **administrador del cliente** realice parte del trabajo, sirviendo como un entrenamiento práctico.
- **Asignación de equipos:** Aunque los equipos ya deben estar creados y asignados a las colas, en este paso debes agregar a los **agentes individuales** a sus equipos correspondientes.

### 2. Capacitación de Usuarios

La formación es clave para el éxito del proyecto.

- **Aprendizaje práctico:** El administrador del cliente puede aprender por **observación** al equipo de implementación durante la configuración.
- **Cursos principales:** Los usuarios deben completar los cursos en **Google Cloud Skills Boost** para sus roles (administrador, gerente, agente).
- **Sesiones complementarias:** Como _partner_, puedes ofrecer sesiones en vivo adicionales para reforzar el aprendizaje.

### 3. Pruebas de Aceptación de Usuario (UAT)

La UAT es el proceso para obtener la **aprobación formal** del cliente antes del lanzamiento.

- **Requisitos:** Asegúrate de que la configuración, la integración con el CRM y la creación de usuarios estén completas antes de iniciar la prueba.
- **Proceso de prueba:**
    1. Verifica que todas las configuraciones coincidan con el documento del proyecto.
    2. Haz pruebas de llamadas internas antes de la sesión con el cliente.
    3. Prepara una **hoja de UAT personalizada** con casos de prueba específicos.
    4. Confirma que la **configuración de red** esté lista en todas las ubicaciones.
    5. Asegura que los agentes tengan acceso, estén asignados a las colas y capacitados.
    6. Realiza una sesión de 60 minutos con el cliente para ejecutar las pruebas.
    7. **Anota los IDs de llamadas** de cualquier problema para reportarlo al equipo de soporte.

### 4. Preparación y Lanzamiento

Esta es la fase culminante del proyecto.
- **Validación final:** Confirma que la configuración, las pruebas de UAT, la capacitación de usuarios y la configuración de la red están completas.
- **Estrategia de números:** Si usarán el **desvío de llamadas** en lugar de la portabilidad, designa a alguien del cliente para que active el desvío hacia el número temporal de CCAI-P.
- **Registro de riesgos:** Crea un **registro RAID** (Riesgos, Supuestos, Problemas y Dependencias) para dar seguimiento a todo durante el lanzamiento.
- **Llamada de lanzamiento:** Programa una conferencia para el momento del lanzamiento y notifica al equipo de soporte con los detalles clave.
- **Ejecución:** La persona designada activa el desvío de los números. El equipo de implementación se queda en la llamada durante la primera hora para monitorear el lanzamiento.

---

### Preguntas Clave para la Preparación

- **¿Cómo preparar a los agentes?**
    - Diles que anoten el **`Call ID`** de su adaptador para reportar problemas y confirma que completaron el entrenamiento en Skills Boost.
- **¿Desvío o portabilidad?**
    - El **desvío de llamadas** es la mejor opción, ya que permite un plan de reversión rápido si algo sale mal.
- **¿Quién debe estar en la llamada de lanzamiento?**
    - Los **actores principales** del proyecto, no necesariamente todos los involucrados.
- **¿Lanzamiento completo o escalonado?**
    - Depende de la preferencia del cliente, pero un lanzamiento completo puede ser caótico. Necesitas un **único punto de contacto** durante el lanzamiento para coordinar.
- **¿Señales para revertir?**
    - Si las llamadas no llegan a los agentes, si los agentes no pueden iniciar sesión o hacer llamadas, si la calidad es muy mala, o si los desvíos son incorrectos.
- **¿Quién debe estar disponible (`on standby`)?**
    - El administrador de red y telecom, el administrador del CRM, los supervisores y, si es necesario, los desarrolladores web o móviles.
- **¿Cómo medir el éxito?**
    - Monitorea los **paneles en tiempo real** de CCAI-P y la actividad en el CRM para ver las llamadas entrantes y el estado de los agentes.
- **¿Se monitorea la calidad de las llamadas?**
    - No se monitorea activamente; solo se investigan los problemas **si los agentes los reportan**

---

# Cierre del Proyecto y Transición al Soporte

El objetivo de esta fase es asegurar un **cierre ordenado del proyecto**, garantizando una transición suave hacia el equipo de soporte y la gestión continua. Esto incluye resolver los últimos problemas, formalizar la transición del cliente y finalizar la documentación interna.

---

### 1. Transición al Soporte

Para garantizar que el cliente se sienta respaldado después del lanzamiento, la transición se realiza de forma gradual.
- **Soporte post-lanzamiento:** Para dar tranquilidad al cliente, mantén las llamadas de seguimiento (`cadence calls`) durante 1-2 semanas después del `go-live`. Durante este tiempo, el **registro RAID** debe actualizarse con cualquier problema nuevo o su resolución. Es crucial resolver todos los problemas mayores pendientes y obtener la aprobación del cliente sobre el estado de cada uno.
- **Llamada de transición:** Programa una llamada final donde se incluya al **equipo de soporte** y al **`Customer Success Manager` (CSM)** del cliente. Esta es la última llamada oficial con el equipo de implementación. El objetivo es que el cliente se sienta seguro y apoyado en su transición al soporte continuo.

---

### 2. Cierre Interno

El cierre interno asegura que todo el trabajo administrativo del proyecto se complete y se documente correctamente.
- **Actualizar la documentación:** Revisa y completa todas las notas de las reuniones y actas del proyecto.
- **Revisar la _checklist_:** Asegúrate de que todos los pasos del `checklist` de gestión del proyecto estén terminados.
- **Cierre de temas pendientes:** Completa o delega formalmente cualquier punto de acción (`action item`) que haya quedado abierto.

### Conclusión

Esta fase evita un final abrupto del proyecto, permitiendo un **aterrizaje suave** hacia la operación diaria. Se enfoca en la estabilidad posterior al lanzamiento y el cierre administrativo interno, dejando al cliente con un canal de soporte claro y toda la documentación en orden.

---

