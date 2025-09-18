---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Customer Engagement Suite with Google AI Architecture/03 Deployment and Operations/"}
---

# Índice
[[#Arquitectura]]
[[#Automatización de infraestructura CES]]
[[#Extracción de Data Insights]]
[[#Disaster Recovery]]

---

# Arquitectura

### **DevOps y gestión de lanzamientos**

Para establecer una gestión de lanzamientos sólida, es necesario responder a dos preguntas:

1. **¿Cómo gestionarás tus entornos?** Es crucial usar distintos entornos para desarrollo, pruebas y lanzamiento (`draft`, `unit testing`, `ready to merge`, etc.).
    
2. **¿Qué interfaz se usará para el monitoreo?** Se necesita una interfaz para diferenciar entre operaciones normales y anómalas, y para medir el rendimiento.
    

---

### **Flujo de trabajo de desarrollo**

El uso de entornos separados y un flujo de trabajo claro permite que múltiples desarrollos se realicen de manera independiente y en paralelo.

1. **Entornos separados:** Diferentes entornos como `draft`, `unit testing` y `ready to merge` permiten a los equipos trabajar en distintas funcionalidades al mismo tiempo.
    
2. **Detección temprana de errores:** La supervisión de cada fase ayuda a identificar y corregir problemas de forma temprana.
    
3. **Artefacto dorado (`Golden Artifact`):** El objetivo es producir un candidato para el lanzamiento a producción que esté completamente probado y validado.
    

### **Consideraciones para el lanzamiento a producción**

Una vez que tienes el "artefacto dorado", hay dos puntos importantes para el lanzamiento:

1. **Despliegue gradual:** Si es posible, implementa la nueva versión de forma gradual, por ejemplo, comenzando con el 1% del tráfico y aumentando progresivamente hasta el 100%.
    
2. **Automatización:** El entorno de producción debe estar completamente automatizado. La intervención manual (`break-glass intervention`) solo debe ocurrir en situaciones de emergencia.
---
# Automatización de infraestructura CES

Existen tres herramientas principales para automatizar las operaciones y el mantenimiento de **Agentes Conversacionales**: la **API nativa**, las **librerías cliente** y la API de _scripting_ de Python **SCRAPI**.

---

### **1. La API de Agentes Conversacionales**

La API de **Agentes Conversacionales** es una herramienta robusta y completa para automatizar y reconfigurar despliegues. Sin embargo, tiene algunas características que pueden suponer un reto para quienes no estén familiarizados con ella:

- Está diseñada en torno a **llamadas a procedimiento remoto (RPC)** en lugar de un diseño **RESTful**, lo cual puede resultar complejo.
    
- Cada **versión de la API** (`Version 2`, `Version 3`) coexiste y tiene su propio ciclo de vida (`Alpha`, `Beta`, `Generally Available`). Una versión no reemplaza a la anterior; simplemente se adaptan a diferentes tipos de trabajo.
    
- Con el tiempo, las APIs más antiguas pueden quedar **obsoletas** y sus funciones se integran en APIs más recientes.
    

### **2. Librerías cliente**

Las librerías cliente funcionan de forma similar a las APIs nativas, permitiendo acceder a ellas desde lenguajes de programación populares. También puedes usar tus propias librerías personalizadas para llamar al servicio de la API.

---

### **3. SCRAPI**

**SCRAPI** (`Conversational Agents SCRipting API`) es una **API de Python de alto nivel** y de código abierto que simplifica el proceso de creación, desarrollo y mantenimiento de **Agentes Conversacionales**. Es una alternativa popular a las APIs nativas, ya que maneja gran parte de la complejidad subyacente.

#### **Ventajas de SCRAPI**

- Maneja la **autenticación y regionalización** de forma automática.
    
- **Reduce la cantidad de código** necesario.
    
- Permite trabajar con datos en estructuras de Python familiares (listas, diccionarios).
    
- Ofrece **extensiones** que se integran con herramientas de uso diario:
    
    - **`Pandas DataFrames`**: Se usa para importar y exportar datos.
        
    - **Google Sheets**: Permite a los equipos de operaciones gestionar y modificar la NLU (unidad de comprensión del lenguaje) de los agentes de forma bidireccional.
        
    - **Cloud Functions**: Permite construir _webhooks_.
        
    - Capacidades avanzadas de _Machine Learning_.
        
- Permite **extraer recursos** (como _intents_ y entidades) para modificarlos y luego volver a escribirlos o transferirlos a otros agentes.
    
- Los recursos pueden almacenarse en un **control de versiones externo** (como `Gitlab` o `Github`) para crear **flujos CI/CD** para la creación, mantenimiento y control de calidad de _bots_.

---

# Extracción de Data Insights

Primero, configura una plantilla de la **API de Prevención de Pérdida de Datos** para enmascarar la información sensible. Segundo, habilita las opciones de **"Conversation History"** y **"BigQuery Export"** en la configuración del agente. Tercero, selecciona el conjunto de datos y la tabla de destino, que deben estar en el mismo proyecto que el agente.

---

### **Consideraciones para la exportación a BigQuery**

- **Proyecto:** El agente y el conjunto de datos de BigQuery deben estar en el mismo proyecto de Google Cloud.
    
- **Esquema de la tabla:** La tabla debe tener la estructura correcta para almacenar la información de las interacciones, incluyendo metadatos y objetos completos de solicitud y respuesta.
    
- **Particionamiento:** Particionar la tabla ayuda a optimizar el rendimiento de las consultas analíticas y a gestionar los costos, además de permitir la definición de una política de caducidad de datos.
    

---

### **Filtrado de logs en Cloud Logging**

- **Filtros básicos:** Permiten buscar un campo específico o combinar búsquedas con operadores `and` y `or`.
    
- **Filtros avanzados:** Ofrecen más flexibilidad, permitiendo el uso de caracteres comodín, rangos, expresiones booleanas y la búsqueda en campos de tiempo (`timestamp`).

---

# Disaster Recovery

### **1. Continuidad del Negocio (BCP)**

Un plan de continuidad del negocio (`BCP`) describe cómo los servicios esenciales seguirán operando a pesar de las interrupciones. Para implementar un BCP sólido, se recomienda:

- **Entender los procesos existentes:** Colabora con los equipos de operaciones y seguridad para integrar sus procesos de respaldo y continuidad en tu plan.
    
- **Usar flujos CI/CD:** Implementa _pipelines_ de integración continua y despliegue continuo para la construcción y despliegue de agentes. Esto asegura un proceso coordinado y eficaz.
    

### **2. Recuperación ante Desastres (DR)**

El plan de recuperación ante desastres (`DRP`) es una parte del BCP. Contempla tres tipos de acciones:

- **Preventivas:** Planificar y familiarizarse con la documentación relevante.
    
- **Detectivas:** Configurar alertas para monitorear fallos en tiempo real.
    
- **Correctivas:** Establecer procedimientos para prepararse y recuperarse de las interrupciones.
    

Dos métricas clave para la recuperación ante desastres son:

- **RTO (`Recovery Time Objective`):** El tiempo máximo de inactividad tolerable después de un incidente.
    
- **RPO (`Recovery Point Objective`):** La cantidad máxima de datos que se puede perder.
    

---

### **3. Mejores prácticas y recomendaciones**

- **Logs y monitoreo:** Configura tus agentes para usar **Cloud Logging**. Esto te permite monitorear la salud del servicio y crear métricas personalizadas.
    
- **Copias de seguridad (`Backups`):**
    
    - **Agentes Conversacionales** crea copias de seguridad de forma periódica después de cada cambio. También se pueden hacer manualmente.
        
    - Estas copias de seguridad son instantáneas completas del estado del agente y ayudan a acortar el **RPO** en caso de un incidente.
        
    - Es recomendable exportar estas copias de seguridad a un repositorio de código (`Gitlab`, `Github`) o a un _bucket_ de **Cloud Storage**.
        
- **Webhooks y dependencias:**
    
    - Haz una lista de todos los servicios relacionados con tus agentes, incluyendo los _webhooks_ y sus dependencias externas.
        
    - Diseña tus _webhooks_ para que proporcionen continuidad e informes de errores.
        
    - Configura tus agentes para que manejen problemas de latencia y disponibilidad con los _webhooks_ de forma fluida.
        
- **Alta disponibilidad:**
    
    - La mejor práctica para garantizar la disponibilidad es usar un **agente global único**.
        
    - Este agente global puede redirigir automáticamente las solicitudes a una región saludable en caso de una interrupción regional.
        
- **Pruebas:**
    
    - Es crucial probar los planes de recuperación ante desastres de forma regular.
        
    - Simula escenarios de interrupción de extremo a extremo, incluyendo los agentes conversacionales y todos sus componentes relacionados (`webhooks`, etc.), para identificar y corregir cualquier brecha.
        

---