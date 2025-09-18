---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Customer Engagement Suite with Google AI Architecture/04 Security and Compliance/"}
---

# Índice

[[#Data Security]]
[[#Redacción de PII]]
[[#Otras consideraciones]]

---

# Data Security

### **Seguridad de los datos**

La seguridad de los datos es una prioridad en cualquier implementación de **CES**. Esto implica definir cómo se transferirán, recibirán y retendrán los datos de forma segura.

- **Encriptación:** Todos los datos en una implementación **CCaaS** están encriptados tanto en tránsito como en reposo.
    
    - **En reposo:** Los datos almacenados por **Agentes Conversacionales** están encriptados por defecto con el algoritmo **AES256**.
        
    - **En tránsito:** Los mensajes de los usuarios finales a los agentes conversacionales están encriptados en tránsito por defecto.
        
- **Gestión de claves:** Google Cloud usa sistemas de gestión de claves endurecidos, que proporcionan controles de acceso y auditoría estrictos. No se necesita configuración manual.
    
- **Google Front End (GFE):** Termina el tráfico entrante, proporciona contramedidas contra ataques **DDoS** y enruta el tráfico a los servicios de Google Cloud.
    

### **Logs y retención de datos**

Tienes la opción de habilitar o deshabilitar el registro de los **Agentes Conversacionales**:

- **Habilitado:**
    
    - Los datos de la conversación se guardan en un almacenamiento interno de Google Cloud.
        
    - Puedes configurar el tiempo de retención (generalmente de 1 a 30 días).
        
    - Puedes solicitar la eliminación de los datos, que se vuelven inaccesibles inmediatamente y se borran físicamente en 24 horas.
        
    - Puedes usar las plantillas de la **API DLP** para redactar datos sensibles en tiempo real.
        
    - **Recomendación de Google:** Habilitar el registro para usar todas las funcionalidades del producto.
        
- **Deshabilitado:**
    
    - No se guarda ninguna conversación.
        
    - Puedes usar el _fulfillment_ para guardar los datos en una solución de almacenamiento de tu elección.

---
# Redacción de PII

### **Mecanismos de redacción**

El servicio de Google Cloud para esta tarea es **Sensitive Data Protection**, que incluye la **API de Prevención de Pérdida de Datos (Cloud DLP)**. Esta API identifica patrones de datos sensibles (números de tarjetas de crédito, de seguridad social, etc.) y los enmascara o elimina de los logs y transcripciones.

#### **Integración con Agentes Conversacionales**

Para configurar la redacción en **Agentes Conversacionales**, se usan las "Configuraciones de Seguridad" (`Security Settings`). El proceso es el siguiente:

1. **Crea plantillas:**
    
    - **Plantilla de inspección:** Define qué tipos de datos quieres redactar.
        
    - **Plantilla de desidentificación:** Especifica el método de redacción (ej. enmascaramiento).
        
2. **Referencia las plantillas:** Vincula estas plantillas en la página de **Configuraciones de Seguridad** del agente.
    
3. **Configura los parámetros:** En la página de parámetros, puedes marcar un parámetro específico para que se redacte en los logs, lo que es útil para datos sensibles que se capturan en las interacciones.
    

#### **Características de la API DLP**

- Está encriptada en tránsito.
    
- Es **sin estado (`stateless`)** y no persistente.
    
- Soporta **residencia de datos**, permitiendo procesar la información en una región específica.
    
- Es **síncrona**, es decir, devuelve una respuesta inmediatamente después de procesar la solicitud.
    

### **Redacción en otros componentes de CES**

- **Agent Assist:** La redacción de **PII** funciona de la misma manera que en **Agentes Conversacionales**, enmascarando los datos de las transcripciones en tiempo real. Se configura en el apartado de **"Conversation Profile Security Settings"**.
    
- **Conversational Insights:** Para redactar PII antes de analizar las transcripciones, se usan las plantillas de inspección y desidentificación con la **API de Conversational Insights**. Es posible configurar los ajustes de redacción de forma individual para cada solicitud.

---

# Otras consideraciones

### **1. Controles de seguridad**

Hay cuatro componentes clave que dictan los controles de seguridad en los servicios de **CES**:

- **Residencia de datos (`DRZ`):** Permite elegir la ubicación de almacenamiento de los datos en reposo. Se define en función del tipo de datos (contenido principal del cliente, configuración, metadatos, etc.), el estado de los datos (en reposo, en uso, en tránsito) y la ubicación geográfica (zona, región, jurisdicción).
    
- **Transparencia de acceso (`AxT`):** Permite recibir logs en tiempo real cuando un empleado de Google accede a los datos del cliente. Estos logs incluyen información como el recurso afectado, la razón del acceso, la hora y la ubicación del empleado.
    
- **Claves de encriptación gestionadas por el cliente (`CMEK`):** Permite a los clientes usar una clave de encriptación que ellos gestionan en **Cloud Key Management Store (KMS)** para encriptar sus datos en reposo. Una vez activada, no se puede cambiar la clave ni convertir recursos no encriptados.
    
- **Controles de servicio de VPC (`VPC-SC`):** Permite controlar el acceso a los datos desde redes de confianza. Es crucial para prevenir la exfiltración de datos, replicar arquitecturas de seguridad _on-premises_ y proteger la información sensible. Asegura que los servicios sean accesibles solo para usuarios y redes autorizadas, independientemente de las políticas de **IAM**.
    

---

### **2. Cumplimiento con PCI DSS**

**Agentes Conversacionales** y **CES** permiten el cumplimiento del estándar de seguridad de datos de la industria de tarjetas de pago (**PCI DSS**). Los pasos esenciales son:

- **Desidentificar los datos PCI:** Usar plantillas de **Cloud DLP** para eliminar la información sensible de los logs.
    
- **Redactar la entrada del usuario:** Usar la redacción de parámetros en el agente para evitar que la información sensible aparezca en la transcripción.
    
- **Eliminar datos de forma rápida:** Borrar o sobrescribir los datos sensibles tan pronto como ya no sean necesarios.
    
- **Encriptar datos con _webhooks_:** Es una medida importante si los sistemas descendentes no son compatibles con **PCI DSS**.
    

---

### **3. Certificaciones de cumplimiento**

**Agentes Conversacionales** es compatible con varias certificaciones clave:

- **HIPAA:** Protege la información de salud electrónica.
    
- **ISO 27001:** Estándar internacional para la gestión de la seguridad de la información.
    
- **ISO 27017:** Guía para la seguridad en la nube, con controles para la responsabilidad compartida, la configuración de máquinas virtuales y la protección del entorno virtual.
    
- **ISO 27018:** Se centra en la protección de **PII** en la nube.
    
- **ISO 27701:** Estándar global de privacidad que se enfoca en la recopilación y procesamiento de **PII**.
    
- **SOC 1:** Un informe sobre los controles internos relevantes para la información financiera del cliente.
    
- **SOC 2:** Evalúa los sistemas de información de una organización en relación con criterios de seguridad, disponibilidad, integridad de procesamiento, confidencialidad y privacidad.
    
- **SOC 3:** Un informe público de los controles internos sobre seguridad, disponibilidad, integridad de procesamiento y confidencialidad.

---

