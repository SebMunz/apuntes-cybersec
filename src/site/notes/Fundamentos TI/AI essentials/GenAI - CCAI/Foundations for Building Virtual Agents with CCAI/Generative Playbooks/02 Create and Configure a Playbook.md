---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Generative Playbooks/02 Create and Configure a Playbook/"}
---

# Índice

[[#Cómo crear un Playbook en Conversational Agents]]
[[#Configuración de Playbooks Objetivos, Instrucciones y Herramientas]]
[[#Tipos de herramientas de Playbook en Conversational Agents]]
[[#La importancia de los ejemplos en los Playbooks]]
[[#Acciones Condicionales]]
[[#Bloques de código (`Code Blocks`) en los Playbooks]]
[[#Configuración de Parámetros en los Playbooks]]
[[#Agentes Híbridos Flujos y Playbooks]]
[[#Errores comunes al crear agentes conversacionales y cómo evitarlos]]

---

# Cómo crear un Playbook

Antes de empezar, debes conocer los componentes clave del flujo de trabajo:

- **Goal (Objetivo):** Una descripción concisa del propósito general del _Playbook_. Ayuda al agente a saber cuándo ha terminado su tarea.
    
- **Instructions (Instrucciones):** Una lista de pasos estructurados que el agente debe seguir.
    
- **Contexto:** Los parámetros de la sesión y los datos del usuario (ej. nombre de perfil, interacciones pasadas) que dan contexto a la conversación.
    
- **Parameters (Parámetros):** Datos que el _Playbook_ necesita para funcionar o que escribirá en la sesión (similar a los argumentos de una función).
    
- **Tools (Herramientas):** Puntos de integración para llamar a **APIs** o **Data Stores** externos y añadir funcionalidades.
    

---

### **El proceso de 4 pasos (es un proceso iterativo)**

#### **1. Crear un nuevo Playbook**

- **Define el objetivo:** Articula claramente el objetivo principal del flujo conversacional.
    
- **Identifica el contexto:** Determina los parámetros de la sesión y los datos de usuario relevantes.
    
- **Esboza los pasos:** Crea un borrador de los pasos clave, acciones y puntos de decisión.
    

#### **2. Editar pasos y objetivos (Crear herramientas y parámetros)**

- **Refina los objetivos:** Asegúrate de que sean **SMART** (específicos, medibles, alcanzables, relevantes y con un tiempo definido).
    
- **Desarrolla los pasos:** Expande el borrador con instrucciones detalladas, definiendo disparadores y respuestas.
    
- **Incorpora el contexto:** Integra los parámetros de contexto en los pasos.
    
- **Crea las herramientas:**
    
    - Define los requisitos de las herramientas (las **APIs** que necesitas).
        
    - Desarrolla las integraciones de las herramientas.
        
    - Prueba que las integraciones funcionen como se espera.
        

#### **3. Crear ejemplos**

- Crea ejemplos de cómo se vería la conversación.
    
- Si creaste herramientas, incluye ejemplos de casos en los que se usen.
    

#### **4. Probar tu Playbook**

- Usa el **simulador** para interactuar con tu agente.
    
- Si una interacción te gusta, puedes guardarla como un **caso de prueba** para futuras pruebas.
    
- Puedes probar desde el principio del proceso (incluso antes de añadir ejemplos) para ver cómo funciona el flujo.
    

Este proceso es **iterativo**. Al probar, es probable que tengas que volver a los pasos anteriores para refinar objetivos, pasos, herramientas, parámetros y ejemplos. Es una mejora continua.

---

# Cómo crear un Playbook en Conversational Agents

Actualmente, hay dos formas de acceder a la consola para crear un agente conversacional:

1. Desde la consola de **Vertex AI Applications**, seleccionando **Conversational Agents** para crear una nueva aplicación.
    
2. Directamente desde la **consola de Conversational Agents**, haciendo clic en **Crear agente**.
    

#### **Opciones de creación de agentes**

Una vez en la consola, tienes tres opciones:

- **Prebuilt agents:** Son agentes pre-configurados para tareas comunes.
    
- **Build your own:** Te da control total para crear una experiencia desde cero. Esta es la opción que elegirás para crear un _Playbook_.
    
- **Create a Q&A agent:** Genera un _bot_ de preguntas y respuestas a partir de una URL que le proporciones.
    

#### **Configuración inicial del agente**

Al elegir "Build your own", debes configurar lo siguiente:

- **Nombre del agente.**
    
- **Ubicación:** Puedes elegir una ubicación global (EE. UU.) para mayor resiliencia o una región específica para reducir la latencia y cumplir con las regulaciones de localización de datos.
    
- **Zona horaria y idioma.**
    

#### **Elegir el tipo de flujo de trabajo**

El agente debe tener un punto de partida para la conversación. Puedes elegir entre:

- **Playbook:** Para casos de uso **generativos** (conversaciones más flexibles y naturales).
    
- **Flow:** Para un camino **determinista** (conversaciones con reglas estrictas).
    

En este caso, eliges **Playbook**.

#### **Creación y gestión de Playbooks**

Una vez que has seleccionado Playbook, puedes empezar a crearlo y a configurar sus componentes clave:

- **Goals (Objetivos):** El propósito general de la conversación.
    
- **Instructions (Instrucciones):** Los pasos que el agente debe seguir.
    
- **Tools (Herramientas):** Las integraciones con servicios externos.
    

Un agente conversacional puede tener más de un _Playbook_. Puedes navegar entre ellos, importarlos o incluso versionarlos para tener diferentes puntos de partida para la conversación.

---

# Configuración de Playbooks: Objetivos, Instrucciones y Herramientas

#### **1. Objetivos (`Goals`)**

Un **objetivo** es la descripción general de lo que el _Playbook_ debe lograr. Es una guía para el LLM.

- **Ejemplo:** "Ayudar a un usuario a reservar una cita o a renovar su licencia de conducir".
    
- Puedes usar **Gemini** para generar objetivos más específicos y funcionales para tu _Playbook_.
    

#### **2. Instrucciones (`Instructions`)**

Las **instrucciones** definen el proceso paso a paso para cumplir el objetivo del _Playbook_.

- **Formato:** Debes usar una lista no ordenada de Markdown (`-`). Puedes anidar pasos para una estructura más compleja.
    
- **Ejemplo de una instrucción:** "Saluda al cliente, dile que puedes ayudarlo con la renovación de su licencia y con la reserva de citas, y pregúntale en qué puedes ayudarlo".
    

#### **3. Llamadas a otros flujos (`Flows`) o _Playbooks_**

Para dirigir la conversación a flujos de trabajo especializados, puedes usar los siguientes parámetros:

- `$playbook:` Se usa para invocar a otro _Playbook_ desde el actual.
    
- `$flow:` Se usa para invocar a un **flujo** tradicional desde el _Playbook_.
    
- **Ejemplo:** En un _Playbook_ de "puerta de entrada", puedes tener una instrucción que diga: "Si el usuario quiere renovar su licencia, invoca `$playbook:renew-license`".
    

#### **4. Herramientas (`Tools`)**

Las **herramientas** son integraciones externas que el _Playbook_ puede llamar para realizar acciones.

- **Uso:** Se invocan en las instrucciones con el parámetro `$Tool`.
    
- **Propósito:** Implementan el patrón de diseño **ReAct** (razonamiento y acción). Permiten que el LLM realice tareas, como buscar información en una base de datos o ejecutar una función de la nube.
    
- **Ejemplo:** `-$Tool:book-appointment` (si `book-appointment` es el nombre de la herramienta).
    

#### **5. Ejemplos**

Los **ejemplos** son demostraciones de cómo debería ser una buena conversación. Sirven para:

- **Aprendizaje en contexto (`in-context learning`):** Ayudan al LLM a entender el comportamiento deseado.
    
- **Definir el flujo:** Te permiten especificar el resultado esperado (`output`) de una herramienta o el comportamiento general del agente.
    

Estos elementos te dan las herramientas para construir un _Playbook_ que no solo razone, sino que también actúe de manera inteligente para resolver las consultas del usuario.

---

# Tipos de herramientas de Playbook en Conversational Agents

Las **herramientas (`Tools`)** son un concepto fundamental en los Playbooks. Permiten a los agentes conversacionales ir más allá de la información que ya tienen, interactuando con sistemas externos. Un Playbook usa una herramienta para combinar datos externos con las capacidades de un LLM.

Hay cuatro tipos principales de herramientas:

#### **1. Herramientas de OpenAPI**

Estas herramientas te permiten conectar tu agente a cualquier API REST externa.

- **Función:** Llaman a _endpoints_ para obtener o enviar datos.
    
- **Configuración:** Se definen usando el esquema **OpenAPI** en formato **YAML** o **JSON**.
    
- **Ejemplo:** Una API para renovar una licencia de conducir. La definición de la herramienta especifica la URL del servidor y los parámetros que se envían y reciben.
    
- **Ventaja:** Permite que los agentes se conecten a casi cualquier servicio en línea.
    

#### **2. Herramientas de funciones (`Functions`)**

Este tipo se utiliza cuando necesitas ejecutar código en el cliente, no a través de una API.

- **Función:** El agente identifica la intención del usuario y extrae los parámetros necesarios, pero la ejecución del código real ocurre en la aplicación del cliente.
    
- **Proceso:**
    
    1. El agente detecta la necesidad de una función.
        
    2. Extrae los parámetros (ej. ciudad y estado para el clima).
        
    3. Llama al código del cliente.
        
    4. El cliente ejecuta la función y devuelve el resultado.
        
    5. El LLM usa la respuesta para generar una respuesta al usuario.
        
- **Ejemplo:** Obtener la temperatura de una ciudad. El agente extrae el nombre de la ciudad y el código del cliente lo procesa para devolver el valor de la temperatura.
    

#### **3. Herramientas de Conectores (`Connectors`)**

Son integraciones pre-construidas por Google que permiten a los agentes interactuar con servicios de terceros populares.

- **Función:** Realizan acciones y reciben datos de servicios como **Salesforce**, **BigQuery**, **Jira**, **PayPal**, y muchos más. La lista crece constantemente.
    
- **Operaciones (CRUD):** Puedes realizar operaciones como **Create**, **Read** (Listar, Obtener), **Update** y **Delete** sobre los objetos de la fuente de datos (ej. tablas en BigQuery, casos en Salesforce).
    
- **Configuración:** Se especifica el nombre, la ubicación del recurso, y opcionalmente los campos de entrada/salida para limitar las operaciones y el tamaño de la respuesta.
    
- **Autenticación:** Las credenciales pueden pasarse a través de parámetros de la sesión para mayor seguridad y flexibilidad.
    

#### **4. Herramientas de Almacenes de Datos (`Data Stores`)**

Permiten al agente usar tus propios datos para responder preguntas, sin necesidad de crear una API.

- **Función:** El agente busca información en los datos de tu empresa (documentos, sitios web, FAQs) para generar una respuesta.
    
- **Configuración:** Se conecta el Playbook a un almacén de datos de **Vertex AI Applications**. Puedes elegir si los datos son estructurados, no estructurados o una URL.
    
- **Personalización:** Puedes ajustar el nivel de confianza y personalizar las respuestas del agente, por ejemplo, incluyendo el nombre de tu empresa en el resumen.

---

# La importancia de los ejemplos en los Playbooks

La ingeniería de _prompts_ es una técnica nueva y sensible. Es fundamental recordar que los **LLMs no siempre son predecibles**. Por eso, no puedes depender solo de las instrucciones. La calidad y cantidad de tus ejemplos de entrenamiento son cruciales para lograr un comportamiento preciso en el agente.

- **¿Qué son los ejemplos?** Los ejemplos son demostraciones paso a paso del flujo ideal de la conversación. Incluyen las condiciones de inicio, lo que ocurre durante la conversación y el estado final.
    
- **¿Por qué son importantes?** Los ejemplos complementan y guían las instrucciones, funcionando como una plantilla clara para el LLM. Esto ayuda a lograr un comportamiento más predecible y una experiencia conversacional más natural.
    
- **Recomendación:** Se sugiere generar al menos **cuatro ejemplos** representativos para cada _Playbook_, cubriendo tanto los caminos felices (`happy paths`) como los caminos con errores (`unhappy paths`).
    

#### **Cómo crear un buen ejemplo**

- **Define el detonante (`usage trigger`):** Especifica cuándo el sistema debe usar el ejemplo durante el entrenamiento.
    
- **Describe el flujo:** En el panel derecho, detalla la conversación, incluyendo los turnos del agente y del usuario, y las llamadas a herramientas.
    
- **Usa el resumen del _Playbook_ (`playbook summary`):** Este campo es útil para pasar contexto entre diferentes _Playbooks_. Por ejemplo, puedes usarlo para pasar el número de una orden a otro _Playbook_.
    
- **Especifica el estado final (`final playbook state`):**
    
    - `OK`: Para la mayoría de los casos de éxito.
        
    - `ESCALATED`: Si el agente debe transferir la llamada.
        
    - `FAILED`: Si el agente no puede completar la tarea.
        
    - `CANCELED`: Si el usuario cancela la tarea a mitad del proceso.
        
- **Muestra las llamadas a herramientas:** En los ejemplos, es vital mostrar dónde se invocan las herramientas y qué parámetros de entrada y salida utilizan. Esto le enseña al LLM a llamar a las herramientas en el momento adecuado y con la información correcta.
    

#### **Consejos adicionales**

- **Copia y pega:** Puedes copiar ejemplos existentes para crear nuevos de forma más rápida.
    
- **Nombres consistentes:** Usa nombres descriptivos para los ejemplos, como "Happy Path - Reserva de hotel".
    
- **Incluye múltiples _Playbooks_:** Añade ejemplos que muestren cómo la conversación pasa de un _Playbook_ a otro para guiar al agente de manera efectiva.

---

# Acciones Condicionales

Las **acciones condicionales** son una configuración opcional en los Playbooks que te dan un control explícito sobre el comportamiento de un agente.

Puedes establecer **disparadores (`triggers`)** y **condiciones** que, al cumplirse, activan una **acción** específica.

---

### **Cómo funcionan las acciones condicionales**

La configuración de una acción condicional se divide en tres pasos:

1. **Definir el disparador (`Trigger`):** Elige el momento en que se activará la lógica condicional.
    
    - **Etapas del ciclo de vida:**
        
        - Inicio del _Playbook_.
            
        - Antes de que el LLM decida su siguiente acción.
            
        - Antes de que el LLM ejecute la siguiente acción.
            
    - **Eventos personalizados:** Por ejemplo, cuando hay un evento específico o no hay entrada del usuario.
        
2. **Establecer las condiciones:** Define los criterios que deben cumplirse para que la acción se ejecute.
    
    - **Ejemplos de condiciones:**
        
        - Un parámetro de sesión o de entrada existe.
            
        - Una acción previa o la siguiente del LLM coincide con un valor.
            
3. **Configurar la acción:** Elige qué debe hacer el agente si se cumplen las condiciones.
    
    - **Tipos de acciones:**
        
        - Dar una respuesta específica al usuario.
            
        - Llamar a una herramienta externa.
            
        - Invocar a otro _Playbook_.
            
        - Anular la siguiente acción del LLM.
            
        - Cambiar la configuración de la voz.
            

---

### **Ejemplo de un caso de uso**

Imagina que quieres que el agente muestre un carrusel con opciones para que el usuario elija su problema.

- **Objetivo:** "Obtener las líneas de suscriptor del usuario e identificar la línea afectada por el problema de conectividad".
    
- **Instrucción del _Playbook_:** "Si hay varios problemas, llama a la herramienta `ConnectivitySelectionCarousel` para mostrar todas las opciones posibles".
    
- **Lógica condicional:**
    
    - **Disparador:** `Before LLM decides next action` (Antes de que el LLM decida su próxima acción).
        
    - **Condición:** El nombre de la última acción (`$last-action.name`) es igual al nombre de la herramienta que quieres verificar, en este caso, `ConnectivitySelectionCarousel`.
        
    - **Acción:** `Respond` (Responder), para mostrarle al usuario el problema que seleccionó en el carrusel.
        

De esta manera, las acciones condicionales te permiten tener un control preciso, garantizando que el agente se comporte de la manera que esperas en situaciones específicas.

---

# Bloques de código (`Code Blocks`) en los Playbooks

Los **bloques de código** son una característica clave que te permite usar código **Python** directamente dentro de un _Playbook_ para tener un mayor control sobre el comportamiento del agente.

Estos bloques le dan a los _Playbooks_ la capacidad de ser más **deterministas**, es decir, de actuar de una manera más predecible, similar a un flujo tradicional.

#### **Componentes de un bloque de código**

Un bloque de código está formado por dos partes principales:

1. **Acciones (`Actions`):**
    
    - Son como las llamadas a herramientas, con un esquema de entrada y salida definido.
        
    - La lógica interna está escrita en Python. El LLM solo ve la entrada y la salida, y no sabe lo que sucede dentro del código. Esto te permite realizar tareas complejas que no se pueden explicar fácilmente en lenguaje natural.
        
2. **Disparadores (`Triggers`):**
    
    - Funcionan de manera similar a los manejadores de eventos en los flujos.
        
    - Te permiten especificar cuándo debe ejecutarse una acción.
        

#### **¿Por qué son importantes?**

Los bloques de código son una forma innovadora de añadir un comportamiento predecible a un agente de IA generativa. Mientras que los flujos conversacionales tradicionales usan IA generativa en contextos y estados predefinidos, los bloques de código te dan la flexibilidad para definir acciones que no serían posibles solo con lenguaje natural, como llamar a otros flujos para salir de la sesión actual y dirigir al usuario hacia un proceso más estructurado.

---

# Tipos de Playbooks: Tarea vs. Rutina

Un agente generativo puede tener varios Playbooks, cada uno diseñado para una tarea específica. Existen dos tipos:

- **Playbooks de Tarea (`Task Playbooks`):**
    
    - Son el tipo original. Se usan para dividir tareas complejas en subtareas más pequeñas y reutilizables.
        
    - Modelan etapas de conversación **compositivas**, donde la comunicación entre etapas se hace a través de **parámetros de entrada y salida**.
        
    - Pueden ser llamados por cualquier otro Playbook (de Tarea o Rutina), pero **no pueden llamar a Playbooks de Rutina**.
        
    - Requieren una **declaración explícita** de parámetros, tanto en el Playbook que los llama como en el propio Playbook de Tarea.
        
- **Playbooks de Rutina (`Routine Playbooks`):**
    
    - Son un tipo nuevo. Se usan para modelar etapas de conversación **secuenciales**, donde cada etapa es completa e independiente.
        
    - Pueden llamar a Playbooks de Tarea para descomponer grandes tareas.
        
    - Pueden hacer una transición a otros Playbooks de Rutina o a flujos (`flows`).
        
    - Manejan los parámetros de forma similar a los flujos, utilizando el **almacenamiento de parámetros de sesión**. Esto significa que heredan automáticamente los parámetros de la sesión de un flujo padre sin necesidad de declararlos explícitamente.
        

---

### **Manejo de Parámetros**

La forma en que se manejan los parámetros es una de las principales diferencias entre ambos tipos de Playbooks.

- **Flujos y Playbooks de Rutina:** Usan un almacenamiento de parámetros de sesión compartido. Los parámetros que se recolectan en un flujo padre están automáticamente disponibles para el Playbook de Rutina. Esta **declaración implícita** simplifica la configuración.
    
- **Playbooks de Tarea:** No tienen acceso al almacenamiento de parámetros de sesión. Los parámetros deben ser **declarados explícitamente** tanto en el Playbook padre como en el Playbook de Tarea hijo para asegurar que los datos críticos estén disponibles.
    

**Recomendación:** Siempre declara explícitamente los parámetros críticos que necesitas en un Playbook de Tarea. El resumen de la conversación generado por el agente no es una forma confiable de hacer que estos parámetros estén disponibles.

---

# Configuración de Parámetros en los Playbooks

Los **parámetros** son una parte esencial de la creación de _Playbooks_ porque permiten que los flujos de trabajo se comuniquen entre sí. Los _Playbooks_ pueden tener dos tipos de parámetros:

- **Parámetros de entrada (`Input Parameters`):** Son valores que se envían desde un flujo hacia el _Playbook_. Esto permite que el _Playbook_ reciba información necesaria para realizar su tarea.
    
- **Parámetros de salida (`Output Parameters`):** Son valores que el _Playbook_ envía de regreso al flujo. Esto permite que el _Playbook_ comparta el resultado de su trabajo, como una confirmación o datos procesados.
    

#### **Proceso de configuración**

1. **Definir los parámetros:** Primero, tienes que definir qué parámetros de entrada y salida usará tu _Playbook_.
    
2. **Usar los parámetros en un ejemplo:** Una vez definidos, debes crear un ejemplo de cómo se usan.
    
    - En el ejemplo de la transcripción, la clave **`moniker`** se usa para pasar un parámetro del flujo, y la clave **`poem_state`** con el valor **`done`** se usa para enviar un estado de vuelta al flujo.
        

Al configurar los parámetros correctamente, aseguras que los _Playbooks_ y los flujos puedan intercambiar información de manera fluida y efectiva.

---

# Agentes Híbridos: Flujos y Playbooks

Un **agente híbrido** combina el comportamiento determinista de los **flujos** (`Flows`) con la flexibilidad de los **Playbooks**. La integración entre ambos es fluida y te permite aprovechar lo mejor de cada uno.

#### **Invocando Flujos desde un Playbook**

Puedes llamar a un flujo dentro de un _Playbook_ siempre que el flujo ya exista.

- **Sintaxis:** Usa la variable `$flow:` seguida del nombre del flujo. Por ejemplo: `-$flow:nombre-del-flujo`.
    
- **Función:** El _Playbook_ puede dirigir la conversación a un flujo específico para una tarea más estructurada.
    
- **Nota:** Si intentas llamar a un flujo que no existe, el agente generará un error.
    

#### **Invocando Playbooks desde un Flujo**

La transición opuesta también es posible. Puedes dirigir la conversación desde un flujo tradicional a un _Playbook_ de manera muy sencilla, seleccionando la opción de _Playbook_ en el menú de transición del flujo.

#### **Diferencia entre Playbooks y Generadores**

Es importante no confundir los _Playbooks_ con los **generadores** (`Generators`) y los **recursos de retorno generativos** (`Generative Fallback`). Estas son características mutuamente excluyentes.

- **Generadores y Retornos:** Son LLMs aplicados a un solo turno de la conversación dentro de un flujo, para completar una respuesta en un contexto específico.
    
- **Playbooks:** Usan un LLM para orquestar **todo el estado de la conversación**, ofreciendo una gestión más completa y flexible. Si usas un _Playbook_, no necesitas generadores, ya que las instrucciones y ejemplos del _Playbook_ cumplen una función similar a un retorno generativo.
    

---

### **Cómo aprender a crear Playbooks**

Una excelente forma de aprender es a través de los **agentes pre-construidos** que Google proporciona.

- **Función:** Estos agentes son ejemplos funcionales que muestran las mejores prácticas y posibles soluciones para tareas comunes.
    
- **Cómo acceder:** En el botón **"Crear agente"** en la consola, puedes seleccionar la opción **"Usar un agente pre-construido"** en lugar de "Construir el tuyo propio".
    
- **Exploración:** Una vez creado, puedes explorar, usar y editar el agente pre-construido de la misma manera que si lo hubieras creado tú mismo.
    
- **Disponibilidad:** Actualmente, los agentes pre-construidos solo están disponibles en inglés.

---

# Errores comunes al crear agentes conversacionales y cómo evitarlos

Al desarrollar agentes conversacionales, es común enfrentarse a varios problemas. Aquí te mostramos los más frecuentes y cómo solucionarlos.

#### **1. Falta de criterios de lanzamiento**

No definir las condiciones para la puesta en marcha (`go-live`) desde el principio puede llevar a retrasos y proyectos fallidos.

- **Solución:** Estandariza los requisitos y criterios de lanzamiento antes de empezar a desarrollar. Por ejemplo, define el porcentaje de precisión de las herramientas, la consistencia de las respuestas, la precisión de la marcación por tonos (DTMF), etc.
    

#### **2. Mala planificación de pruebas**

No tener un plan de pruebas claro y bien definido desde el inicio.

- **Solución:** Si es posible, utiliza el desarrollo guiado por pruebas (`Test Driven Development`). Selecciona casos de uso iniciales de manera estratégica, evitando los más complejos al principio, como los que requieren múltiples transferencias entre _Flows_ y _Playbooks_ o un uso intensivo de bloques de código.
    

#### **3. Querer hacer demasiado, muy pronto**

Intentar construir múltiples casos de uso a la vez, lo que puede sobrecargar el equipo.

- **Solución:** Perfecciona el primer caso de uso y establece un ritmo de trabajo antes de empezar a construir otros casos de uso simultáneamente.
    

#### **4. Configuración y selección de modelo inadecuada**

No usar los modelos recomendados o no mantenerse al día con las mejores prácticas.

- **Solución:** Utiliza los modelos recomendados por la plataforma. Para agentes de voz, ten en cuenta que el _prompting_ es diferente al de los agentes de texto. Sé explícito en el _prompt_, usa pocos ejemplos (ya que añaden latencia), explica cómo pronunciar los números y usa puntuación para lograr un sonido más natural.
    

#### **5. Expectativas poco realistas**

Creer que el agente funcionará perfectamente desde el primer día.

- **Solución:** Considera la mejora de la calidad como un proceso iterativo. Establece una base y luego optimiza el _prompt_. Configura evaluaciones continuas para que se ejecuten varias veces al día y, lo más importante, no te saltes las **pruebas manuales**, especialmente para los agentes de voz.
    

#### **6. Falta de conocimiento y habilidades en el equipo**

Empezar un proyecto sin la capacitación adecuada.

- **Solución:** Antes de iniciar, asegúrate de que el equipo reciba una capacitación completa que cubra la estrategia del producto, la selección de casos de uso, los fundamentos de desarrollo y las mejores prácticas.
    

#### **7. Transferencia de datos inexacta**

No manejar adecuadamente la transferencia de datos entre diferentes tipos de _Playbooks_.

- **Solución:** Para evitar la pérdida de información crítica, como nombres o correos electrónicos, asegúrate de utilizar el **paso explícito de parámetros** siempre que inicies un _Playbook_ de tarea.

---