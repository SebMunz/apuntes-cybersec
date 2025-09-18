---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/02 Create a Test Plan/"}
---

# Índice

[[#Review de desarrollo]]
[[#Pruebas exploratorias]]
[[#Creando una prueba en el simulador]]
[[#Validación de agentes conversacionales]]
[[#Importancia de la cobertura de pruebas completa]]
[[#Mejores prácticas para agente de voz]]

---

# Review de desarrollo

Para desarrollar casos de prueba sólidos, es esencial revisar los flujos existentes y desglosarlos en componentes funcionales. Un ejemplo de **recorrido del cliente** (`Customer User Journey`, **CUJ**) es la verificación del saldo de una cuenta, que se divide en tres componentes clave para el desarrollo de pruebas.

---

### **Componentes del flujo del CUJ: "Verificar Saldo"**

1. **Reconocimiento de la intención:** El agente debe capturar correctamente la intención del usuario. El punto de partida es la página **`Ask why user is calling`**, que encamina al usuario al flujo correcto.
    
2. **Autenticación:** Es el segundo componente, en el que se verifica si el usuario necesita autenticarse para acceder a la información de su cuenta.
    
3. **Confirmación del saldo:** Una vez autenticado el usuario, el agente le proporciona la información solicitada (`Confirm Balance`).
    

### **Asignación de pruebas a cada componente**

Cada componente requiere un tipo de prueba específico:

- **Reconocimiento de la intención:** Requiere **pruebas unitarias NLU** para probar una variedad de frases relacionadas con la solicitud del saldo de una cuenta.
    
- **Autenticación:** Requiere **pruebas de enrutamiento** para verificar que el flujo regrese a la intención principal de "consulta de saldo" después de que el _webhook_ de autenticación devuelva una respuesta positiva. También debe probarse el escenario en el que el usuario no está reconocido y se le pide que ingrese sus credenciales.
    
- **Confirmación del saldo:** Requiere **pruebas de enrutamiento** y **pruebas de integración** para asegurar que el agente responda con los valores correctos para el usuario autenticado y que la respuesta se muestre correctamente.

---

# Pruebas exploratorias

Además de las pruebas estructuradas, las **pruebas exploratorias** te permiten interactuar de forma libre y adversaria con el agente para encontrar errores inesperados. El simulador de **Dialogflow CX** y el _messenger_ son herramientas clave para este tipo de pruebas.

---

### **Pruebas exploratorias con el simulador**

El simulador te permite:

- Simular conversaciones reales con diferentes entradas.
    
- Emular la interacción con clientes de _front-end_ usando parámetros de inicialización o eventos.
    
- Monitorear el estado de la sesión, los parámetros y los cambios de contexto.
    
- Probar la funcionalidad de _webhooks_ e integraciones externas.
    
- Volver a un punto anterior en la conversación para probar diferentes comportamientos.
    

### **Configuración del simulador**

En el panel lateral derecho de la consola, puedes:

- Seleccionar el entorno o la versión del flujo.
    
- Habilitar o deshabilitar _webhooks_.
    
- Probar cómo el agente maneja las respuestas parciales.
    
- Activar el análisis de sentimiento.
    

### **Entradas que puedes simular**

- **Texto:** La forma más común de interactuar.
    
- **DTMF:** Para probar las interacciones de telefonía simulando las pulsaciones del teclado del teléfono.
    
- **Metadatos del usuario final:** Para probar diferentes tipos de usuarios o estados.
    
- **Eventos personalizados:** Para ver cómo reacciona el agente a ciertos disparadores.
    
- **Valores y ámbitos de parámetros:** Para probar diferentes contextos o estados de la sesión.
    

### **Monitorear el estado de la sesión**

El simulador te permite ver en todo momento:

- El flujo y la página activos.
    
- Los parámetros recolectados y sus valores.
    
- Los pasos de ejecución detallados que toma el agente en la conversación.
    

### **Limitaciones del simulador**

- **Valores nulos:** No permite establecer directamente el valor de un parámetro a nulo.
    
- **Multilingüe:** Solo permite probar un idioma a la vez.
    
- **Entidades de sesión:** No es compatible con las entradas de entidades de sesión.
    
- **Voz:** El rendimiento de la traducción de voz puede variar según el acento, la claridad del habla y el ruido de fondo.
    

### **Uso del _messenger_**

El **Dialogflow CX Messenger** permite realizar pruebas en un entorno web más realista, lo que permite:

- Probar en diferentes dispositivos o navegadores.
    
- Revisar la consistencia de las respuestas y el renderizado de elementos visuales.
    
- Interactuar con elementos de la interfaz gráfica.

---

# Creando una prueba en el simulador

Se divide en tres fases: la creación de un escenario, el guardado del caso de prueba y la gestión de la ejecución y los resultados.

---

### **Crear un caso de prueba**

1. **Crea un escenario de conversación:** Inicia una conversación en el simulador que represente un recorrido ideal o un escenario específico. Estos se conocen como **"casos de prueba dorados" (`golden test cases`)** porque son conversaciones de referencia que se alinean con las frases de entrenamiento y el diseño del agente.
    
2. **Guarda el caso de prueba:** Una vez que el escenario se desarrolle según lo esperado, haz clic en **`Save as test case`**. Al guardarlo, puedes agregar detalles, como:
    
    - **Nombre de visualización único (`Display Name`).**
        
    - **Etiquetas (`Tags`):** Para organizar los casos de prueba. Las etiquetas deben seguir una convención de nomenclatura previamente acordada (ej. `#nombre_pod_nombre_flujo`).
        
    - **Notas:** Para describir el propósito del caso de prueba.
        
    - **Parámetros:** Selecciona los parámetros de sesión que desees monitorear. El simulador verificará que los valores de estos parámetros coincidan con los del caso de prueba dorado en cada ejecución.
        

---

### **Ejecutar y gestionar los casos de prueba**

Una vez guardados, los casos de prueba se pueden gestionar desde la sección **`Test Cases`** en la consola de **Dialogflow CX**.

1. **Ejecución:** Puedes buscar casos de prueba por nombre o filtrarlos por etiquetas. Al encontrarlos, haz clic en el botón de **reproducir** para ejecutar un solo caso de prueba o en **`Run all test cases`** para ejecutar todos.
    
2. **Monitoreo y resultados:** Después de la ejecución, puedes ver el estado y los resultados en la cola de tareas. El sistema compara la ejecución en vivo con el caso de prueba dorado en cada turno.
    
    - Verifica la coincidencia del diálogo, la intención, la página actual y los parámetros de sesión.
        
    - Cualquier discrepancia o fallo se resaltará para su revisión.
        

---

### **Mejores prácticas y herramientas adicionales**

El simulador también ofrece herramientas para facilitar el proceso de pruebas.

- **Actualizaciones en tiempo real:** Puedes hacer cambios en un caso de prueba mientras se ejecuta. Si detectas un error o una oportunidad de mejora, puedes actualizar el escenario y guardarlo con un nuevo nombre o sobrescribir el existente.
    
- **Botón `Undo Last Conversation Turn`:** Permite retroceder un paso en la conversación para corregir algo y volver a probar el escenario.
    
- **Filtros con etiquetas:** Usar etiquetas con una convención de nomenclatura clara te ayudará a organizar y encontrar casos de prueba más fácilmente.

---

# # Validación de agentes conversacionales

La validación de agentes conversacionales es una herramienta de **Dialogflow CX** que ayuda a mejorar la calidad y el rendimiento de los agentes. Se puede solicitar a demanda desde la consola o la **API**.

### **Características de la validación**

- **Es a demanda:** Se ejecuta cuando el usuario lo solicita, después de editar el agente y re-entrenar los modelos **NLU**.
    
- **Solo informativa:** Los resultados no afectan el comportamiento del agente. Se pueden ignorar y aun así lanzar el agente.
    
- **Categorías de mensajes:** Los mensajes cubren la calidad de los datos de entrenamiento (**NLU**) y la estructura de los flujos basados en páginas. Un ejemplo de mensaje es cuando una página no puede llegar al final de un flujo o sesión.
    
- **Visualización:** Los mensajes se muestran en la lista de intenciones, entidades y páginas. En la lista de páginas, un ícono indica el nivel de gravedad de los mensajes asociados.
    

### **Niveles de gravedad**

Hay tres niveles de severidad para los problemas identificados:

- **Info:** Advertencias informativas sobre el incumplimiento de las mejores prácticas de diseño.
    
- **Warning:** Alertas sobre posibles comportamientos inesperados del agente.
    
- **Error:** Notificaciones de fallos que está experimentando el agente.

---

# Importancia de la cobertura de pruebas completa

Una **cobertura de pruebas** completa es crucial en el desarrollo de agentes conversacionales para garantizar la calidad y el rendimiento. Ayuda a detectar problemas a tiempo, asegura una experiencia de usuario positiva y previene regresiones.

---

### **Beneficios de una cobertura de pruebas completa**

- **Detección temprana de errores:** Permite identificar y resolver problemas antes de que afecten a los usuarios finales, lo que ahorra tiempo y recursos.
    
- **Mejora la calidad:** Asegura que el agente se comporte de manera esperada en distintos escenarios, lo que resulta en interacciones más precisas y útiles para el usuario.
    
- **Alineación con el diseño:** Cada caso de prueba valida una funcionalidad específica, asegurando que las características, desde las más simples a las más complejas, se alineen con los objetivos de diseño.
    
- **Prevención de regresiones:** Los cambios o actualizaciones en el agente no afectarán negativamente a las funcionalidades existentes.
    
- **Validación de la lógica del flujo:** Confirma que la conversación progresa de manera lógica y fluida, basándose en la entrada del usuario.
    
- **Robustez:** Incluye pruebas para **casos extremos** (`edge cases`), asegurando que el agente puede manejar una amplia variedad de interacciones inusuales.
    
- **Precisión del modelo NLU:** Al probar con diversas frases, se entrena y mejora la capacidad del modelo para entender la intención del usuario.
    

---

### **Medición de la cobertura de pruebas**

La funcionalidad de **cobertura de pruebas** en **Dialogflow CX** ayuda a entender qué tan exhaustivos son los casos de prueba para validar el comportamiento del agente.

- **Qué mide:** Evalúa qué tan bien los casos de prueba verifican las transiciones, intenciones y grupos de rutas del agente.
    
- **Cómo usarlo:** Al analizar la cobertura de pruebas, se pueden identificar **brechas** en el proceso de pruebas. Esto indica dónde se deben añadir o modificar casos de prueba.
    
- **Cómo aumentarla:** Agrega nuevos casos de prueba o modifica los existentes para asegurar que todas las transiciones, intenciones y grupos de rutas estén probados a fondo. Es importante revisar y actualizar los casos de prueba regularmente para mantenerlos alineados con los cambios en el diseño del agente.

---

# Mejores prácticas para agente de voz

### **Pasos para crear un plan de pruebas**

1. **Definir el alcance (`Test Scope`):** Establece qué aspectos del agente conversacional se van a probar. Esto puede incluir la precisión de las respuestas, la correcta redirección de los usuarios o el manejo de escenarios de respaldo (`fallback`).
    
2. **Crear casos de prueba:** Desarrolla casos que cubran todas las interacciones posibles con el usuario. Es fundamental incluir los **casos extremos** (`edge cases`) y basar estos casos en los recorridos del cliente (`CUJs`).
    
3. **Configurar herramientas y entornos:** Asegura que los entornos de prueba sean lo más parecidos posible al entorno de producción para obtener resultados fiables.
    
4. **Crear un plan de ejecución:** Define un cronograma para ejecutar los casos de prueba y registrar los resultados.
    
5. **Definir métricas de rendimiento:** Establece métricas claras, como el tiempo de respuesta, la precisión y la satisfacción del usuario, para medir la efectividad del flujo conversacional.
    
6. **Recopilar datos:** Realiza las pruebas para obtener datos sobre cómo el agente maneja las consultas, las redirecciones y los escenarios de respaldo.
    
7. **Analizar y reportar:**
    
    - Analiza los datos recopilados para identificar áreas de mejora.
        
    - Compila un informe con los hallazgos.
        
    - Implementa los cambios basados en los resultados de las pruebas.
        
8. **Revisión final:** Antes de pasar al siguiente entorno, realiza una revisión final para asegurar que se hayan cumplido todos los objetivos del plan.

### **Consideraciones para las pruebas de _chat_**

- **Variaciones textuales:** Asegúrate de que las pruebas cubran variaciones en el lenguaje, incluyendo la jerga, errores de ortografía y abreviaciones que los usuarios pueden usar.
    
- **Integración de la interfaz de usuario:** Si el agente se integra con una **UI visual** (`user interface`), verifica que las respuestas de texto se coordinen correctamente con botones, imágenes y otros elementos visuales.
    
- **Capacidad asincrónica:** El _chat_ a menudo permite pausas largas entre los mensajes. El agente debe ser capaz de manejar estos tiempos de espera (`timeouts`) y reanudar la conversación de manera fluida.
    
- **Elementos visuales:** Las pruebas deben incluir la correcta visualización de elementos gráficos. Esto es algo que no se considera en las pruebas de voz, pero que es crucial para la experiencia de usuario en un _chat_.

---

