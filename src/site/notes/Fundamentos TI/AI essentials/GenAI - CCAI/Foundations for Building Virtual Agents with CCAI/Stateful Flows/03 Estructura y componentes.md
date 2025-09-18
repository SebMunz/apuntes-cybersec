---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Stateful Flows/03 Estructura y componentes/"}
---

# Índice

[[#Parámetros y Recopilación de Parámetros]]
[[#Rutas y grupos de rutas]]
[[#Eventos]]
[[#Fulfilment]]
[[#Transiciones]]
[[#State Handlers]]

---

Los agentes conversacionales en la plataforma se construyen con una estructura modular que va desde áreas temáticas amplias hasta componentes más específicos. La estructura se organiza de la siguiente manera:

---

### **Flujos (`Flows`)**

Los flujos son las áreas temáticas principales que encapsulan las rutas de conversación. Un agente puede tener uno o varios flujos.

- **Propósito**: Dividen una conversación compleja en temas manejables, como `facturación`, `estado de la orden`, o `resolución de problemas`.
    
- **Default Start Flow**: Todo agente viene con un **flujo de inicio por defecto**, que es suficiente para agentes sencillos. Puedes añadir más flujos según la complejidad de la conversación.
    

---

### **Páginas (`Pages`)**

Una página representa un paso o estado en la conversación dentro de un flujo. Juntas, las páginas de un flujo manejan una conversación completa sobre un tema específico.

- **Propósito**: Un flujo puede contener múltiples páginas para manejar los diferentes pasos de una conversación. Por ejemplo, en el flujo de `pagos`, podrías tener páginas para `recopilar el monto`, `confirmar la intención de pago`, y `mostrar el estado de la transacción`.
    
- **Start Page**: Cada flujo tiene una página de inicio especial, que es la primera página activa al entrar en ese flujo.
    

---

### **Componentes de la Página**

Cada página puede tener tres componentes opcionales que le permiten realizar múltiples funciones.

- **Fulfillments de entrada**: Acciones que se ejecutan al entrar en la página, como saludar al usuario o preestablecer un parámetro.
    
- **Parámetros**: Se usan para capturar y almacenar valores de las entidades que el agente extrae del usuario (ej. la fecha de un viaje). Esto permite usar esa información más adelante en la conversación.
    
- **Manejadores de estado (`State handlers`)**: Definen el comportamiento del agente en respuesta a eventos o condiciones. Se dividen en dos tipos principales de **rutas**, además de otros manejadores:
    
    - **Rutas de intención**: Se activan cuando la expresión del usuario coincide con una intención específica (ej. `pagar la cuenta`).
        
    - **Rutas de condición**: Se activan solo si se cumplen ciertas condiciones (ej. el usuario proporciona una fecha que ya pasó).
        
    - **Otros manejadores**: Incluyen `grupos de rutas` (conjuntos reutilizables de rutas), `manejadores de eventos` (para eventos como fallos de _webhooks_ o cuando el agente no entiende algo), y `almacenes de datos` (para integrar información de sitios web o documentos).
        

---

### **Fulfillments**

Cada uno de los componentes de la página está asociado a un _fulfillment_. Estos son las acciones que ejecuta el agente. Por ejemplo, un _fulfillment_ puede hacer que el agente envíe un mensaje, haga una llamada a un _webhook_ o establezca un parámetro.

---

# Parámetros y Recopilación de Parámetros

Los **parámetros** son una forma de capturar y almacenar datos clave de las expresiones del usuario durante una conversación. A diferencia del texto sin procesar, los parámetros son **datos estructurados** que facilitan la lógica y las respuestas del agente. Cada parámetro tiene un **nombre** y un **tipo de entidad**.

El tipo más común son los **parámetros de sesión**, cuya sintaxis es `$session.params.nombre_del_parametro`.

---

### **Formas de Capturar Parámetros**

Hay dos métodos principales para recopilar parámetros de un usuario:

1. **Mediante el emparejamiento de una intención (`intent`):** Cuando una frase del usuario coincide con una intención que tiene entidades etiquetadas, el agente extrae los valores de esas entidades y los almacena como parámetros.
    
    - **Ejemplo:** Si la intención `pagar-factura` tiene una entidad de fecha, cuando el usuario dice "Quiero pagar mi factura el 3 de noviembre", el agente captura "3 de noviembre" como un parámetro.
        
2. **Preguntando directamente al usuario en una página:** Puedes configurar una página para solicitar un parámetro específico. Cuando el usuario lo proporciona, el agente lo captura.
    
    - **Ejemplo:** En una página configurada para capturar una fecha, el agente pregunta: "¿Qué fecha desea pagar su factura?".
        

---

### **Configuración de la Recopilación de Parámetros**

Para configurar la recopilación de un parámetro en una página, debes seguir varios pasos:

- **Nombre del parámetro:** Un nombre claro y único (ej., `fecha_pago`).
    
- **Tipo de entidad:** El tipo de entidad asociado (ej., `$sys.date` para una fecha).
    
- **Descripción:** Una breve explicación del parámetro.
    
- **Opciones:**
    
    - `Required`: Si la información es obligatoria para continuar la conversación.
        
    - `Is list`: Si el usuario puede proporcionar múltiples valores.
        
    - `Redact in log`: Para ocultar el valor en los registros, útil para información sensible.
        
- **Configuración avanzada:**
    
    - **Mensaje de bienvenida (`Initial prompt fulfillment`):** El mensaje inicial que el agente usa para solicitar el parámetro.
        
    - **Manejadores de re-solicitud (`Reprompt event handlers`):** Manejan los casos en los que la respuesta del usuario no es suficiente y se necesita repetir la pregunta.
        
    - **Ajustes de DTMF:** Permiten la recopilación de información ingresada a través del teclado del teléfono.

---

# Rutas y grupos de rutas

Las **rutas** son un concepto central en los agentes conversacionales, ya que dirigen el flujo de la conversación. Hay dos tipos principales de rutas: las rutas de intención y las rutas de condición.

---

### **Tipos de rutas**

1. **Rutas de intención:** Estas rutas se activan cuando la expresión de un usuario coincide con una **intención** específica. Por ejemplo, si el usuario dice "pagar la factura", se le puede dirigir al flujo de facturación.
    
2. **Rutas de condición:** Estas rutas se activan cuando se cumplen ciertas **condiciones**, como el valor de un parámetro de sesión. Por ejemplo, si el parámetro `is_authenticated` no es verdadero, la conversación puede terminar.
    

Un mismo camino puede tener **ambos tipos de rutas**. Para que este se active, tanto la intención como la condición deben cumplirse.

---

### **Configurando una ruta**

Cuando configuras una ruta, puedes incluir lo siguiente:

- **Descripción**: Una breve explicación de lo que hace la ruta.
    
- **Intención**: La intención que debe coincidir para que la ruta se active.
    
- **Condiciones**: Expresiones lógicas que deben ser verdaderas.
    
    - **Condición siempre verdadera**: Para que una ruta se active siempre, puedes establecer la condición como `true`.
        
    - **Parámetros completos**: Para que la ruta se active solo cuando todos los parámetros obligatorios de la página han sido capturados, puedes usar la condición `$page.params = final`.
        
- **Fulfillment**: Las acciones que el agente debe realizar, como dar una respuesta o ejecutar un _webhook_.
    
- **Transición**: La página o el flujo al que se debe dirigir la conversación.
    

---

### **Grupos de rutas (`Route Groups`)**

Un **grupo de rutas** es una colección de rutas que se pueden reutilizar en varias páginas. Esto es útil para manejar temas que pueden surgir en diferentes puntos de la conversación.

#### **Cómo usarlos**

1. **Crear el grupo**: Define el grupo de rutas y especifica si se aplica a un flujo en particular o a todos los flujos.
    
2. **Añadir rutas**: Dentro del grupo, agrega las rutas que correspondan (por ejemplo, rutas relacionadas con el balance de la cuenta).
    
3. **Aplicar a las páginas**: En una página, añade el grupo de rutas a través de la opción `Add state handler` > `Route Groups`.
    

#### **Mejores prácticas**

- **Comprende el alcance**: Asegúrate de que las rutas dentro de un grupo son apropiadas para todas las páginas en las que se usarán.
    
- **Prioridad**: Recuerda que las rutas a nivel de página tienen prioridad sobre las rutas a nivel de flujo.
    
- **Diseño general**: Usa _fulfillments_ y transiciones que tengan sentido en múltiples contextos.
    
- **Reutilización**: Crea grupos de rutas para parámetros y transiciones comunes.

---

# Eventos

### **Eventos en agentes conversacionales**

Los **eventos** se activan cuando algo ocurre durante la conversación o fuera de ella. Son una forma de manejar situaciones específicas, como errores o falta de respuesta del usuario.

#### **Tipos de eventos**

- **Eventos integrados:** Son eventos predefinidos que manejan situaciones comunes.
    
    - **No-match:** Se activa cuando la frase del usuario no coincide con ninguna intención del agente.
        
    - **No-input:** Se activa en conversaciones de voz cuando el usuario no responde después de un _prompt_.
        
    - **Error de _webhook_**: Se activa cuando hay un error en una llamada a un _webhook_.
        
- **Eventos personalizados:** Permiten tener un control preciso sobre cómo activar el agente cuando algo sucede fuera de la conversación, como una acción del usuario en una interfaz externa o un cambio en el inventario.
    

---

### **Manejadores de eventos (`Event handlers`)**

Para que un evento tenga efecto, se necesita un **manejador de eventos**. Estos se pueden añadir en diferentes lugares:

- **En una página:** Como uno de los manejadores de estado, para responder a un evento en un paso específico de la conversación.
    
- **En los parámetros de una página:** Dentro de la sección de "Reprompt event handlers" (manejadores de eventos de re-solicitud), para manejar situaciones en las que el agente necesita volver a pedir un parámetro.
    

#### **Mejores prácticas para no-match y no-input**

Es crucial manejar los eventos de "no-match" y "no-input" para mantener la fluidez de la conversación, especialmente en llamadas de voz.

1. **Asegura la cobertura:** Siempre que el usuario pueda dar una respuesta, debe haber un manejador para los eventos "no-match" y "no-input".
    
2. **Respuestas específicas:** En lugar de respuestas genéricas como "Lo siento, no entendí", usa _prompts_ más específicos que le digan al usuario qué información debe proporcionar, como "Lo siento, ¿cuál es el número de teléfono que está solucionando?".
    
3. **Diferencia por intento:** Varía la respuesta según el número de veces que se activa el evento:
    
    - **Primer intento:** Un mensaje breve que simplemente repite la pregunta.
        
    - **Segundo intento:** Un mensaje más elaborado que indique que el agente aún tiene problemas para entender.
        
    - **Tercer intento:** Ofrece transferir al usuario a un agente humano, ya que el problema persiste.
        

Esta lógica se puede aplicar de manera similar para los eventos "no-input" en las conversaciones de voz, donde el primer _prompt_ debe ser un simple recordatorio de la pregunta, y los siguientes deben escalarse hasta la transferencia a un agente.

---

# Fulfilment

Los **fulfillments** son las acciones que tu agente realiza para interactuar con el usuario o con sistemas externos. Se pueden agregar en los **fulfillments de entrada** de una página, los **parámetros de página** y los **manejadores de estado**.

Puedes configurar seis tipos de acciones dentro de un _fulfillment_:

1. **Parámetros preestablecidos (`Parameter presets`):** Permiten añadir o modificar el valor de los parámetros de la sesión. Es una herramienta poderosa para controlar el flujo de la conversación, como asignar el valor `true` a un parámetro cuando se cumple una condición.
    
2. **Generadores (`Generators`):** Una función que permite llamar a un LLM (modelo de lenguaje grande) para que genere una respuesta.
    
3. **Respuestas del agente (`Agent responses`):** La funcionalidad más importante, que permite al agente comunicarse con el usuario. Puedes agregar varios tipos de respuestas.
    
    - **Texto:** Para proporcionar el contenido que el agente dirá o mostrará. Puedes usar parámetros de sesión dentro del texto para personalizar la respuesta, como `$session.params.nombre_usuario`.
        
    - **Otros tipos de respuesta:** Incluyen audio, cargas útiles personalizadas y más.
        
4. **Ejecutar un _webhook_:** Para llamar a servicios externos o APIs.
    
5. **Configuraciones avanzadas:** Permiten ajustar el comportamiento del agente.
    
6. **Configuraciones de Call Companion:** No se cubren en esta transcripción.
    

El elemento más crucial es la capacidad de proporcionar **respuestas de texto**. Con esta función, el agente puede hacer preguntas (`¿Qué fecha saldrá para su viaje?`) o dar mensajes de confirmación, usando los valores de los parámetros para que la conversación sea más natural y personal.

---

# Transiciones

Las **transiciones** te permiten dirigir el flujo de la conversación, moviéndote entre diferentes páginas o flujos. Están asociadas a los manejadores de estado, como rutas y eventos.

#### **Funcionalidades clave de las transiciones**

- **Transición a otro flujo o página:** Puedes mover al usuario de un flujo (ej., `facturación`) a otro (ej., `internacional`).
    
- **Volver a un flujo anterior (`End Flow`):** Cuando terminas un flujo (ej., `internacional`), la opción `End Flow` te devuelve automáticamente al flujo anterior que todavía estaba activo (ej., `facturación`), retomando la conversación exactamente en el punto donde la dejaste.
    
- **Finalizar la sesión (`End Session`):** Esta opción termina por completo la conversación, ya sea un chat o una llamada telefónica.
    
- **Volver a la página anterior (`Previous page`):** Te permite regresar a la página en la que estabas, manteniendo el mismo estado.
    
- **Reiniciar la página actual (`Current page`):** Te lleva de nuevo al comienzo de la página en la que te encuentras, ejecutando su _fulfillment_ de entrada.

---

# State Handlers

Los **manejadores de estado** (`state handlers`) son la forma en que los agentes conversacionales controlan el flujo del diálogo, ya sea creando una respuesta para el usuario o haciendo una transición a otra página o flujo. Hay cuatro tipos: rutas, grupos de rutas, eventos y almacenes de datos.

El procesamiento de un manejador de estado sigue tres pasos principales:

1. **Ámbito (`scope`):** El manejador debe estar en el ámbito correcto para poder ser considerado.
    
2. **Orden:** Los manejadores que están en el ámbito se evalúan en un orden específico para ver si sus requisitos se cumplen.
    
3. **Llamada:** Si los requisitos se cumplen, el manejador se "llama" y se ejecutan sus acciones y transiciones asociadas.
    

---

### **Ámbito de los manejadores**

El ámbito de un manejador determina si puede ser procesado en un momento dado.

- **Rutas y grupos de rutas:** Todas las rutas y grupos de rutas adjuntos a la página actual están en el ámbito. Las rutas de intención adjuntas a la página de inicio del flujo también lo están.
    
- **Manejadores de eventos:** El ámbito depende de si se está recopilando un parámetro requerido.
    
    - **Recopilando un parámetro requerido:** Los manejadores de eventos de ese parámetro están en el ámbito.
        
    - **No recopilando un parámetro:** Los manejadores de eventos en la página actual y en la página de inicio del flujo están en el ámbito.
        

---

### **Orden de evaluación**

El orden en que los manejadores se evalúan es crucial y depende de la situación.

#### **Transición a un flujo**

Al hacer una transición a un flujo, siempre vas a la página de inicio (`Start Page`), a menos que estés regresando de un flujo que finalizó.

#### **Transición a una página**

El orden de evaluación en una página es:

1. **Fulfillment de entrada**: Primero se ejecuta el _fulfillment_ de entrada de la página.
    
2. **Rutas de condición**: Se evalúan las rutas de condición en la página en el orden en que están listadas. Las rutas de intención se ignoran en este punto, excepto si acabas de hacer una transición de un flujo a la página de inicio.
    
3. **Grupos de rutas**: Se evalúan los grupos de rutas adjuntos a la página.
    
4. **Parámetros requeridos**: Si hay parámetros obligatorios sin valor, se pasa al _prompt_ inicial del primer parámetro.
    

Si una ruta te lleva a una nueva página, el proceso de la página actual se detiene.

#### **Inicio de un turno**

Este es el caso más complejo, ya que el orden depende de dos factores: si se está recopilando un parámetro obligatorio y si hubo un evento de "no-match" o "no-input" en el turno anterior.

- **Si hay un parámetro obligatorio sin valor:**
    
    - Si hubo un "no-match" o "no-input", se evalúan los **manejadores de eventos** de ese parámetro.
        
    - Si no, se evalúan las **rutas de intención** de la página, seguidas de las **rutas de condición**, los **grupos de rutas** de la página y los del flujo.
        
- **Si no hay parámetros obligatorios sin valor:**
    
    - Si hubo un "no-match" o "no-input", se evalúan los **manejadores de eventos** en la página actual, y si no hay uno aplicable, se evalúan los de la página de inicio del flujo.
        
    - Si no, se evalúan las **rutas de intención** de la página, seguidas de las **rutas de condición** y los **grupos de rutas** de la página.

---