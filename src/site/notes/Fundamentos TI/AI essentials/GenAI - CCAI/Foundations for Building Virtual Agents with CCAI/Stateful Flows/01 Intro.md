---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Stateful Flows/01 Intro/"}
---

[[#Flujos]]
[[#Construir una taxonomía]]

# Flujos

### **Cómo crear agentes virtuales con flujos**

Los **flujos** (`Flows`) te permiten construir experiencias conversacionales con lógica **determinista**, lo que significa que el comportamiento del agente está predefinido. Son ideales para casos que requieren precisión, cumplimiento de reglas y lógica paso a paso.

---

### **Conceptos clave en los flujos**

1. **Drivers:** Son categorías de objetivos generales del usuario, como "facturación" o "estado de la orden".
    
2. **Intents (`Intenciones`):** Capturan grupos de expresiones de usuario que tienen el mismo propósito. Por ejemplo, "Quiero pagar mi factura" o "Pagar la cuenta" se agrupan en una intención llamada `pagar-factura`.
    
3. **Entities (`Entidades`):** Son las piezas de información clave que se extraen de las expresiones del usuario, como sustantivos o cuantificadores. Por ejemplo, en la frase "Quiero pagar $100 el 5 de julio", "$100" y "5 de julio" serían entidades.
    

#### **Diferencia entre intenciones y entidades**

- Una **intención** identifica el **propósito** de la frase completa del usuario (ej., "agendar un pago").
    
- Una **entidad** extrae la **información específica** dentro de esa frase (ej., "$100" y "5 de julio").
    

#### **Tipos de intenciones**

- **Intención principal (`Head intent`):** Identifica la tarea principal que el usuario quiere lograr. Suele ser la primera en la conversación (ej., "revisar estado de orden").
    
- **Intención contextual (`Contextual intent`):** Captura expresiones adicionales que el usuario hace durante la conversación, como preguntas secundarias ("¿cuánto debo?") o respuestas sencillas ("sí", "no").
    

---

### **Consejos para la creación**

- **Identifica las intenciones:** Busca los verbos o las frases que expresan la intención del usuario. La mejor manera es analizar cómo se expresan tus clientes e incluirlas como frases de entrenamiento.
    
- **Identifica las entidades:** Busca los sustantivos o cuantificadores que te darán los detalles de la interacción (ej., nombres, fechas, números).
    
- **Personaliza la conversación:** Usa las entidades para extraer datos del usuario (como su nombre o su canción favorita) y luego repítelos en la conversación para que se sienta más natural.

---

Un buen **agente conversacional** requiere una **taxonomía** bien definida. Una taxonomía es una manera de categorizar los objetivos del usuario, los cuales son el pilar fundamental de cualquier conversación. Una taxonomía para el desarrollo de agentes conversacionales implica: **categorizar los objetivos del usuario en _drivers_**, **identificar las intenciones principales y contextuales** y luego asociar estas, según corresponda, con tus _drivers_.

---

# Construir una taxonomía

**Los tres datos que necesitas**
Para empezar a construir una taxonomía, necesitas tres piezas de datos principales:

1. **Transcripciones de conversaciones:** Son transcripciones de conversaciones similares a las que intentas modelar. Pueden ser de humano a humano o de humano a agente. Es crucial eliminar cualquier **información de identificación personal (PII)** por motivos de privacidad.
    
2. **Conjuntos de datos de conversaciones:** Colecciones de transcripciones de conversaciones.
    
3. **Enlaces externos del cliente:** Enlaces que se pueden usar para redirigir a los usuarios a fuentes externas para autoservicio o información adicional.
    

Cuando no hay transcripciones históricas disponibles para un nuevo caso de uso, tendrás que hacer suposiciones sobre lo que los usuarios podrían decir en ciertos puntos de la conversación.

---

### **Construyendo una taxonomía: El proceso**

Construir una taxonomía sólida es un proceso iterativo que ayuda a garantizar que el modelo de comprensión del lenguaje natural (NLU) del agente funcione de manera efectiva. El proceso de alto nivel es el siguiente:

1. **Identifica los _drivers_ clave:** Estas son las categorías principales de los objetivos del usuario. Puedes consultar con expertos en la materia, analizar planes de proyectos existentes o leer transcripciones de conversaciones para identificarlos. Por ejemplo, en el contexto de una empresa de telecomunicaciones, los _drivers_ podrían ser "facturación", "estado de la orden" o "resolución de problemas".
    
2. **Identifica las intenciones principales:** Son las acciones principales que un usuario quiere realizar dentro de cada _driver_. Es mejor identificarlas _driver_ por _driver_. Por ejemplo, bajo el _driver_ "facturación", podrías tener "pagar factura" o "cambiar fecha de vencimiento". Puedes usar métodos similares a los de la identificación de _drivers_: consultar con expertos, leer transcripciones o usar aprendizaje automático.
    
3. **Identifica las intenciones contextuales:** Son expresiones adicionales que no se relacionan directamente con la tarea principal, pero que son esenciales para una conversación natural. A menudo se dividen en tres categorías comunes:
    
    - **Flujo conversacional:** Respuestas simples como "sí", "no" o "repite eso".
        
    - **Preguntas secundarias:** Preguntas que surgen en medio de una tarea, como preguntar "¿cuánto debo?" mientras se está en el proceso de pagar una factura.
        
    - **Expresiones dependientes del contexto:** Respuestas que solo tienen sentido en el contexto de la conversación anterior, como responder con "¿cuánto es?" a la pregunta, "¿Cuál es tu pregunta sobre la facturación?".
        

A medida que construyes tu taxonomía, también es una buena práctica comenzar a identificar las **frases de entrenamiento** para tus intenciones y las **entidades** (los sustantivos o cuantificadores que necesitas extraer).

---

### **Riesgos de una taxonomía incompleta**

Una taxonomía incompleta, que carezca de _drivers_ o intenciones, puede llevar a varios riesgos:

- **Detección de intención incorrecta:** El agente puede malinterpretar las consultas del usuario, lo que lleva a respuestas incorrectas o confusas.
    
- **Reducción del compromiso del usuario:** Los usuarios serán menos propensos a usar un agente que los malinterpreta constantemente, lo que lleva a una disminución de la satisfacción del cliente.
    
- **Aumento de los costos:** Un agente que no puede manejar las consultas de los usuarios correctamente requerirá una mayor intervención humana, lo que aumenta los costos operativos.

---

