---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Advanced Performance Measurement/01 Understanding Conversational Agents log data/"}
---

# Índice

[[#Habilitar Logs]]
[[#Estructura]]
[[#Entender los logs]]

---

# Habilitar Logs

### **Habilitar y usar los registros de Dialogflow CX**

Para habilitar la función, tienes que ir a la configuración del agente (`Agent Settings`) y activar los registros de **Cloud Logging**. Al hacerlo, se registrarán todos los datos de las interacciones, lo que te permitirá analizarlos posteriormente.

Los registros te permiten:

- **Analizar el flujo de conversación:** Entender cómo navegan los usuarios por el diálogo, dónde encuentran obstáculos y qué caminos son los más frecuentes. Esto te ayuda a refinar los flujos para una interacción más fluida.
    
- **Identificar errores de comprensión:** Revelan dónde el agente tiene dificultades para entender la intención del usuario. Al analizar malinterpretaciones o respuestas fallidas, puedes corregir las debilidades en tus datos de entrenamiento o modelos de **NLP**.
    
- **Registrar el historial de transacciones:** Captura la interacción del usuario como parte de su historial de transacciones, lo que proporciona **información valiosa (`insights`)** para optimizar el agente y mejorar la participación del usuario.
    
- **Realizar análisis de rutas:** Muestra las rutas más frecuentes que toman los clientes en las conversaciones.

---

# Estructura

### **Conceptos de conversación**

- **Conversación:** Cualquier interacción entre un usuario y un agente en un momento dado.
    
- **Turno:** Un par que consiste en una frase del usuario y una respuesta del agente. Una respuesta del agente puede contener varias frases.
    

### **Lenguaje específico de Dialogflow CX**

- **Flujos:** Se usan para organizar conversaciones complejas en torno a temas específicos, como la autenticación o el saldo de una factura. Cada agente empieza con un flujo predeterminado (`Default Start Flow`).
    
- **Páginas:** Componentes dentro de un flujo que capturan información, preguntas y respuestas.
    
    - **Páginas de entrada (`Input Pages`):** Piden información al usuario.
        
    - **Páginas de enrutamiento (`Routing Pages`):** Contienen la lógica de negocio para dirigir la conversación hacia un resultado exitoso. Muchas de estas páginas intermedias no aparecen en las transcripciones.
        
- **Intenciones:** Representan el objetivo del usuario. Hay dos tipos:
    
    - **Intención principal (`Head Intent`):** El objetivo principal de la interacción (ej. hacer un pago).
        
    - **Intención suplementaria o contextual:** Intenciones adicionales que proporcionan detalles o aclaraciones (ej. decir "sí" o "no" a una pregunta).

---

# Entender los logs

Para examinar los registros de **Dialogflow CX**, se usa la herramienta **Logs Explorer** en la consola de **GCP**. Estos registros son cruciales para medir el rendimiento del _bot_ y proporcionan una visión detallada de cada transición de estado en una conversación.

---

### **Pasos para revisar los registros**

1. **Filtra por nombre de registro:** Asegúrate de que solo se muestren los registros de **Dialogflow CX**.
    
2. **Filtra por `Session ID`:** Usa este identificador (también llamado `Conversation ID`) para ver todas las entradas de un solo diálogo.
    
3. **Filtra por tipo de respuesta final:** Busca la palabra "final" para obtener el registro que representa el estado final de cada turno.
    

### **Estructura de una entrada de registro**

Cada entrada de registro es un objeto **JSON** con campos clave:

- **`insertId`:** Un ID único para la entrada.
    
- **`timestamp`:** La hora de inicio del turno.
    
- **`logName`:** El nombre de la API de Google que generó el registro.
    
- **`labels`:** Contiene información de contexto, como el `Session ID`.
    

### **Carga útil (`Payload`) de la respuesta JSON**

El campo **`jsonPayload`** es la parte más importante. Dentro de este, el campo **`queryResult`** tiene información detallada sobre las transiciones de estado del _bot_ en ese turno:

- **`transcript`:** La frase del usuario.
    
- **`language`:** El idioma del _bot_.
    
- **`match`:** Contiene información sobre la coincidencia de intenciones, incluyendo el tipo de coincidencia, el nombre de la intención detectada y el puntaje de confianza (`confidence score`).
    
- **`parameters`:** Los parámetros de la sesión establecidos al final del turno.
    
- **`responseMessages`:** Las respuestas del _bot_ en ese turno. Puede haber varias si el _bot_ pasó por varios pasos intermedios.
    
- **`diagnosticInfo`:** Proporciona información detallada, paso a paso, sobre lo que ocurrió. Es útil para la depuración y para establecer métricas personalizadas. Contiene la secuencia de ejecución (`Execution Sequence`), que muestra las páginas, flujos e intenciones activadas en el turno.