---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/01 Create a Testing Strategy/"}
---

# Índice
[[#Framework]]
[[#Métodos]]
[[#Implementando una estrategia de pruebas]]
[[#Integración de testeos]]
[[#Testeo end-to-end (E2E)]]

---

Un enfoque sólido de pruebas es fundamental para el desarrollo de un agente conversacional. Este proceso debe centrarse en el recorrido del cliente (`Customer User Journey`, **CUJ**) para garantizar que el _bot_ funcione de manera efectiva antes de cada lanzamiento.

---
# Framework
### **Marco para una estrategia de prueba sólida**

1. **Enfocarse en el recorrido del cliente (CUJ):**
    
    - El desarrollo de _bots_ presenta desafíos por los complejos requisitos de negocio y la gran cantidad de datos y actores involucrados.
        
    - Una estrategia de pruebas robusta, basada en el **CUJ**, permite evaluar sistemáticamente el rendimiento de punta a punta del agente, en lugar de probar solo funcionalidades aisladas.
        
    - El **CUJ** es una representación de la experiencia del cliente al interactuar con el _bot_ para completar una tarea o hacer una pregunta.
        
    - Adoptar un enfoque de **"CUJ primero"** asegura que las funcionalidades principales del recorrido del usuario se verifiquen antes de cada lanzamiento.
        
2. **Crear un catálogo de CUJ:**
    
    - **Establece un catálogo finito:** Define una lista explícita de escenarios del **CUJ** y haz que todos los actores estén de acuerdo con ellos. Esto actúa como un "contrato" entre los equipos de desarrollo y control de calidad (`QA`), haciendo que las pruebas sean **reproducibles** y **deterministas**.
        
    - **Prioriza los CUJ:** Prioriza los escenarios según las necesidades de negocio, el volumen de tráfico en producción y la complejidad. Priorizar por tráfico es lo más importante, ya que asegura que los **CUJ** más comunes funcionen bien.
        
    - **Genera reportes:** El equipo de `QA` debe generar reportes sobre los **CUJ** probados, destacando los que tuvieron éxito y los que fallaron. Documentar los fallos es crucial para que el equipo de desarrollo pueda reproducirlos y solucionarlos.
        
3. **Matriz de Trazabilidad de Requerimientos (RTM):**
    
    - La **RTM** es un mapa que relaciona los pasos del **CUJ** con los casos de prueba.
        
    - Proporciona una visión de la cobertura de las pruebas, actuando como una lista de verificación antes de cada lanzamiento.
        
    - Asegura que la cobertura de las pruebas se alinee con las necesidades reales del usuario.
        
4. **Interactuar de forma adversaria con el _bot_:**
    
    - El `QA` también debe crear casos de prueba que desafíen al _bot_ y lo saquen del "camino feliz" (`happy path`).
        
    - Esto ayuda a identificar problemas temprano en el ciclo de desarrollo, ya que el comportamiento del usuario no siempre es predecible o "amigable".

---

Un agente conversacional interactúa con diferentes sistemas (telefonía, aplicaciones móviles, _backends_), por lo que la estrategia de pruebas debe ser exhaustiva.

---

# Métodos
### **Enfoque de prueba de cuatro niveles**

La estrategia de prueba más exitosa en agentes conversacionales se basa en un enfoque de cuatro niveles que involucra a los equipos de desarrollo y control de calidad (`QA`). La automatización disminuye a medida que avanzas en los niveles, mientras que el esfuerzo manual aumenta.

#### **Nivel 1 y 2: Pruebas unitarias y de integración**

- **Responsables:** El equipo de desarrollo.
    
- **Cuándo:** Al inicio del ciclo de desarrollo.
    
- **Pruebas unitarias:** Se dividen en dos tipos:
    
    - **Pruebas de enrutamiento:** Verifican que la lógica y las transiciones entre los pasos del **CUJ** funcionen como se espera.
        
    - **Pruebas NLU:** Aseguran que el modelo **NLU** (Entendimiento del Lenguaje Natural) reconozca correctamente la intención del usuario. Debes incluir variaciones de frases, sinónimos y lenguaje informal. Es crucial para identificar frases no reconocidas (`no match`) y crear respuestas adecuadas.
        
- **Pruebas de integración:** El objetivo es encontrar errores en las interfaces y asegurar que los componentes trabajen en conjunto. Se realizan en un entorno lo más similar posible a producción.
    

#### **Nivel 3 y 4: Pruebas de punta a punta y A/B**

- **Responsables:** El equipo de `QA`.
    
- **Cuándo:** Cerca del despliegue en producción.
    
- **Pruebas de punta a punta (UAT):** El equipo de `QA` verifica que se cumplan todos los requisitos de la experiencia del cliente. Para esto, prueban el catálogo completo de **CUJs** e interactúan de forma adversaria con el agente.
    
- **Pruebas A/B:** Se comparan aleatoriamente dos versiones del sistema para determinar cuál funciona mejor. Es la fase final de certificación antes del lanzamiento completo.
    

### **Otras estrategias de prueba complementarias**

Además de los cuatro niveles, existen otras pruebas que se pueden usar de forma regular o esporádica:

- **Pruebas de diseño:** Ejecutadas por el equipo de diseño para garantizar que las intenciones correctas se activen en los escenarios planeados.
    
- **Pruebas de rendimiento:** Un equipo de arquitectos e ingenieros de telecomunicaciones evalúa el rendimiento del agente bajo diferentes cargas de trabajo.
    
- **Pruebas de regresión:** Aseguran que las funciones existentes sigan operando correctamente después de añadir nuevas características.
    
- **Pruebas de _failover_ y recuperación:** Evalúan cómo el agente maneja los fallos del sistema y se recupera de ellos.
    
- **Pruebas beta:** Se realizan con un grupo limitado de usuarios antes de un lanzamiento completo para exponer el _bot_ a un entorno real sin un riesgo a gran escala.
    

### **Seguimiento de resultados**

Es esencial definir un sistema de seguimiento para los resultados de las pruebas. Mantener un registro detallado de cada resultado por lanzamiento (`pass`/`fail`, defectos, observaciones) ayuda a identificar tendencias y problemas recurrentes. La información de los fallos se puede usar en el ciclo de _feedback_ para mejorar el agente de forma continua y prevenir problemas futuros.

---

# Implementando una estrategia de pruebas

La implementación de la estrategia de pruebas para un agente conversacional se basa en dos tipos de **pruebas unitarias**: las de enrutamiento y las de **NLU**. La estrategia de **desarrollo guiado por pruebas (`test-driven development`, TDD)** es fundamental para un desarrollo continuo y la mejora del agente.

---

### **Tipos de pruebas unitarias**

Las pruebas unitarias son la base de cualquier estrategia de pruebas para agentes conversacionales. Se enfocan en verificar partes pequeñas y específicas del _bot_.

1. **Pruebas de enrutamiento (`Routing tests`):** También conocidas como **"pruebas de página parcial"**, se centran en verificar que las transiciones entre páginas, la lógica condicional y las transiciones por reconocimiento de intenciones funcionen correctamente. Son útiles para aislar y resolver _bugs_ en una página específica sin tener que recorrer todo el flujo.
    
2. **Pruebas de NLU (`NLU tests`):** Evalúan la eficacia de las frases de usuario para activar la intención correcta en cada página. Se deben probar grandes lotes de frases ambiguas para asegurar una detección precisa. Se pueden usar herramientas personalizadas para automatizar estas pruebas y garantizar la precisión de la detección de intenciones.
    

### **Estrategia de desarrollo guiado por pruebas (TDD)**

El **TDD** es una filosofía central en el desarrollo de IA conversacional. Promueve pruebas iterativas a lo largo de todo el ciclo de vida del desarrollo.

1. **Entender los requisitos:** Antes de escribir cualquier prueba, define claramente lo que se espera que haga el agente.
    
2. **Escribir los casos de prueba:** Es la mejor práctica escribir los casos de prueba antes de desarrollar la funcionalidad. Estos casos deben cubrir diferentes escenarios de interacción, manejo de contexto y `fallbacks`.
    
3. **Implementar las características:** Con los casos de prueba listos, puedes empezar a desarrollar las intenciones, frases de entrenamiento, parámetros, respuestas y lógica de cumplimiento.
    
4. **Ejecutar las pruebas:** Usa las funciones nativas de **Dialogflow CX** o _scripts_ personalizados para ejecutar las pruebas.
    
5. **Refactorizar y repetir:** Si una prueba falla, modifica la configuración o la lógica del agente hasta que pase. Luego, refactoriza el código y vuelve a ejecutar las pruebas para asegurar que no se haya dañado nada en el proceso.
    
6. **Integración continua (`Continuous Integration`):** Una vez que las pruebas pasan, automatiza la ejecución de las pruebas cada vez que se realicen cambios en el agente para asegurar una calidad y funcionalidad consistentes.
    
7. **Monitoreo y retroalimentación:** Implementa un sistema de monitoreo para rastrear el rendimiento del agente. Usa los datos y la retroalimentación del usuario para escribir nuevas pruebas, creando un ciclo de mejora continua.
---

# Integración de testeos

Las pruebas de sistemas de integración garantizan que el agente conversacional funcione sin problemas con sistemas externos. Las pruebas más comunes se centran en la integración con el usuario final, los _webhooks_, la telefonía, el **DTMF** y el **`barge-in`**.

---

### **Pruebas de telefonía**

- **DTMF (`Dual Tone Multi-Frequency`):** Permite a los usuarios ingresar números usando el teclado del dispositivo. Es útil para entornos ruidosos o para ingresar secuencias largas. Para probarlo, debes llamar al agente para verificar que reconozca la entrada del teclado a través de la integración de telefonía. Una buena práctica es que el agente repita el número ingresado para confirmar que la información fue capturada correctamente.
    
    - **Mejores prácticas de DTMF:** No uses números (`1` o `2`) como sinónimos para la entidad **DTMF**, ya que puede causar conflictos si la página también recolecta otros números. Además, usa nombres para caracteres especiales como `pound` o `star` en la entidad para evitar un comportamiento errático.
        
- **`Barge-in`:** Permite a los usuarios interrumpir al agente mientras está hablando para acelerar la conversación. Se puede habilitar o deshabilitar a nivel de agente, flujo o página. Para probarlo, debes llamar al agente a través de la integración de telefonía, asegurándote de que la interrupción funcione en las páginas donde está habilitada y no lo haga en las páginas donde está deshabilitada.
    

---

### **Pruebas de _webhook_**

Las pruebas de _webhook_ aseguran que el código de cumplimiento (`fulfillment code`) del _bot_ pueda manejar distintos tipos de fallos. Para esto, se simulan fallos intencionales usando la consola de pruebas o la API.

- **Simulación de fallos:** Puedes usar la función de **inyección de parámetros** de la consola de pruebas para establecer valores específicos al inicio de un caso de prueba. El servicio de _webhook_ leerá estos parámetros para activar un fallo esperado.
    
- **Códigos de estado HTTP:** Cada código de error **HTTP** activará un evento diferente en **Dialogflow CX**. Tus casos de prueba deben cubrir cada uno de estos posibles eventos para asegurarte de que cada tipo de fallo esté manejado en tu código de cumplimiento.
---

# Testeo end-to-end (E2E)

Las pruebas de punta a punta (`end-to-end testing`, **E2E**) validan todo el recorrido del cliente. Hay tres tipos principales, listados en orden de complejidad: **pruebas modulares**, **pruebas de recorrido enfocado** y **pruebas de pila completa (`full-stack`)**. Todas deben incluir la validación de escenarios de respaldo (`fallback`) para asegurar un manejo adecuado de los fallos.

---

### **Tipos de pruebas E2E**

1. **Pruebas modulares:** Se centran en probar un **flujo** completo, desde el principio hasta el final. Son útiles para validar la lógica y el rendimiento de características o actualizaciones específicas de forma aislada. Son más amplias que las pruebas de página y garantizan la funcionalidad completa de un flujo.
    
2. **Pruebas de recorrido enfocado:** Prueban un **recorrido de usuario completo (`CUJ`)** utilizando entradas simuladas. Su objetivo es obtener _feedback_ temprano y aislar problemas dentro de un flujo de trabajo específico. Son más rápidas que las pruebas de pila completa y son ideales para probar un **CUJ** que ha sido actualizado recientemente.
    
3. **Pruebas de pila completa (`Full-Stack`):** Son las pruebas más completas. Incluyen todos los principios de las pruebas modulares y de recorrido enfocado, pero se aplican a **todos los flujos y CUJs** del agente. También abarcan la integración con todos los sistemas externos, como la telefonía y los _backends_.
    

### **Pruebas de escenarios de respaldo (`Fallback`)**

Es crucial que el agente pueda manejar situaciones inesperadas y errores de manera adecuada. Los escenarios de _fallback_ más comunes son:

- **Sin coincidencia (`No-match`):** Ocurre cuando la entrada del usuario no coincide con ninguna intención definida. El agente debe pedir una aclaración o ofrecer opciones alternativas. Para probarlo, crea escenarios con entradas fuera del alcance del _bot_.
    
- **Sin entrada (`No-input`):** El usuario no responde. El agente debe volver a preguntar o proporcionar información adicional. Para probarlo, no respondas o usa un espacio como entrada para simular el silencio.
    
- **Fallas de _webhook_:** Ocurren cuando una llamada a un servicio externo falla o expira. El agente debe informar al usuario sobre el problema de manera amigable y, si es posible, ofrecer alternativas, como escalar a un agente humano.
    

### **Mejores prácticas para las pruebas E2E**

- Cuando agregues una nueva página, prueba todas las rutas y transiciones existentes en el flujo para asegurar que sigan funcionando.
    
- Siempre incluye casos de prueba para los escenarios de "sin coincidencia" y "sin entrada".
    
- Para las actualizaciones de **NLU**, crea de 10 a 15 casos de prueba con variaciones en las frases para cada intención.
    
- Si una página tiene varios puntos de acceso, crea casos de prueba para cada ruta de entrada.

---

