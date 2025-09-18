---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Incorporate Generative Features into Conversational Agent Flows/01 Generators/"}
---

# Índice

[[#Generadores en agentes conversacionales]]
[[#Parámetros y selección de modelo]]
[[#Ejemplos]]
[[#Cómo configurar y desplegar generadores]]
[[#Respuestas basadas en código]]

---

# Generadores en agentes conversacionales

Los **generadores** son una función que permite a los agentes conversacionales usar los modelos de lenguaje de Google para crear respuestas dinámicas en tiempo real. Esto los hace una herramienta poderosa que integra la IA generativa en flujos estructurados y determinísticos.

#### **Capacidades de los generadores**

- **Respuestas dinámicas:** Pueden generar respuestas que no son estáticas, utilizando conocimiento general o el contexto de la conversación.
    
- **Uso del contexto:** Capturan el contexto de la conversación, como un resumen de lo que se ha dicho, para crear respuestas más personalizadas.
    
- **Integración con _webhooks_:** El texto generado puede usarse como entrada para un _webhook_ o para pre-establecer parámetros en el flujo.
    
- **Encadenamiento de llamadas:** Permiten encadenar múltiples llamadas a modelos de lenguaje (LLM) para crear flujos híbridos más complejos.
    
- **Controles de IA responsable:** Cuentan con configuraciones que te permiten establecer "barreras de seguridad" para bloquear respuestas dañinas u ofensivas.
    

#### **Funciones de los generadores**

Los generadores se pueden usar en múltiples casos prácticos:

- **Resúmenes:** Resumir artículos o la conversación en curso.
    
- **Análisis de sentimiento:** Evaluar el sentimiento del cliente en tiempo real.
    
- **Actualización de datos:** Convertir la información de la conversación en formatos de datos estructurados, como JSON.
    
- **Toma de decisiones:** Evaluar la elegibilidad de un usuario basándose en el contexto y el conocimiento, para luego dirigir la conversación de manera apropiada.

---

# Parámetros y selección de modelo

### **Personalización de Generadores**

Los **generadores** permiten crear respuestas dinámicas en tiempo real a través de la personalización de _prompts_, parámetros y la selección del modelo.

#### **1. _Prompts_ personalizados**

- **Qué son:** Un _prompt_ es una instrucción o pregunta en lenguaje natural que se envía a un modelo de lenguaje para obtener una respuesta. Pueden incluir preguntas, instrucciones, contexto, ejemplos, etc.
    
- **Instrucciones claras:** Para obtener una respuesta satisfactoria, el _prompt_ debe ser una pregunta o solicitud clara. Se puede instruir al modelo sobre cómo comportarse, por ejemplo, "sé un experto en resumen de texto".
    
- **Marcadores de posición (`placeholders`):** Puedes hacer los _prompts_ contextuales usando marcadores de posición (`$nombre-del-marcador`). Estos se asocian con parámetros de la sesión y se reemplazan por los valores capturados durante la conversación.
    
- **Marcadores de posición integrados:** Existen marcadores especiales que no necesitan ser asociados manualmente, como:
    
    - `$conversation`: Contiene la conversación completa entre el agente y el usuario.
        
    - `$last-user-utterance`: Contiene la última frase del usuario.
        

#### **2. Parámetros del modelo**

- Puedes seleccionar el modelo de lenguaje que deseas usar (ej., Gemini Pro, Flash o Ultra).
    
- Se pueden ajustar los parámetros del LLM, como `Temperature`, `Top P` y `Top K`, para controlar la aleatoriedad de la respuesta.
    

### **Generadores vs. API de Vertex AI**

La funcionalidad de los generadores es muy similar a la API de Vertex AI, ya que utilizan el mismo _backend_. Sin embargo, hay algunas diferencias clave:

- **Integración de parámetros:** La principal diferencia es que en los generadores de Conversational Agents los parámetros se sustituyen automáticamente en el _prompt_ dentro de la herramienta. En la API de Vertex AI, el desarrollador tendría que analizar y enviar la respuesta completa.
    
- **Funciones adicionales:** La API de Vertex AI actualmente ofrece más funciones, como `Max responses`, `stop sequences`, `streaming responses` y `safety filters`. Estas características podrían ser añadidas a los generadores de Conversational Agents en el futuro.

---

# Ejemplos

Los generadores se pueden personalizar con _prompts_ específicos para realizar diversas tareas, lo que los hace muy versátiles en un agente conversacional.

#### **Resumir contenido**

- **Prompt:** Para resumir texto, primero das una instrucción general sobre el objetivo (ej., "sé un experto en resumen de texto"). Luego, defines un marcador de posición para el texto de entrada (ej., `$text`) y describes el formato de salida deseado (ej., "un resumen conciso de 1 o 2 frases").
    
- **Ejemplo de uso:** El agente puede resumir una conversación completa entre el humano y la IA. En este caso, el _prompt_ incluirá el marcador `$conversation` y el marcador `$last-user-utterance` para asegurarse de que el resumen es preciso.
    

#### **Responder preguntas con conocimiento**

- **Prompt:** Puedes instruir al generador para que responda preguntas de forma cortés.
    
- **Fuentes de conocimiento:**
    
    1. **Conocimiento interno:** El generador usará la información de sus datos de entrenamiento. Sin embargo, no hay garantía de que la información sea actual o veraz.
        
    2. **Información externa:** Para respuestas precisas y actualizadas, puedes conectar el generador a un sistema de búsqueda (como una base de datos) para recuperar información dinámicamente. El generador se instruye para responder basándose solo en la información proporcionada.
        

#### **Manejar la escalada a un agente humano**

- **Prompt:** El generador se configura para actuar como un agente de servicio al cliente que transfiere llamadas.
    
- **Instrucciones:** Se le pide que responda de manera cortés y que asegure al usuario que hará lo posible por ayudarlo. Para evitar respuestas demasiado extensas o innecesarias, puedes incluir instrucciones como "No hagas preguntas" y "No preguntes si hay algo más en lo que puedas ayudar".
    

#### **Optimizar una búsqueda en Google**

- **Prompt:** Se le indica al generador que actúe como un experto en búsquedas en Google. La tarea es convertir la frase del usuario en un término de búsqueda conciso y de alta calidad.
    
- **Ejemplo:** El _prompt_ puede incluir un ejemplo de entrada (`query del usuario`) y salida (`query optimizado`) para guiar al modelo sobre el comportamiento esperado. Esto le permite al agente transformar una frase compleja en una búsqueda efectiva.

---

# Cómo configurar y desplegar generadores

Para empezar, debes crear un generador en la consola de agentes conversacionales y luego asociarlo a tus flujos.

#### **1. Crear el generador**

- En la consola, ve a la pestaña **`Manage`** y selecciona **`Generators`**.
    
- Haz clic en **`Create New`**.
    
- Asigna un nombre al generador y configura el _prompt_, el modelo y los controles.
    
- Puedes añadir varios generadores a un mismo _fulfillment_ para **encadenar sus resultados**. Esto puede ayudarte a depurar y controlar mejor cada paso, por ejemplo, usando un generador para obtener información y otro para resumirla antes de dársela al usuario.
    

#### **2. Usar el generador en un flujo**

- En la configuración de una ruta, en la sección **`Fulfillment`**, activa la opción **`Generators`**.
    
- Selecciona el generador que creaste.
    
- **Asocia los marcadores de posición** del _prompt_ con los parámetros de sesión que hayas definido. Si tu _prompt_ solo usa marcadores de posición incorporados (como `$conversation`), no necesitas hacer esta asociación.
    

#### **3. Usar la salida del generador**

- A la salida de un generador se le asigna un nombre de variable único (ej., `request generative destination`).
    
- Esta variable se puede usar como cualquier otro **parámetro de sesión**. Puedes usarla en la respuesta del agente, en _webhooks_ o para pre-establecer otros parámetros.

---

# Respuestas basadas en código

La función de generadores en agentes conversacionales te permite crear código dinámicamente a partir de descripciones en lenguaje natural. Los modelos de Gemini están capacitados en una gran cantidad de datos de código para responder preguntas y generar soluciones en varios lenguajes de programación (como Go, SQL, Java, Javascript, Python y Typescript).

#### **Casos de uso para la generación de código**

Los generadores pueden ser útiles para varias tareas relacionadas con el código:

- **Generación de código:** Escribir código desde cero.
    
- **Generación de pruebas unitarias:** Crear pruebas para el código existente.
    
- **Corrección de código:** Encontrar y solucionar errores.
    
- **Optimización de código:** Mejorar la eficiencia del código.
    
- **Traducción de código:** Convertir código de un lenguaje a otro.
    

#### **Consideraciones de seguridad**

Es crucial informar a los usuarios sobre las limitaciones del código generado:

- **No reemplaza a un humano:** La generación de código no sustituye el trabajo de un desarrollador.
    
- **Requiere pruebas:** El código debe ser exhaustivamente probado antes de usarse en un entorno de producción.
    
- **Evita usos sensibles:** No debe usarse para soluciones en industrias sensibles, como ciberseguridad o prevención de _hacking_.
    

#### **Cómo configurar un generador para código**

Para que un generador cree código, el _prompt_ debe ser claro y estructurado:

1. **Define el objetivo:** Indica al generador que su tarea es escribir código para resolver un problema.
    
2. **Usa marcadores de posición:** Incluye marcadores de posición para el **problema** (`$problem`) y el **lenguaje de programación** (`$programming_language`).
    
3. **Solicita la solución:** Termina el _prompt_ pidiendo al generador que proporcione el código.
    

Esto permite al generador tomar los datos del usuario (el problema y el lenguaje) y generar una solución de código en consecuencia.

---