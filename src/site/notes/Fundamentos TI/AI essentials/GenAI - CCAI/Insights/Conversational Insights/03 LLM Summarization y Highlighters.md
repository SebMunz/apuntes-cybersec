---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/03 LLM Summarization y Highlighters/"}
---

# Resúmenes con LLM

- **Objetivo:** Proporciona resúmenes de conversaciones para los agentes de centros de contacto.
    
- **Funcionamiento:** Utiliza un modelo de lenguaje grande (LLM) y no requiere entrenamiento adicional para datos de voz y chat.
    
- **Activación:** Se puede activar configurando el anotador de resumización en `true` durante el análisis de una conversación.
    
- **Personalización:** Se puede personalizar el resumen seleccionando secciones predefinidas, como:
    
    - **`Situation`**: La necesidad o pregunta del cliente.
        
    - **`Action`**: La acción que tomó el agente.
        
    - **`Resolution`**: El resultado del servicio (Sí, No, Parcial o N/A).
        
    - **`Customer Satisfaction`**: La satisfacción del cliente (Satisfecho o insatisfecho).
        
    - **`Reason for cancellation`**: El motivo de cancelación (solo si aplica).
        
    - **`Entities`**: Entidades clave extraídas de la conversación.
        
- **Consideraciones:** Los resúmenes de baja calidad pueden ser descartados, en cuyo caso la respuesta será vacía.
    

---

### **Cómo habilitar la resumización con LLM**

Existen dos métodos para habilitar esta funcionalidad:

1. **A través de la interfaz de usuario (`UI`):**
    
    - Navega a la sección de **Summarization** en la consola de **Agent Assist**.
        
    - Crea un generador.
        
    - Haz clic en **Start**.
        
    - Configura el modelo para incluir las secciones relevantes para tu caso de uso.
        
2. **A través de la API:**
    
    - Se puede habilitar mediante una serie de comandos `curl` en la **API de Insights**.
        
    - Para recuperar el resumen, se necesita un **ID de perfil de conversación**.
        

---

### **Demostración y características adicionales**

- En la demostración, se muestra el proceso completo sobre conversaciones ya ingeridas. Se observa cómo el modelo genera un resumen en un panel lateral, extrayendo información clave de cada sección.
    
- La resumización con LLM se considera una **versión base (`Baseline model v2.0`)** que se activa como un modelo personalizado.

---

# Highlighters

### **1. Marcadores (`Highlighters`)**

Un marcador contiene palabras o frases clave que **Conversational Insights** reconoce como importantes para determinar la intención del usuario. Ayudan a identificar segmentos de una conversación relevantes para un área de interés.

- **Marcadores inteligentes (`Smart highlighters`):** Están preconfigurados con un conjunto de frases comunes, como las relacionadas con la autenticación o la confirmación de la resolución de un problema.
    
- **Marcadores personalizados (`Custom highlighters`):** Puedes crear tus propios marcadores para identificar frases o palabras específicas de tu negocio. Ejemplos de uso:
    
    - **Menciones a la competencia:** Para identificar cuándo los clientes mencionan a competidores.
        
    - **Detección de entidades del cliente:** Para reconocer entidades que la extracción de NLP estándar no pudo, como "ESIM" o "MODB".
        
    - **Validación de cumplimiento:** Para asegurar que los agentes usen frases de seguridad específicas, como "necesito verificar información".
        
    - **Satisfacción del cliente:** Para identificar frases clave que confirmen el éxito de una interacción, como "Gracias, es todo lo que necesitaba".
        
    - **Problemas del sistema:** Para marcar menciones de fallos en aplicaciones, la cadena de suministro o la red.
        
- **Sinergia con el modelado de temas:** Usar marcadores junto con el modelado de temas proporciona un análisis más detallado de las conversaciones.
    
- **Coincidencia semántica (`Semantic match`):** La función de coincidencia semántica se enfoca en la coincidencia de conceptos en lugar de cadenas de texto exactas. Esto permite que el sistema comprenda el significado detrás de la consulta, incluso si se utilizan palabras diferentes.
    

---

### **2. Preguntas frecuentes generativas (`Generative FAQ`)**

- **Función:** La función de **LLM generative FAQ** en **Conversational Insights** muestra las preguntas que los clientes están haciendo a tu centro de contacto y cómo se responden.
    
- **Beneficios:** Esta información es útil para:
    
    - Identificar lagunas en tus preguntas frecuentes existentes.
        
    - Rastrear preguntas que se están volviendo tendencia.
        
    - Mejorar las respuestas del servicio al cliente.
        
- **Generación:** Las principales consultas se pueden generar fácilmente desde la consola de **Conversational Insights**.

---

