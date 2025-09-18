---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Incorporate Generative Features into Conversational Agent Flows/02 Generative Fallbacks/"}
---

# Índice

[[#Fallback enablement level]]
[[#Configuración]]
[[#Seguridad]]

---

La función de **respuesta generativa de reserva** usa modelos de lenguaje grande (LLMs) con _prompts_ personalizados para responder cuando el agente no encuentra una coincidencia para la intención del usuario.

#### **Cómo funciona y por qué usarla**

En cada paso de la conversación, hay una posibilidad de que la frase del usuario no coincida con una intención del agente. Las respuestas de reserva generativa entran en juego en estos escenarios, funcionando como un **"pegamento conversacional"** para manejar situaciones comunes, como:

- El usuario pide que el agente repita algo.
    
- Conversaciones triviales (saludos, despedidas, etc.).
    
- El usuario pide un resumen de la conversación.
    

Sin una respuesta de reserva generativa, un agente podría dar una respuesta genérica como "Lo siento, no sé cómo ayudarte", lo que puede frustrar al usuario. Una buena respuesta de reserva debe ser contextual y útil, de manera similar a cómo respondería un agente humano.

#### **Ejemplo de un agente sin y con `Generative Fallback`**

Imagina un agente que le pregunta a un usuario a qué concierto quiere ir.

- **Sin `Generative Fallback`:** Si el usuario pregunta: "¿Cuándo viene **él** a la ciudad?", el agente no entenderá el pronombre "él" y repetirá su pregunta original. La conversación se estancará.
    
- **Con `Generative Fallback`:** El agente utiliza el contexto de la conversación para entender que "él" se refiere al artista del concierto. El agente puede entonces continuar la conversación por el camino deseado.
    

#### **Mejores prácticas**

Aunque la respuesta generativa de reserva es una herramienta poderosa, no reemplaza la importancia de un buen diseño de intención. La **mejor práctica** es siempre priorizar la creación de frases de entrenamiento variadas y sólidas para tus intenciones. Esto evita que ocurra un evento de "no-match" en primer lugar y mantiene las conversaciones en su camino previsto.

---

# Fallback enablement level

La **respuesta generativa de reserva** (`Generative Fallback`) se puede activar en los manejadores de eventos de "no coincidencia" en varios niveles, lo que permite al agente tener respuestas contextuales y más naturales cuando el usuario dice algo que el agente no espera.

#### **Nivel de flujo (`Flow level`)**

- **Cuándo usarlo:** Cuando el usuario tiene una conversación genérica antes de entrar en un flujo específico. Es útil para saludos, preguntas de propósito general ("¿Cómo estás?", "¿En qué puedes ayudarme?") o para definir términos.
    
- **Cómo funciona:** La respuesta generativa usa la **descripción del flujo** como contexto para responder adecuadamente y reconducir la conversación hacia el propósito principal del agente.
    
- **Cómo configurarlo:** Activa la respuesta generativa en los manejadores de eventos de la página de inicio del flujo.
    

#### **Nivel de página (`Page level`)**

- **Cuándo usarlo:** Cuando la conversación ya está en un flujo definido, pero el usuario hace una pregunta que no coincide con las intenciones configuradas para esa página.
    
- **Cómo funciona:** La respuesta generativa utiliza la **descripción de la ruta** activa como contexto para generar una respuesta relevante. Esto permite al agente responder preguntas específicas sobre el tema de la página, incluso si no hay una intención definida para ellas.
    
- **Cómo configurarlo:** Activa la respuesta generativa en los manejadores de eventos de "no coincidencia" en una página específica.
    

#### **Nivel de parámetro (`Parameter level`)**

- **Cuándo usarlo:** Cuando un usuario introduce un valor no válido mientras se le solicita un parámetro específico.
    
- **Cómo funciona:** El agente puede identificar la entrada no válida (ej., un destino que no está en la lista) y usar la IA generativa para dar una respuesta contextual que guíe al usuario a proporcionar la información correcta, como los rangos o las opciones disponibles.
    
- **Cómo configurarlo:** Abre la página que contiene el parámetro, ve a la sección de "Manejadores de eventos de re-solicitud" y activa la respuesta generativa para el manejador de "no coincidencia". Para parámetros numéricos, puedes usar expresiones regulares para definir un rango aceptable (ej., de 4 a 15).

---

# Configuración

Los _prompts_ de las respuestas generativas de reserva combinan lenguaje natural con información del agente y la conversación. Esto permite un control preciso sobre las respuestas del agente cuando no hay una coincidencia de intención.

#### **Plantillas de _prompts_**

Puedes usar plantillas predefinidas o crear una personalizada.

- **Plantilla por defecto (`Default`):** No se puede modificar directamente, pero puedes influir en las respuestas añadiendo detalles en el _prompt_ del almacén de datos (`Data store`).
    
- **Plantilla de ejemplo (`Example`):** Es editable y sirve como una buena base para crear tus propias plantillas.
    
- **Nueva plantilla (`New template`):** Te permite definir tu propio _prompt_ desde cero.
    

#### **Elementos clave del _prompt_**

El _prompt_ de una respuesta de reserva debe incluir contexto para que el modelo genere una respuesta apropiada. Para esto, se usan los siguientes marcadores de posición:

- `$conversation`: Contiene el historial de la conversación, excluyendo la última frase del usuario.
    
- `$last-user-utterance`: La última frase que dijo el usuario.
    
- `$flow-description`: La descripción del flujo en la página de inicio.
    
- `$route-descriptions`: Las descripciones de las intenciones de las rutas activas en la página.
    

**Ejemplo de cómo funcionan los marcadores:**

Un _prompt_ puede incluir: "Eres un agente amigable... Actualmente, puedes $route-descriptions... El usuario preguntó $last-user-utterance".

Cuando el agente procesa esto, los marcadores se llenan con la información contextual:

- `$flow-description` trae la descripción del flujo (ej., "buscar, encontrar y reservar viajes en barcos de buceo").
    
- `$route-descriptions` trae la descripción de las rutas activas (ej., "asistir a los usuarios que buscan una reserva grupal...").
    
- `$conversation` se llena con el diálogo previo.
    
- `$last-user-utterance` inserta la última frase del usuario (ej., "los niños quieren ir a las Maldivas").
    

Con todo este contexto, el agente puede generar una respuesta útil y precisa como: "Lo siento, Alicia. Solo puedo ayudarte con viajes a Costa Rica, las Islas Galápagos y varias ubicaciones en México".

Asegúrate de que las descripciones de tus flujos y rutas sean claras y detalladas, ya que son la principal fuente de contexto para las respuestas generativas de reserva.

---

# Seguridad

### **Configuraciones de seguridad en IA generativa**

Puedes controlar las configuraciones de seguridad para tu agente conversacional en la pestaña de **`Agent Settings`**, en la sección **`Generative AI`**.

#### **1. Frases prohibidas (`Banned phrases`)**

- **Qué son:** Una lista de palabras o frases que están prohibidas para el agente.
    
- **Cómo funcionan:** Si una de estas frases aparece en el _prompt_ del usuario o en la respuesta generada, la generación fallará.
    
- **Tipos de coincidencia:** Puedes elegir entre **coincidencia parcial** o **coincidencia completa**.
    
- **Consideración:** El uso de una lista larga puede aumentar la latencia del agente.
    

#### **2. Filtros de seguridad (`Safety filters`)**

- **Qué son:** Filtros que bloquean contenido en categorías sensibles como lenguaje de odio, contenido peligroso, explícito o acosador.
    
- **Niveles de sensibilidad:** Puedes elegir el nivel de sensibilidad para cada categoría, desde "pocos" hasta "la mayoría" de las respuestas bloqueadas. La configuración se basa en probabilidades, por lo que puede requerir pruebas.
    
- **Comportamiento:** Si una respuesta es bloqueada por los filtros de seguridad, el agente emitirá la respuesta de reserva (`fallback`) que se tenga configurada.
    

---

### **Seguridad de _Prompts_**

- **Propósito:** Esta configuración adicional se aplica a los **Playbooks** y los **Almacenes de datos** para prevenir ataques de inyección de _prompts_ y otras consultas maliciosas.
    

---

### **Respuesta generativa de reserva**

- **Propósito:** Puedes configurar el _prompt_ que usará el agente cuando se active la respuesta generativa de reserva, lo que sirve para controlar las respuestas del agente ante consultas que no coinciden con las intenciones definidas.

