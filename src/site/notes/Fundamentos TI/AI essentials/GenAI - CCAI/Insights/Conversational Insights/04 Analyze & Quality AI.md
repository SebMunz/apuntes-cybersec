---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/04 Analyze & Quality AI/"}
---

# Índice

[[#Análisis]]

---

# Análisis

### **1. Análisis de conversaciones a través de la consola**

- **Requisitos:** Asegúrate de que todas las conversaciones estén cargadas en el panel de Insights y de que el modelo de temas esté entrenado y desplegado si es necesario.
    
- **Pasos:**
    
    1. Navega al panel de Insights y selecciona tu proyecto.
        
    2. Verifica el recuento de conversaciones en la sección `Conversation history`.
        
    3. Aplica filtros si solo quieres analizar un subconjunto de conversaciones.
        
    4. Haz clic en `Analyze` y establece el porcentaje de conversaciones a analizar.
        
    5. Haz clic en `Analyze number of conversations` para comenzar.
        

### **2. Análisis de conversaciones a través de la API**

- **Flujo de trabajo:** Este proceso se realiza utilizando un _Vertex AI workbench_.
    
    1. Crea un archivo llamado `request.json` donde especifiques el porcentaje de conversaciones a analizar.
        
    2. Usa un comando `curl` para enviar una solicitud de análisis masivo, reemplazando el ID del proyecto y la ubicación.
        
- **Operación de larga duración:** El análisis masivo es una operación que tarda un tiempo considerable. Puedes verificar el estado en la interfaz de usuario, revisando el ícono del reloj de arena en la esquina superior derecha del panel.
    

### **3. Revisión de las conversaciones analizadas**

Una vez finalizado el análisis, puedes verificar los resultados:

- **Verificación en la interfaz de usuario:** Realiza revisiones puntuales en el **Conversation Hub** para confirmar que los temas, los resúmenes, la detección de silencio y el análisis de sentimiento se generaron con precisión.
    
- **Confirmación de la precisión:** Revisa si los temas y los campos asignados reflejan con exactitud el contenido de las conversaciones.

---

