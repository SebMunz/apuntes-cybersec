---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/05 Model Deployment/"}
---

### Apuntes sobre el despliegue del modelo

- **Propósito:** Una vez que el modelo personalizado ha sido entrenado y validado, el objetivo es moverlo al entorno de producción del cliente para que pueda ser utilizado.
- **Pasos clave del despliegue:**
    1. **Creación del modelo (`Model Creation`):**
        - Se copia el modelo, una vez entrenado y evaluado en el entorno de desarrollo, al "Entorno del cliente" (`Client Tenant Environment`).
        - Se puede usar la sección `From Saved Model` del `Model Management Colab` para realizar esta acción.
        - El modelo ahora estará visible en la consola de Agent Assist del cliente.
    2. **Despliegue del modelo (`Deploying the Model`):**
        - El despliegue se puede hacer de dos maneras:
            - Directamente a través de la **consola de la UI**.
            - Usando el _backend_ con el `Model Management Colab`.
    3. **Vinculación del modelo con el perfil de conversación (`Linking the Model to the Conversation Profile`):**
        - Este es el paso final para que el modelo esté operativo.
        - Se integra el modelo a un perfil de conversación existente o se crea uno nuevo.
        - Esta acción se realiza a través de la **consola de Agent Assist**.
        - El `integration id` del perfil de conversación se usa para hacer llamadas a las APIs de Agent Assist.
- **Consideraciones:**
    - Cada uno de estos pasos es crucial para asegurar que el modelo no solo se despliegue con éxito, sino que también esté optimizado para el rendimiento en escenarios reales.
