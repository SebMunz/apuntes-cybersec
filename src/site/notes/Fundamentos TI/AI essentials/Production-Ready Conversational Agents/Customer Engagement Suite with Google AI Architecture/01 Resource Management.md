---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Customer Engagement Suite with Google AI Architecture/01 Resource Management/"}
---

# Índice

[[#CES y sus componentes principales]]
[[#Entorno operacional]]
[[#Control de Acceso]]
[[#GCP y 3rd Party]]
[[#Ecosistema Vertex]]
[[#Historia y opciones de integración]]

---

# CES y sus componentes principales

**Customer Engagement Suite (CES)** con **Google AI Architecture** es una solución diseñada para transformar y optimizar los centros de contacto. Antes de implementarla, es crucial hacerse algunas preguntas básicas:

- **¿Qué soluciones necesitas?**
    
    - **CCaaS (Contact Center as a Service):** Si buscas una solución integral para modernizar tu centro de contacto.
        
    - **Customer Engagement Suite (CES):** Si solo necesitas implementar soluciones específicas como:
        
        - **Agentes conversacionales:** Para escalar la auto-asistencia y mejorar la satisfacción del cliente.
            
        - **Agent Assist:** Para proporcionar asistencia a agentes humanos y mejorar su eficiencia.
            
        - **Conversational Insights:** Para realizar análisis profundos de las interacciones y obtener KPIs de clientes y agentes.
            

### **Consideraciones arquitectónicas y de recursos**

Al planificar una solución CES, es importante considerar varios factores para una implementación exitosa:

1. **Interconexión de tecnologías:** La forma en que los componentes de CES se comunican y comparten datos es crucial para una operación eficiente.
    
2. **Recursos operacionales:** Debes definir los recursos necesarios para soportar tus entornos operacionales.
    
3. **Captura de datos:** Es esencial definir cómo se capturarán los datos de la solución CES para medir el éxito operacional y los KPIs.
    

### **Solución integral de CES**

Una solución CES completa puede combinar varias tecnologías:

- **Telefonía:** La base de la comunicación.
    
- **Agentes conversacionales:** Manejan las interacciones iniciales o de rutina.
    
- **Tecnologías de asistencia al agente humano:** Ayudan a los agentes en sus interacciones.
    
- **Conversational Insights:** Se utiliza para analizar los datos generados por todas estas tecnologías, interactuar con las APIs y la capa de datos, y conectarse con otros servicios para personalizar la solución.
    

Las necesidades de la empresa son el principal motor de decisión para determinar qué soluciones de CES implementar.

---

# Entorno operacional

### **Gestión de recursos y proyectos**

- **Proyectos de Google Cloud:** Se recomienda crear al menos dos proyectos para mantener una separación clara: uno para entornos de **no producción** (desarrollo y pruebas) y otro para **producción** (staging y producción). Algunos usuarios prefieren tener tres proyectos separados para cada entorno.
    
- **Agentes conversacionales (`Conversational Agents`):** Generalmente, solo necesitas un agente para los entornos de no producción y otro para los de producción.
    
    - Si diferentes equipos gestionan agentes para distintos tipos de usuarios o líneas de negocio, es aconsejable colocarlos en proyectos separados para gestionar el control de acceso de forma independiente.
        
- **Término "agente":** Cuando se usa en el contexto de recursos, "agente" se refiere a un `Conversational Agent`, no a un agente humano.
    

---

### **Conectividad: pública vs. privada**

La decisión sobre la conectividad depende de los requisitos de seguridad y de la infraestructura.

- **Conectividad pública:**
    
    - No requiere infraestructura adicional.
        
    - Los clientes se conectan a un _endpoint_ público de la API de `Conversational Agents`.
        
    - La comunicación está encriptada con **TLS** y utiliza credenciales **OAuth** y una cuenta de servicio para autenticación.
        
    - Es la opción más rápida y no sacrifica la seguridad.
        
- **Conectividad privada:**
    
    - Requiere una **interconexión privada** a una **VPC de Google Cloud**.
        
    - Es más compleja, ya que necesita configurar `Private Service Connect` y un servidor **DNS** interno.
        
    - Usada por industrias o ubicaciones con requisitos estrictos de privacidad o que necesitan un mayor ancho de banda de red.
        

### **Ruta del flujo de conversación**

La forma en que las conversaciones se enrutan a **CES** depende de la solución que implementes:

- **Con `Agent Assist`:**
    
    - **Si usas `CCaaS` en Google Cloud:** El sistema gestionará automáticamente el envío de las conversaciones a los agentes conversacionales y mostrará la información relevante al agente humano.
        
    - **Si usas un enfoque híbrido (`on-premises`):** Debes asegurar que exista una integración para enviar los datos a **CES**.
        
- **Sin `Agent Assist`:** El flujo de audio debe ser enviado directamente al agente conversacional. Hay dos maneras de hacerlo:
    
    1. **Solicitudes `gRPC`:** Usando APIs de `Conversational Agents` como `Analyze Content` o `Streaming Detect Intent`.
        
    2. **`SIP Endpoint`:** Usando el _endpoint_ SIP proporcionado por la **Plataforma de Telefonía de Google (GTP)**.

---

# Control de Acceso

### **IAM y roles**

- **IAM (`Identity and Access Management`):** Es el marco de políticas y tecnologías que te permite definir quién tiene permisos para realizar acciones sobre los recursos de Google Cloud.
    
- **Roles:** Son conjuntos de permisos que se agrupan y se asignan a usuarios o cuentas de servicio. Google Cloud ofrece roles predefinidos, pero también puedes crear roles personalizados para permisos más granulares.
    

### **Roles recomendados para equipos de CES**

Para implementar una solución CES, se recomienda asignar roles específicos a los diferentes equipos:

- **Equipo de Operaciones de Desarrollo (`Developer Operations`):**
    
    - Gestiona las configuraciones principales de los agentes. Se les puede asignar un rol personalizado para esta tarea.
        
- **Desarrolladores de Agentes Conversacionales (`Conversational Agents Developers`):**
    
    - Necesitan permisos para editar flujos (`flows`).
        
- **Desarrolladores de webhooks (`Webhook Devs`):**
    
    - Requieren el rol de **`Cloud Run Administrator`** para administrar los servicios de `Cloud Run` donde se alojan los webhooks.
        
    - También necesitan el rol de **`Dialogflow Webhook Admins`** para configurar los webhooks del agente.
        
    - _Nota:_ Los roles todavía se denominan **Dialogflow** a pesar de que el producto se llama **Conversational Agents**.
        
- **Desarrolladores de `Agent Assist`:**
    
    - Necesitan el rol de **`Dialogflow Admin`** y el rol de **`PubSub Admin`** (debido al papel crucial de PubSub en `Agent Assist`).
        
- **Analistas de datos de `Conversational Insights`:**
    
    - Suelen recibir el rol de **`BigQuery Admin`** y el de **`Contact Center Insights Editor`**.
        
- **Personal que despliega servicios CES:**
    
    - Se les debe asignar el rol de **`Contact Center AI Platform Admin`**.

---

# GCP y 3rd Party

### **Servicios de Google Cloud que complementan CES**

Estos servicios son clave para la observabilidad, el análisis de datos, la seguridad y la conectividad:

- **Observabilidad (`Cloud Observability`):**
    
    - **`Cloud Logging`:** Permite capturar información de logs de tus recursos para monitorear las interacciones de tus agentes conversacionales.
        
    - **`Cloud Monitoring`:** Recopila y observa métricas, eventos y metadatos importantes (como tasas de error y latencia) para evaluar el rendimiento de CES.
        
- **Análisis de Datos:**
    
    - **`BigQuery`:** Ideal para crear _data warehouses_ cuando necesitas registrar e analizar interacciones de CES. Permite adaptar, mantener y evolucionar tu solución.
        
    - **`Looker Studio`:** Facilita la visualización de datos de BigQuery, permitiendo crear reportes y monitorear el rendimiento de CES.
        
- **Seguridad de Datos:**
    
    - **`Cloud Data Loss Prevention (Cloud DLP)`:** Protege la información de identificación personal (PII) al identificarla y luego enmascararla, reemplazarla o eliminarla. Es crucial para identificar y proteger parámetros recolectados por agentes conversacionales que podrían ser PII.
        
- **Conectividad y Ejecución de Código:**
    
    - **`Webhooks`:** Permiten a los agentes conversacionales conectarse a sistemas externos para buscar información o realizar transacciones.
        
    - **`Cloud Functions` y `Cloud Run`:** Opciones populares y elásticas para implementar código de webhook, facilitando la creación de microservicios que escalan rápidamente. Otras opciones incluyen `Kubernetes Engine`, `Compute Engine`, `App Engine` o `Apigee`.
        

---

### **Integraciones con proveedores de terceros**

CES facilita la integración con:

- **Proveedores de telefonía y chat:** Estas integraciones son esenciales para el éxito de cualquier implementación de CES.
    
- **Integraciones "one-click":** `Conversational Agents` ofrece integraciones directas con muchos proveedores populares.
    
- **Conexiones personalizadas:** Si no existe una integración directa, se pueden desarrollar conexiones personalizadas a través de las APIs de CES.

---

# Ecosistema Vertex

### **Integración con Google Cloud**

Las soluciones de **CES** no funcionan de forma aislada. Se complementan con otros servicios de Google Cloud para potenciar sus capacidades. Los servicios más comunes que se integran con CES son:

- **Cloud Logging & Cloud Monitoring:** Para monitorear el rendimiento, los eventos y las métricas de tu solución CES, incluyendo tasas de error y latencia.
    
- **BigQuery & Looker Studio:** Para almacenar y analizar grandes volúmenes de datos de interacción en un _data warehouse_. **Looker Studio** se utiliza para crear informes y visualizar los datos de **BigQuery**.
    
- **Sensitive Data Protection (Cloud DLP):** Para identificar y proteger información de identificación personal (PII) en tus datos, permitiendo enmascarar, reemplazar o eliminar información sensible.
    
- **Cloud Functions & Cloud Run:** Opciones populares para el desarrollo de microservicios, como _webhooks_, que conectan a los agentes conversacionales con otros sistemas para buscar información o realizar transacciones.
    

### **CES dentro del ecosistema de Vertex AI**

**Vertex AI** es la plataforma de _machine learning_ de Google Cloud. **CES** se sitúa en la parte superior de su ecosistema, aprovechando toda la tecnología subyacente. El _stack_ de Vertex AI se compone de varias capas:

1. **Infraestructura optimizada para IA:** La base del _stack_ con GPU y TPU.
    
2. **`Vertex AI Model Garden`:** Un catálogo de modelos de lenguaje grandes (LLMs) propios, de código abierto y de terceros.
    
3. **`AI Platform`:** Las herramientas para construir, desplegar y monitorear modelos de IA generativa (`Gen AI`) y flujos de trabajo.
    
4. **`Vertex AI Search and Conversation`:** La interfaz que permite a los desarrolladores infundir rápidamente capacidades de `Gen AI` y búsqueda en sus aplicaciones.
    
5. **Soluciones de IA:** Aquí es donde se ubican soluciones preempaquetadas como **`Contact Center as a Service`** y **CES**. Estas soluciones utilizan `Vertex AI Search and Conversation` para desplegar _chatbots_ y _voicebots_ a escala.
    

---

### **Enfoques de implementación**

La forma de implementar una solución de CES depende del nivel de experiencia técnica y las necesidades de personalización.

- **"Construye tu propia solución":** Para clientes con alta competencia en IA, que buscan casos de uso altamente personalizados. Estos pueden usar componentes individuales de Vertex AI como `Model Garden`, `AI Platform` y `AI Applications` para ensamblar su propia solución.
    
- **Productos "listos para usar":** Para clientes que buscan productos de bajo o nulo código. Pueden usar soluciones preempaquetadas como **CES**, **Agentes Conversacionales**, **Agent Assist** o **Conversational Insights**.
    
- **`Prebuilts` (soluciones predefinidas):** Plantillas para casos de uso específicos de verticales como servicios financieros o pedidos de comida, que solo requieren un ajuste fino.

---

# Historia y opciones de integración

- **Integraciones con ISVs (2019 en adelante):** Inicialmente, Google Cloud se asoció con los principales proveedores de software independientes (como Genesys, NICE, Avaya, Cisco, Five9, etc.) para que los clientes pudieran agregar capacidades de IA conversacional a su infraestructura de centro de contacto existente. Esta opción prolongó la vida útil de las soluciones tradicionales.
    
- **CCaaS (`Contact Center as a Service`):** A raíz de la demanda por una solución de extremo a extremo, surgió **CCaaS**, la propia oferta de Google Cloud para un centro de contacto moderno y potenciado por IA. **CES** forma parte de esta solución.
    

### **Modelos de adopción de CES**

La elección del modelo de implementación depende de las necesidades y la infraestructura existente del cliente. Tienes tres opciones principales:

1. **Adopción de una nueva infraestructura:** Puedes optar por **CCaaS** como una solución completa de Google Cloud, que incluye **CES**. Este modelo es ideal para una configuración optimizada y resultados rápidos.
    
2. **`CES over the top`:** Si deseas mantener tu plataforma actual de centro de contacto, puedes agregar las capacidades de IA de **CES** a tu solución existente. Esta opción es flexible y te permite migrar a una plataforma completa en el futuro si lo deseas.
    
3. **Integración con socios OEM:** Si quieres retener tu infraestructura existente, puedes aprovechar las integraciones de **CES** con socios originales (`OEM partners`).

---

