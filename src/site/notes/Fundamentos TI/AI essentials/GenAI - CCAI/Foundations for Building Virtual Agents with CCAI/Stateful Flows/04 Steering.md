---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Stateful Flows/04 Steering/"}
---

# Índice

[[#Diseñando el Steering del agente]]
[[#Desambiguaciones en Agentes Conversacionales]]
[[#Cómo afinar un agente conversacional]]

---

# Diseñando el Steering del agente

El _steering_ (dirección o guiado) en un agente conversacional se refiere a cómo se conduce la conversación para que el usuario llegue a su objetivo. Los puntos clave a la hora de diseñar la recopilación de intenciones principales son:

- **¿Dónde colocar la recopilación de intenciones principales?**
    
    - Puedes usar la **página de inicio** de tu flujo para que las intenciones principales estén en el ámbito de todas las páginas, lo que es útil si quieres que el agente esté siempre listo para manejar una nueva solicitud en cualquier punto de la conversación.
        
    - Alternativamente, puedes usar una **página separada** para la recopilación de intenciones principales. Esto te permite tener un control más preciso y realizar acciones previas (como pre-establecer parámetros o ejecutar _webhooks_) antes de que el usuario declare su intención. Esta es la opción más común y recomendada.
        
- **¿Qué usar para dirigir la conversación? Rutas o grupos de rutas?**
    
    - **Rutas:** No tienes que agruparlas, lo que puede ser más sencillo para agentes simples.
        
    - **Grupos de rutas:** Te dan un control más granular y facilitan la reutilización de conjuntos de rutas en múltiples páginas. Por ejemplo, un grupo de rutas `facturación` puede ser usado tanto en la página de inicio como en una página de desambiguación.
        

---

### **Construyendo un flujo de _Steering_**

Para crear un flujo de _steering_, puedes seguir un proceso típico que a menudo se inicia con la intención de bienvenida (`Default Welcome Intent`).

1. **Activación de la conversación:** La conversación se inicia con el **`Default Welcome Intent`**. Esta intención se activa en el primer turno y sirve para que el agente salude al usuario y le pregunte cómo puede ayudarle.
    
2. **Configuración de la página:** En la página donde se recopilará la intención principal, debes agregar:
    
    - **Un mensaje de bienvenida:** Algo como: "Hola, ¿en qué puedo ayudarte hoy?".
        
    - **Manejo de errores:** Configura los manejadores de eventos para `no-match` y `no-input` en caso de que el agente no entienda al usuario.
        
    - **Rutas o grupos de rutas:** Añade las rutas necesarias para cada intención principal que tu agente deba manejar. Una buena práctica es guardar el nombre de la intención coincidente como un parámetro para un enrutamiento posterior más sencillo.
        

### **Consideraciones adicionales**

- **Manejo de DTMF:** Si estás construyendo un agente de voz, considera el manejo de la marcación por tonos (DTMF) para permitir que los usuarios usen el teclado numérico.
    
- **Transferencia a operadores:** Planifica cómo manejarás las solicitudes de los usuarios para hablar con un agente humano. La decisión de transferir al usuario (o tratar de retenerlo) puede depender del valor comercial de su solicitud. Por ejemplo, en el caso de un cliente que quiere cancelar un servicio, es mejor escalarlo a un agente humano lo antes posible.

---

# Desambiguaciones en Agentes Conversacionales

La **desambiguación** es el proceso de aclarar la intención de un usuario cuando su solicitud inicial es ambigua o incompleta. Este proceso es clave para dirigir al usuario al flujo o sistema correcto.

Existen dos escenarios principales en los que se requiere desambiguación:

1. **Solicitud inicial vaga:** El usuario hace una afirmación genérica como "Tengo una pregunta" o "Tengo un problema" en lugar de una solicitud específica. También puede dar un término amplio como "solución de problemas", que requiere que el agente aclare a qué se refiere.
    
2. **Información faltante para el _routing_:** La solicitud del usuario es clara, pero el agente necesita más información para saber a dónde dirigir la conversación. Por ejemplo, un usuario dice que quiere "portar una línea", pero el agente necesita saber si es "portar _dentro_" o "_fuera_" para aplicar las reglas de negocio correctas.
    

---

### **Cómo construir desambiguaciones efectivas**

El diseño de las desambiguaciones debe ser estratégico para evitar la frustración del usuario.

- **Reacciones a "pre-expansiones":** Si el usuario dice algo vago como "Tengo una pregunta", el agente solo necesita mostrar que está listo para escuchar y animarlo a continuar (ej., "Adelante" o "Claro, ¿qué pregunta tienes?"). Esto es útil cuando hay un gran número de posibles intenciones.
    
- **Solicitud de información específica:** Si el abanico de opciones es limitado (ej., "¿portar dentro o fuera?"), el agente debe pedir la información específica que necesita para continuar.
    
- **Combinación de opciones:** En plataformas de chat, puedes combinar ambas estrategias usando **botones** para las opciones más comunes mientras permites que el usuario escriba su respuesta.
    

---

### **Principios de diseño conversacional para la desambiguación**

1. **Evita la repetición:** No hagas la misma pregunta de desambiguación una y otra vez. Almacena el valor de los parámetros para evitar bucles.
    
2. **Usa datos de _backend_:** Si tienes información del cliente (ej., sabe que solo tiene una cuenta de móvil), úsala para evitar hacer preguntas innecesarias ("¿Llamas por tu cuenta de hogar o de móvil?").
    
3. **Haz eco de las palabras del cliente:** Usa el lenguaje del cliente para hacer la pregunta. Por ejemplo, si el cliente dice "problema de facturación", pregunta "¿Qué problema de facturación tienes?" en lugar de "¿Qué pregunta de facturación tienes?".
    
4. **Maneja el contexto:** Los usuarios a menudo asumen un contexto previo. Si el agente pregunta "¿Qué pregunta de facturación tienes?", el usuario podría responder solo con "Cuánto es". Asegúrate de tener **intenciones contextuales** para capturar este tipo de frases.

---
# Cómo afinar un agente conversacional

Después de configurar un agente, es crucial optimizarlo para que su rendimiento sea óptimo. Para ello, se utilizan varias herramientas y métodos antes de llevarlo a producción.

#### **Herramientas de validación**

1. **Herramienta de validación nativa:**
    
    - **Propósito:** Identifica problemas como frases de entrenamiento demasiado similares entre intenciones, parámetros sin entidades definidas o anotaciones inconsistentes.
        
    - **Tipos de mensajes:**
        
        - **Errores:** Impiden que el agente maneje la solicitud. Es obligatorio resolverlos.
            
        - **Advertencias:** Podrían reducir la precisión del agente. Se recomienda resolverlas.
            
        - **Información:** Sugieren mejoras según las mejores prácticas. Deben ser revisadas.
            
2. **Scripts de validación personalizados:**
    
    - **Propósito:** Puedes crear tus propios _scripts_ para identificar problemas específicos que la herramienta nativa no cubre, como frases de entrenamiento similares en diferentes intenciones o errores en el etiquetado de entidades.
        

#### **Uso de conjuntos de pruebas (`test sets`)**

- **Evita las frases de entrenamiento:** No uses las mismas frases que usaste para el entrenamiento en los conjuntos de pruebas. Esto no te dará información útil sobre cómo se comportará el agente con frases nuevas.
    
- **Usa frases naturales:** Las frases de prueba deben ser expresiones que los usuarios reales dirían. Si tienes datos de producción, úsalos.
    
- **Asegura una amplia cobertura:** Si tu agente tiene muchas intenciones, asegúrate de que tus pruebas cubran un amplio rango de ellas y no solo unas pocas.
    
- **Automatiza las pruebas:** Puedes usar herramientas como casos de prueba integrados en Conversational Agents o bibliotecas como SCRAPI para automatizar la ejecución de tus pruebas.
    

#### **Afinación del NLU**

La afinación de la **comprensión del lenguaje natural (NLU)** es un proceso clave para mejorar la precisión del agente.

- **Evita el sobreajuste (`overfitting`):** Si una frase no coincide con una intención, no la añadas directamente a las frases de entrenamiento. Primero, considera si el etiquetado de entidades es correcto o si hay un problema de superposición entre intenciones.
    
- **Prueba siempre los cambios:** Después de hacer una modificación, ejecuta tus pruebas para asegurarte de que los cambios no han generado un peor rendimiento.
    

#### **Ajustes comunes: Unir y dividir intenciones**

A menudo, las intenciones con frases de entrenamiento muy similares causan problemas de "no-match". Para solucionarlo, puedes unir o dividir intenciones.

- **Unir intenciones:**
    
    - **Cuándo:** Cuando dos o más frases representan la misma intención del usuario.
        
    - **Cómo:** Mueve las frases de entrenamiento de la intención que quieres eliminar a la que quieres mantener. Asegúrate de no copiar frases innecesarias y actualiza las rutas de la intención eliminada.
        
- **Dividir intenciones:**
    
    - **Cuándo:** Cuando una intención cubre dos o más intenciones distintas del usuario.
        
    - **Cómo:** Revisa las frases de entrenamiento una por una y decide a qué intención nueva pertenecen.
        

Para una pequeña cantidad de frases, estos cambios se pueden hacer directamente en la consola. Para intenciones más grandes, se recomienda descargar las frases a una hoja de cálculo, editarlas y volver a subirlas.