---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Introduction to CES and Conversational Agents/03 Diseño de Conversaciones/"}
---

# Índice

[[#Introducción al diseño de conversaciones (CXD)]]
[[#Fundamentos del Diseño de Conversaciones (CXD)]]
[[#Cómo Crear una persona para un agente conversacional]]
[[#Escritura de guiones de conversación]]
[[#Mejorando turnos]]
[[#Guías para mantener conversaciones]]
[[#Transferencia a agentes humanos (escalation)]]
[[#Manejo de rechazos de solicitudes del cliente]]

---

# Introducción al diseño de conversaciones (CXD)

El diseño de conversaciones para agentes virtuales busca crear experiencias de chat que se sientan humanas. Aunque esta presentación se centra en chat, los principios se aplican también a voz.

- **Modelos de lenguaje grandes (LLMs):** Son "generalistas" entrenados en un vasto corpus de texto. Permiten conversaciones divergentes y creativas.
    - **Ventaja:** Pueden manejar conversaciones abiertas y fuera de lo común.
    - **Desventaja:** Pueden ser poco útiles para resolver problemas específicos, frustrando al usuario con demasiadas opciones o información irrelevante.

- **Diseño determinista:** Se basa en intenciones predefinidas y rutas fijas.
    - **Ventaja:** Resuelve problemas de manera directa y predecible.
    - **Desventaja:** Se siente impersonal y robótico. No puede manejar entradas inesperadas del usuario, lo que puede llevar a fallos.
        

#### **Pensamiento divergente vs. convergente**

- **Pensamiento divergente:** Busca múltiples soluciones creativas para un problema. Es bueno para conversaciones abiertas o para aprender.
- **Pensamiento convergente:** Se enfoca en una única solución bien definida. Es ideal para resolver un problema específico.

En el diseño de conversaciones, se debe ser **divergente** al explorar opciones, pero **convergente** al ayudar a los usuarios a resolver un problema o realizar una transacción.
- Los **LLMs** son perfectos para el pensamiento divergente.
- Los agentes virtuales tradicionales (deterministas) son ideales para el pensamiento convergente.

#### **El principio del "Pavo Real"**

Este principio es una guía para el diseño de agentes:

- **La cabeza del pavo real (20% de las rutas):** Representa los casos de uso principales (el 80% de los usuarios). Son rutas comunes y críticas (ej. reportar una tarjeta robada).
    - Debes diseñar estas rutas de forma **determinista**, con _prompts_ que recojan y validen datos estructurados. Esto evita la frustración del usuario.
        
- **La cola del pavo real (80% de las rutas):** Incluye desvíos comunes, rutas menos comunes y casos excepcionales (el 20% de los usuarios).
    - Deja que los **LLMs** se encarguen de esta parte. Por ejemplo, la función de `generative fallback` permite al agente responder cuando la entrada del usuario no coincide con una intención, evitando un fallo en la conversación.


#### **Consideraciones de diseño**

Antes de usar LLMs en tu diseño, ten en cuenta:

- **Regulaciones:** Industrias como la financiera, de salud o de comercio minorista están fuertemente reguladas, lo que limita la flexibilidad del diseño.
- **Seguridad:** Las aplicaciones basadas en LLMs son vulnerables a la "inyección de _prompt_", por lo que se debe tener cuidado con la información sensible.
- **Control de calidad:** Cualquier respuesta no determinista requiere una revisión exhaustiva para garantizar que cumple con los protocolos de calidad.

---

#  Fundamentos del Diseño de Conversaciones (CXD)

#### **Estrategia y mejores prácticas**

- El diseño de conversaciones (CXD) crea interfaces naturales e intuitivas.
- Un diseñador debe anticipar las necesidades del usuario y colaborar con el negocio y los desarrolladores.
- **Objetivo:** Dar la información correcta a la persona adecuada, de la forma y en el momento oportuno.
- **Mejores prácticas:**
    - Maximizar la usabilidad.
    - Convertir patrones rígidos en conversaciones inteligentes.
    - Soportar múltiples plataformas, idiomas y dialectos.

---

### **Proceso de diseño en 3 fases**

#### **1. Recopilar requisitos de diseño**

- **Definir usuarios:** ¿Quiénes son? ¿Cuáles son sus metas y contexto? Acomoda a todos, incluyendo a personas con habilidades diversas.
- **Evaluar limitaciones técnicas:**
    - **Del sistema:** ¿Qué es posible con la tecnología actual (ej. Dialogflow)? ¿Cómo manejar la identificación del usuario y sesiones simultáneas?
    - **De los datos:** Evaluar el formato, la calidad, la disponibilidad y la necesidad de reformatear el contenido (ej. para TTS).
- **Identificar casos de uso:** Priorizar casos factibles con alto impacto (que beneficien a muchos usuarios).
- **Crear una persona (voz) para el agente:** Diseñar un personaje que represente la marca.

#### **2. Diseñar a alto nivel**

- Si eres nuevo, empieza por aprender sobre la experiencia conversacional.
- Escribir diálogos de ejemplo y diagramar flujos a alto nivel.
- **Importante:** Diseña la conversación hablada primero (como si fuera cara a cara). El diseño de la pantalla viene después, para no perder el hilo.

#### **3. Diseñar en detalle**

- **Pruebas e iteración:** Probar los diseños y cubrir el "long tail" (caminos de conversación poco comunes).
- **Manejo de errores:** Diseñar cómo manejar errores y escenarios inesperados.
- **Escalar el diseño:** Preparar el diseño para un despliegue más amplio.

---

### **Recursos útiles (assets)**

- **Documentos de descubrimiento:** Explican cómo se manejan las interacciones actualmente. Ayudan a definir los objetivos del proyecto.
- **Hoja de diseño de persona:** Contiene la descripción del agente virtual, sus rasgos de personalidad y marca.
- **Guiones de conversación:** Muestran el lenguaje de las interacciones entre el agente y el cliente. Útiles para diseñar y evaluar.
- **Diagrama de diseño conversacional:** Diagramas de flujo o representaciones visuales. Muestran la arquitectura de la solución, las llamadas a API y los posibles caminos del usuario.
- **Taxonomía de intenciones:** Clasificación estructurada de las intenciones de los usuarios.
- **Especificaciones de parámetros/entidades:** Detallan el formato de los parámetros, nombres y requisitos de API. Incluye ejemplos de `JSON`.

---
# Cómo Crear una persona para un agente conversacional

Una **persona** es un personaje que se percibe a través del lenguaje de una aplicación. Al crear una, el objetivo es hacer que el usuario sienta que interactúa con un individuo, no con un _bot_. Esto crea confianza y establece un modelo mental de lo que el agente puede o no hacer.

---

### **Áreas clave para diseñar una persona**

El diseño de una persona debe estar en la intersección de tres áreas:
1. **Mensaje de la marca:** Debe alinearse con las características existentes de la marca para evitar confusión. Por ejemplo, si Google es útil y empático, sus agentes deberían reflejarlo.
2. **Objetivo del negocio:** Debe ayudar a cumplir una meta específica.
3. **Audiencia objetivo:** Debe conectar con las características de los usuarios.

#### **Rasgos personales**

- **Identidad:** Considera la edad, género (incluso no-binario), nombre, imagen y antecedentes. Esto informa el tono y la voz del agente.
- **Rasgos de carácter:** Son la personalidad del agente. Es recomendable que sea accesible, amigable, confiable y consistente. La consistencia es clave para generar confianza.

#### **Componentes de la conversación**

- **Apertura:** El estilo del saludo (formal o informal) define el tono. El uso de "nosotros" en lugar de "yo" puede posicionar al agente como parte de la empresa.
- **Manejo de errores:** Evita decir "lo siento" en exceso. Los marcadores de discurso como "Hmm" pueden hacerlo más humano. Prioriza dar instrucciones claras y soluciones.
- **Conversación casual (_Small Talk_):** Debe ser breve y solo en respuesta al cliente. Usa un lenguaje simple como "gracias" o "está bien". Los _emojis_ pueden ser útiles si se alinean con la marca.
- **Cierre:** Debe ser fluido. El agente debe despedirse o hacer una transición suave a un agente humano, si es necesario.

---

### **Principios guía para el diseño**

- **El cliente es el centro:** No permitas que la persona tome el protagonismo. En lugar de decir "Hice tu reserva", di "Tu reserva está lista".
- **Confianza y brevedad:** Comunica con confianza. Evita respuestas largas y complicadas; el tiempo del cliente es valioso. Ofrece solo la información esencial.
- **Minimiza la distancia social:** Usa un lenguaje natural y cercano. Evita palabras como "por favor" o "le ruego" en exceso. Usa frases como "¿De qué se trata la llamada?" en lugar de "¿Podría decirme la razón de su llamada?".
- **Evita la jerga:** Habla como una persona común. No uses términos técnicos como "intención" o "entidad".
- **Sé proactivo y servicial:** En lugar de solo rechazar una solicitud, ofrece alternativas. Por ejemplo, si no hay conductores disponibles, pregunta "¿Quieres que vuelva a buscar en 2 o 3 minutos?".
- **No te disculpes por los errores:** No llames la atención sobre los problemas. Di, por ejemplo, "¿Aún no lo entiendo? Intenta decir la fecha una vez más".

---
# Escritura de guiones de conversación

El objetivo es escribir un guion para un _bot_ de "dirección" que solo detecta la intención principal (Head Intent Detection o HID).

#### **El proceso de escritura: Construir una casa** 🏠

1. **Cimientos (La Fundación):** Crea la estructura básica de la conversación.
2. **Plomería (La Estructura):** Añade la estructura para cada caso de uso.
3. **Paredes (Los Refuerzos):** Agrega preguntas secundarias e intenciones para redirigir la conversación cuando se sale del guion.
4. **Pintura (Los Detalles):** Elige las palabras específicas para que el guion refleje la persona del agente virtual.

---

### **La estructura de la conversación en servicio al cliente**

Las conversaciones siguen un esquema natural de tres fases:

1. **Secuencia de Apertura:**
    - Un mensaje de bienvenida corto (menos de 5 segundos).
    - Incluye 3 acciones (que pueden estar implícitas):
        - **Saludo:** "Hola, bienvenido a la compañía".
        - **Identificación:** "Soy Joe, de la compañía A". Para agentes virtuales, es recomendable que se identifiquen como tal.
        - **Oferta de servicio:** "En qué puedo ayudarte hoy?".
    - El objetivo es animar al cliente a exponer su problema.

2. **Secuencia Principal:**
    - **Solicitud de servicio:** El cliente explica su problema (aquí se detecta la intención principal o Head Intent).
    - **Serie interrogativa:** El agente hace preguntas para obtener más información. (Esto se omite en casos simples de FAQ).
    - **Respuesta de servicio:** El agente ofrece la solución.
    - **Acción de aceptación:** El cliente confirma que la solución es la correcta. Es un paso crucial.

3. **Secuencia de Cierre:**
    - Agradecimiento y despedida. Opcionalmente, se puede preguntar si el cliente tiene otro problema.

---

### **Manejo de situaciones inesperadas**

Después del saludo, el cliente puede no dar su intención principal de inmediato. Hay dos escenarios:

- **Pre-expansión:** El cliente introduce el tema sin hacer una solicitud completa (ej. "Tengo una pregunta").
    - **Cómo responder:** Reacciones cortas y genéricas (ej. "Claro", "Adelante"). El objetivo es mostrar que estás escuchando y darle espacio al cliente para que se explique. Evita preguntar "qué necesitas" inmediatamente, ya que podría sonar robótico y hacer sentir al cliente que se está comunicando mal.
        
- **Desambiguación:** El cliente hace una solicitud, pero no es clara o es muy vaga (ej. "Conexión a internet").
    - **Cómo responder:** Haz preguntas más largas y específicas para aclarar el problema. El objetivo es obtener la información necesaria para continuar con la conversación.

![](https://i.imgur.com/4wtOD29.png)

---

# Mejorando turnos

Para que una conversación con un agente conversacional se sienta natural y fluida, los diseñadores suelen usar dos estrategias principales: **reconocimientos** y **preguntas de opción cerrada**.

### **Reconocimientos (Acknowledgments)**

Los reconocimientos son una forma de demostrar al usuario que se le ha entendido. Sin embargo, usarlos en exceso puede hacer que el agente suene robótico.

- **¿Cuándo usarlos?** 🗣️
    - Úsalos de forma estratégica, especialmente durante las transiciones importantes de la conversación, como después de que el usuario expresa su intención principal.
    - Evita usarlos después de cada respuesta. Un uso excesivo interrumpe el flujo y puede parecer antinatural.
- **Ejemplo:**
    - Usuario: "Quiero añadir un servicio nuevo a mi plan."
    - Agente: "**Okay**, ¿qué servicio estás intentando añadir?"
    - En este caso, el agente usa un reconocimiento ("Okay") para confirmar que entendió la solicitud del usuario, pero no usa más a lo largo de la conversación para no sonar repetitivo.

---

### **Preguntas de opción cerrada**

Son preguntas que ofrecen un conjunto limitado de opciones (ej. "¿Quieres A, B o C?"). Su objetivo es facilitar el flujo de la conversación al guiar al usuario.

- **Desafío:** A veces, los usuarios responden con algo que no está en las opciones, como un simple "sí" o "no", lo que puede causar un error en el sistema.
- **Mejores prácticas y soluciones:**
    1. **Añade guardarraíles:** Configura **intenciones para "sí", "no" y "no sé"**. Si el usuario las activa, el agente debe reformular la pregunta sin culpar al usuario, como si la respuesta fuera apropiada. Por ejemplo, "Entiendo. ¿Entonces, quieres A, B o C?".
    2. **Usa estructuras contrastantes:** Para dejar claro que el usuario debe elegir, utiliza técnicas de escritura como:
        - **"O... o..."**: "¿Quieres **activar o mejorar** tu dispositivo?"
        - **Ordinales**: "La **primera** opción es... y la **segunda** es..."
        - **Numerales**: "Tienes **dos** opciones: ..."
            
        - **"Cuál" + sustantivo**: "¿**Qué método** prefieres: en línea o por la app?"

- **Consejos adicionales:**
    - Añade una pregunta alternativa al final del _prompt_. Por ejemplo, "Te puedo ayudar con activaciones o mejoras. ¿Qué opción te gustaría?"
    - Anticipa las opciones declarando el número de ellas. Por ejemplo, "Tienes **dos** opciones...".
    - Permite respuestas con números ordinales ("la primera opción").

---

# Guías para mantener conversaciones

Un guion conversacional no siempre va a ir por la ruta que se planeó. Por eso, hay que diseñar "guardarraíles" para guiar la conversación de vuelta al camino correcto. Esto se conoce como **reparación conversacional** (`conversation repair`).

La reparación es cualquier intento de corregir malentendidos o errores para que la conversación fluya sin problemas.

### **Tipos de reparación conversacional**

Existen varios tipos de reparación, pero en el contexto de un _bot_ de conversación, se pueden agrupar en dos categorías principales.

#### **1. Reparación de clase abierta (`Open-class repair`)**

Esta técnica solo indica que hubo un malentendido, sin especificar cuál fue. Es una forma genérica de pedirle al usuario que repita o aclare su mensaje. Es útil cuando el agente no entendió nada de lo que dijo el usuario.
- **Ejemplos:**
    - "¿Perdón?"
    - "¿Qué fue eso?"
    - "¿Podrías repetir eso?"

#### **2. Reparación con preámbulo**

Este tipo de reparación es más específica. Usa una frase introductoria (un preámbulo) para indicar qué parte del mensaje necesita aclaración. Hay dos formas principales de hacerlo:

- **Repetición y pregunta:** El agente repite la parte del mensaje que no entendió y pide más información. Esto es muy directo y útil cuando la confusión es sobre una palabra o dato específico.
    - **Ejemplo:**
        - Usuario: "Quiero cambiar mi número de teléfono."
        - Agente: "¿Qué quieres decir con **número de teléfono**?"

- **Comprobación de entendimiento:** El agente parafrasea lo que el usuario dijo para confirmar si lo entendió correctamente. Esto demuestra que el agente está prestando atención y es una forma más avanzada de reparación.
    - **Ejemplo:**
        - Usuario: "Tengo una pregunta sobre las opciones de datos celulares... el _roaming_."
        - Agente: "**¿Quieres decir** si el _roaming_ de datos está encendido o apagado?"

---

### **Manejo de pausas largas**

Aunque la transcripción no lo cubre explícitamente en la sección final, la habilidad para manejar pausas es un componente clave de la reparación conversacional. Si un usuario se queda en silencio, un agente bien diseñado no asumirá un error de inmediato. En cambio, puede usar un _prompt_ o una pregunta de clase abierta para reiniciar la conversación, como "¿Todavía estás ahí?" o simplemente esperar unos segundos para ver si el usuario retoma la conversación. La forma en que se maneja el silencio puede ser tan importante como la forma en que se maneja el lenguaje.

---

# Transferencia a agentes humanos (escalation)

La **transferencia** (`escalation` o `handover`) ocurre cuando un agente virtual no puede resolver la consulta de un cliente. Puede ser parte del diseño esperado o el resultado de un fallo.

#### **Tres categorías principales de transferencia**

1. **Temprana en la interacción:** El cliente pide hablar con un agente humano desde el principio.
    - **Estrategia:** El agente virtual debe reconocer la solicitud del cliente para evitar frustración. Se puede aprovechar esta oportunidad para recolectar información relevante que ayude al agente humano (ej. la intención principal).
    - **Ejemplo de _prompt_:** "Claro. Mientras te conecto, ¿puedes contarme un poco más sobre tu consulta?"

2. **Por diseño:** La consulta del cliente requiere, por naturaleza, la asistencia de un agente humano (ej. consultas muy complejas).
    - **Estrategia:** Informa al cliente que será transferido. Guíalo para que se prepare (ej. que tenga a mano su número de cuenta). Esto asegura una transición fluida.
    - **Ejemplo de _prompt_:** "Entendido. Un momento mientras te conecto con un experto para atender tu solicitud."

3. **Por limitaciones:** El agente virtual no puede satisfacer la solicitud debido a fallos o limitaciones de diseño. Esta es una situación de "fallo elegante" (`fail gracefully`).
    - **Tipos comunes para el chat:**
        - **Falta de coincidencia (`No-match`):** Ocurre cuando el usuario no proporciona la información requerida y el agente no puede identificar su intención. La mejor práctica es transferir al tercer intento fallido de coincidencia, a menos que las reglas de negocio indiquen lo contrario.
        - **Fallo en la confirmación:** Cuando el agente solicita al usuario que confirme si la información que se recolectó es correcta y el usuario responde "no". En este punto, el agente puede intentar de nuevo o transferir al cliente. La transferencia es recomendable si los intentos adicionales no son deseables.

#### **Consejos clave para la transferencia**

- **No ignores al usuario:** Siempre reconoce su solicitud de hablar con un humano para no generar una impresión negativa.
- **Prepara al cliente:** Si es posible, infórmale sobre el tiempo de espera y qué información debe tener lista.
- **Define una plantilla:** Crea un guion básico para la transferencia donde le informas al usuario que será transferido.

---

#  Manejo de rechazos de solicitudes del cliente

A veces, el agente virtual no puede cumplir la solicitud del cliente. En estos casos, es crucial saber cómo negarla de forma elegante.

#### **Dos tipos de rechazo**

1. **Rechazo sin alternativa:** Ocurre cuando no hay ninguna solución posible para el cliente.
    - **Estructura ideal:**
        - **1. Frase suavizante:** "Desafortunadamente..." o "Lo siento, pero...".
        - **2. Explicación:** "ya que se encuentra fuera del plazo...".
        - **3. Rechazo directo:** "...no hay nada que podamos hacer...".
    - **Ejemplo:** El cliente quiere cambiar su teléfono, pero se le pasó el tiempo. El agente responde con una estructura similar a la descrita.

2. **Rechazo con alternativa:** Ocurre cuando no se puede cumplir la solicitud original, pero sí hay otras opciones.
    - **Estructura ideal:**
        - **1. Frase suavizante:** "Sí" o "Claro".
        - **2. Ofrece la alternativa:** "Tenemos vuelos a las 9:40 y a las 10:40".
        - **3. Explicación (si es necesario):** Se da solo si el cliente insiste en el motivo por el cual no se puede cumplir la solicitud original.
    - **Ejemplo:** El cliente quiere un vuelo a las 10:00 a.m. El agente le ofrece otras opciones cercanas y solo explica por qué no está disponible el de las 10:00 a.m. si el cliente pregunta.
#### **Reglas generales para el diseño de respuestas**

Al escribir el guion, debes tener en cuenta estos puntos para que la respuesta suene humana:

- **Si hay una solución:**
    - Comienza con una palabra que suavice la respuesta, como "Sí", "Claro", "Ok" o "Bueno".
    - Inmediatamente, presenta la alternativa.
- **Si no hay una solución:**
    - Usa una frase suavizante como "Desafortunadamente" o "Lo siento, pero".
    - Da una explicación del porqué del rechazo.
    - Finalmente, niega la solicitud.

---

### **Cómo aplicarlo a tu guion**

Cuando crees tu plantilla de guion conversacional, asegúrate de incluir una sección de "respuesta de servicio" que contemple los rechazos. En esta sección, el usuario debe tener la oportunidad de "aceptar" el resultado, incluso si es negativo.

**Ejemplo de guion:**

- **Agente Virtual:** "Hola, bienvenido a Viajes Mundo. ¿En qué puedo ayudarte?"
- **Cliente:** "Quiero comprar un boleto de avión a Roma."
- **Agente Virtual:** "Lo siento, pero Viajes Mundo no vende boletos para Roma. ¿Te gustaría buscar un destino diferente?"
- **Cliente:** "No, gracias. Es el único destino que me interesa."
- **Agente Virtual:** "De acuerdo. Te deseo un excelente día."

---

