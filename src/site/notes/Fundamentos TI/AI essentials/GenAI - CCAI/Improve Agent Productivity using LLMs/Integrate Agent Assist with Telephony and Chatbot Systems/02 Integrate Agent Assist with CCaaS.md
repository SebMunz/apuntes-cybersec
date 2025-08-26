---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Integrate Agent Assist with Telephony and Chatbot Systems/02 Integrate Agent Assist with CCaaS/"}
---

# **Principios Fundamentales de la Integración**

La configuración se debe realizar en **dos lugares** distintos:

1. **En el Proyecto/Consola de Agent Assist** (Google Cloud).
2. **En la Plataforma CCaaS**.

---

### **Configuración en el Proyecto de Agent Assist**

1. **Crear un Conversation Profile:**
    - Crear y configurar un **Conversation Profile** en el proyecto de Agent Assist.
    - Habilitar en él todas las **funcionalidades deseadas** de Agent Assist (ej: Smart Reply, Knowledge Assist, Summarization).
2. **Crear una Clave de Cuenta de Servicio (Service Account Key):**
    - Crear una **Service Account** con los permisos necesarios.
    - Generar y descargar una **clave JSON** para esta cuenta. Esta clave dará permisos a CCaaS para usar el Conversation Profile.

---

### **Configuración en la Plataforma CCaaS**

1. **Habilitar la Plataforma Agent Assist:**
    - Ir a **`Developer Settings`** dentro de CCaaS.
    - **Añadir una nueva plataforma** de tipo "Agent Assist".
    - **Asignar un nombre** a la plataforma.
    - **Añadir y validar** la clave JSON de la Service Account creada en el paso anterior.
    - **Activar** la plataforma.
2. **Habilitar Features para Canales:**
    - Ir a la configuración de **Chat** y **Calls** (Llamadas) de CCaaS.
    - **Activar Agent Assist** y seleccionar **todas las funcionalidades** aplicables y requeridas para el caso de uso específico.
3. **Habilitar y Configurar para una Cola Específica:**
    - Navegar a la configuración de un **canal** (ej: Voice o Chat) y seleccionar una **cola** específica.
    - **Activar y configurar Agent Assist:**
        - Seleccionar la **Plataforma Agent Assist** añadida anteriormente.
        - Seleccionar el **Conversation Profile** aplicable (el creado en el proyecto de Agent Assist).
    - **Configurar Wrap Up (Opcional):** Para la feature de **Summarization** (Resumen automático), habilitar y configurar los ajustes de "Wrap Up" en la cola si es necesario.

---

### **Flujo de Pasos de Integración (Resumen)**

1. **Preparar en Cloud:** Crear Conversation Profile y Service Account Key en el proyecto de Agent Assist.
2. **En CCaaS > Developer Settings:** Añadir y activar la plataforma "Agent Assist" usando la clave JSON.
3. **En CCaaS > Chat/Call Settings:** Activar Agent Assist y seleccionar sus features.
4. **En CCaaS > Configuración de Cola:** Vincular la plataforma y el perfil de conversación a una cola específica.