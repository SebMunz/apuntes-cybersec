---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Basic Performance Measurement/02 Fase de Comprensión/"}
---

# Índice
[[#Cómo se ve]]
[[#Revisión de conversaciones]]

---
La **fase de comprensión** del ciclo de retroalimentación se enfoca en entender el recorrido del cliente para identificar oportunidades de mejora en un agente conversacional. Este proceso ayuda a los desarrolladores a crear soluciones que satisfacen las necesidades de los usuarios y ofrecen experiencias excepcionales.

---
# Cómo se ve
### **El recorrido del cliente**

El recorrido típico de un cliente con un _bot_ incluye varios puntos de contacto, desde el problema inicial hasta la posible resolución o escalada:

1. **Punto de dolor del cliente:** Un problema específico que el cliente necesita resolver, por ejemplo, relacionado con su cuenta.
    
2. **Herramientas de autoservicio en línea:** El cliente primero intenta resolver el problema por su cuenta usando recursos en línea, como la página de búsqueda o de su cuenta.
    
3. **Llamar a servicio al cliente:** Si el problema no se resuelve en línea, el cliente busca soporte directo, iniciando el contacto que podría llevar a la resolución o escalada.
    
4. **Conducción (`Steering`):** Se determina la intención del cliente en la llamada para dirigirlo al recurso adecuado, mejorando la eficiencia y la satisfacción.
    
5. **Experiencia de autoservicio durante la llamada:** El sistema automatizado intenta resolver el problema. Si tiene éxito, el problema se resuelve; de lo contrario, se indica la necesidad de escalada.
    
6. **Escalada o colgado:** Si las opciones de autoservicio se agotan, el problema se transfiere a un agente humano. El cliente también puede optar por colgar la llamada.
    

Cada paso del recorrido ofrece datos valiosos que pueden analizarse para mejorar el rendimiento del agente conversacional. El objetivo es crear una experiencia eficiente para el cliente, reduciendo la necesidad de escalada y mejorando su satisfacción general.

---
# Herramientas útiles

Para entender el recorrido del cliente, puedes usar la herramienta de **historial de conversaciones (`Conversation History`)** para analizar interacciones reales entre tu agente y los usuarios. Esta herramienta te permite:

- **Filtrar y buscar** conversaciones completas por fecha, hora, intenciones, o palabras clave.
    
- **Revisar detalles de la conversación**, como su duración, el número de turnos, el canal y el idioma.
    
- **Examinar conversaciones individuales**, donde puedes ver la respuesta del agente, la entrada del usuario, la intención y la entidad detectada.
    
- **Identificar problemas**, como malentendidos comunes, respuestas inútiles o temas que el agente no pudo manejar.
    

---

### **Cómo funciona la herramienta de historial de conversaciones**

El **historial de conversaciones** te proporciona una visión general y detallada de cada interacción.

#### **Información general**

En la vista de resumen, puedes ver:

- **Identificador único:** Para encontrar conversaciones específicas.
    
- **Duración:** El tiempo que duró la conversación.
    
- **Turnos:** El número de intercambios entre el usuario y el agente. Un número alto indica una conversación larga.
    
- **Canal:** Por dónde se realizó la conversación (ej. web, móvil).
    
- **Idioma:** El idioma configurado para el agente.
    
- **Hora de inicio:** Cuándo comenzó la conversación.
    

#### **Información detallada**

Al abrir una conversación individual, puedes ver:

- **`User Utterance`:** Lo que el usuario dijo.
    
- **`Agent Response`:** Lo que el agente respondió.
    
- **`Intent Detected`:** La intención que el agente detectó en la frase del usuario (ej. pagar mi factura).
    
- **`Entity Detected`:** Las entidades detectadas en la frase (ej. "iPhone" como un dispositivo).
    
- **`Page` y `Flow`:** La página y el flujo en el que se encontraba el usuario.
    
- **`Escalation Indicator`:** Un indicador que muestra si la conversación fue transferida a un agente humano.
    

---

### **Oportunidades de mejora**

El análisis del historial de conversaciones puede ayudarte a identificar oportunidades para mejorar la **NLU**, el flujo conversacional y la calidad de las respuestas. Puedes descubrir:

- **Malentendidos:** Palabras mal transcritas o intenciones y entidades que no se reconocieron correctamente.
    
- **Respuestas inútiles:** Usuarios insatisfechos o respuestas del agente que no son claras.
    
- **Temas no manejados:** Situaciones en las que el agente no pudo manejar una solicitud, como transferir la llamada a un agente humano.
    

El uso de esta herramienta te permite refinar el agente, mejorar la experiencia del usuario y usar la información para estrategias de negocio más amplias, como la creación de personas de usuario o la mejora del desarrollo de productos.

### **Consideraciones éticas**

Al extraer información de las conversaciones, es fundamental tener en cuenta la ética. Esto incluye la **privacidad de los datos**, la **transparencia** sobre cómo se recogen y utilizan los datos, y el **control del usuario**, dándoles la opción de no participar en la recopilación de datos.

---

# Revisión de conversaciones

Hay dos métodos para revisar el historial de conversaciones: manual y dirigido. El método manual es muy detallado, pero consume mucho tiempo. El método dirigido, que utiliza filtros, es más eficiente para grandes volúmenes de datos. La combinación de ambos es ideal para una revisión exhaustiva y escalable.

---

### **Cómo revisar las conversaciones**

1. **Establece un objetivo:** Antes de sumergirte en las transcripciones, define un objetivo claro. Esto te mantendrá enfocado y te asegurará de obtener la información necesaria para mejorar el agente. Los objetivos comunes son:
    
    - Evaluar la efectividad en la detección de intenciones.
        
    - Entender la capacidad del _bot_ para comprender las entidades.
        
    - Juzgar la adecuación de las respuestas del agente.
        
2. **Crea una plantilla:** Diseña una plantilla para recopilar información de las transcripciones de manera consistente, sin importar quién las revise. Puedes usar una hoja de cálculo de Google (`Google Sheet`) con campos para la consulta del usuario, la respuesta del agente y si la conversación fue exitosa.
    
3. **Selecciona una muestra aleatoria:** Revisa una muestra aleatoria de las conversaciones para evitar sesgos. Si solo analizas las conversaciones problemáticas, obtendrás una visión distorsionada del rendimiento del agente. Puedes usar los filtros del historial de conversaciones para seleccionar el subconjunto de llamadas que necesitas y ordenarlas por ID.
    
4. **Revisa y documenta:**
    
    - **Presta atención a:** El entendimiento de la consulta del usuario, la calidad de las respuestas y la capacidad del agente para completar tareas.
        
    - **Documenta las observaciones:** Agrega las respuestas de todos los revisores en un documento común. Esto ayuda a identificar tendencias y patrones de comportamiento para que el equipo pueda darles prioridad.
        

### **Limitaciones**

- **Revisión manual:** Es el método más detallado, pero no es escalable. A medida que el número de conversaciones crece, se vuelve imposible revisarlas todas manualmente.
    
- **Detección automática de tendencias:** Puede identificar patrones rápidamente en grandes conjuntos de datos, pero puede no ofrecer el mismo nivel de detalle que la revisión manual y podría pasar por alto problemas importantes.
    

La mejor estrategia es una mezcla de ambos enfoques, adaptada a tus necesidades y recursos. Si tienes pocas conversaciones, la revisión manual puede ser suficiente. Pero si manejas un gran volumen de conversaciones, la detección automática de tendencias es la mejor opción.

---
