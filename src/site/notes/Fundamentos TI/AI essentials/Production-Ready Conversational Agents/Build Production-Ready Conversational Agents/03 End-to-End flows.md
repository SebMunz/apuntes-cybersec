---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/03 End-to-End flows/"}
---

# Índice
[[#Diseño de flujos en agentes conversacionales]]
[[#Mejores prácticas]]

---

# Diseño de flujos en agentes conversacionales

Existen dos tipos principales de flujos:

- **Flujos de dirección (`Steering flows`)**: Ayudan a identificar el objetivo del usuario.
    
- **Flujos de caso de uso (`Use case flows`)**: Se encargan de cumplir ese objetivo.
    

---

### **Pasos para desarrollar un flujo de caso de uso**

1. **Identificar los recorridos del usuario (`User Journeys`):** Define los recorridos clave relacionados con un tema específico. Por ejemplo, en un flujo de facturación, se pueden identificar recorridos como:
    
    - Explicar una factura.
        
    - Identificar el saldo.
        
    - Entender por qué la factura aumentó.
        
2. **Identificar pasos y puntos de decisión:** Desglosa los recorridos en pasos y establece los puntos donde el _bot_ debe tomar decisiones. Por ejemplo, para un aumento de factura:
    
    - Obtener los detalles de la factura.
        
    - Si la factura no aumentó, clarificarlo.
        
    - Si sí, identificar y explicar las razones principales.
        
    - **Mejores prácticas:** Revisa transcripciones de conversaciones humanas para adaptar el lenguaje del _bot_ y hacerlo más natural.
        
3. **Identificar parámetros y _webhooks_:**
    
    - Define los **parámetros** que se necesitan rastrear para cumplir el objetivo del usuario.
        
    - Si se requiere información del _backend_, determina la estructura de los **webhooks** que proporcionarán esos datos.
        
4. **Identificar la estructura de páginas:**
    
    - Divide las rutas de conversación en páginas de manera lógica.
        
    - Una **página** puede representar un estado conversacional o simplemente servir para dirigir al usuario sin que el agente responda.
        
    - Evita sobrecargar una página con demasiadas tareas.
        
5. **Construir el agente:** Con toda la información anterior, se puede proceder a la construcción del agente en **Dialogflow CX**.

---

### **Caminos felices vs. Caminos infelices**

- **Caminos felices (`Happy paths`):** Son las conversaciones ideales y fluidas. En estos escenarios, el usuario responde como se espera, el _bot_ lo entiende sin problemas y todo el proceso se desarrolla sin interrupciones ni errores.
    
- **Caminos infelices (`Unhappy paths`):** Son las conversaciones problemáticas. Ocurren cuando el _bot_ no entiende al usuario, no escucha su entrada, se encuentra con errores de **webhook** o simplemente malinterpreta lo que el usuario dice. Esto a menudo resulta en una escalada de la llamada a un agente humano.
    

### **Pasos para construir un camino feliz**

Generalmente se recomienda empezar por los caminos felices. Aquí tienes los pasos para construirlos en tu flujo:

1. **Añadir páginas:** Incluye las páginas que has identificado como necesarias para la conversación.
    
2. **Crear mensajes (`prompts`):** Agrega los mensajes o preguntas que el _bot_ hará al usuario.
    
3. **Configurar intenciones y parámetros:** Define las **intenciones** y los **parámetros** para capturar lo que el usuario responderá a tus preguntas.
    
4. **Establecer rutas:** Define las **rutas** que el usuario seguirá a través del flujo.
    
5. **Añadir _webhooks_ y parámetros:** Agrega los **webhooks** y los valores preestablecidos de parámetros si el flujo los requiere.

---

### **Cómo manejar los caminos infelices**

- **Respuestas para `no-match` y `no-input`:**
    
    - Incluye respuestas para cuando la entrada del usuario no coincide con ninguna intención esperada (`no-match`).
        
    - Para agentes de voz, también agrega respuestas para cuando el usuario no dice nada (`no-input`).
        
- **Errores de _webhook_:**
    
    - En cada punto donde uses un _webhook_, añade eventos que manejen los errores que puedan ocurrir.
        
- **Respuestas no comprometidas:**
    
    - Anticipa las respuestas ambiguas o no comprometidas del usuario. Por ejemplo, si preguntas "¿Qué fecha viajará?", diseña una ruta para una respuesta como "No estoy seguro".
        
- **Escaladas y peticiones de tiempo:**
    
    - Prepara respuestas para cuando los usuarios quieran hablar con un agente humano.
        
    - Considera los casos en que los usuarios pidan más tiempo para responder. Estos son patrones conversacionales comunes que deben ser abordados.

---

# Mejores prácticas

Un **flujo de caso de uso** debe ser sencillo, reutilizable y fácil de entender. Implementar estas **mejores prácticas** ayuda a minimizar errores y a crear un agente conversacional más robusto.

---

### **Mejores prácticas para flujos de casos de uso**

#### **1. Construir una vez y reutilizar**

- **Reutilizar entidades e intenciones:** En lugar de crear intenciones para casos similares (`"yes"` o `"no"`), usa una sola intención que pueda ser usada en múltiples lugares. Esto también estandariza el **NLU**. Las entidades se pueden exportar e importar para su reutilización.
    
- **Abstraer patrones comunes:** Crea un flujo o subflujo dedicado para tareas comunes como la autenticación. De esta forma, cualquier flujo que lo necesite puede ser dirigido a este subflujo.
    
- **Usar grupos de rutas:** Usa **grupos de rutas** o rutas en la página de inicio en lugar de copiar la misma ruta en varias páginas. Esto reduce el tiempo de configuración y es útil para flujos de dirección con muchas intenciones. Puedes usar grupos de rutas a nivel de agente para reutilizarlos en diferentes flujos.
    
- **Unificar tratamientos:** Si múltiples intenciones tienen el mismo tratamiento, haz que todas establezcan el mismo parámetro. Luego, usa una sola ruta basada en ese parámetro para ejecutar la acción deseada.
    

---

#### **2. Mantenerlo simple y autodoocumentado**

- **Evitar soluciones complejas:** No anides demasiadas funciones. Es mejor que el código sea claro y que la próxima persona que trabaje en él pueda entenderlo fácilmente.
    
- **Usar nombres claros:** Asigna nombres fáciles de entender a páginas, intenciones y flujos. Por ejemplo, si tienes varias páginas relacionadas con la facturación, nombra cada una con un prefijo (`"Reducir factura"`).
    
- **Usar descripciones:** Añade descripciones concisas a intenciones y páginas. Esto actúa como metadato y ayuda a otros a entender la función de cada elemento.
    
- **Evitar sobrecargar las páginas:** No pongas demasiadas tareas o rutas en una sola página. Si una página tiene que hacer muchas cosas, es una señal de que debe dividirse en varias páginas.
    

---

#### **3. Estandarizar tratamientos y enfoques**

- **Convenciones de nombres:** Usa convenciones consistentes para nombrar todos los elementos de un flujo. Por ejemplo, que todas las páginas empiecen con el nombre del subflujo y una descripción de su función.
    
- **Tratamientos consistentes:** Si una funcionalidad está habilitada en un lugar (ej. **DTMF**), es recomendable habilitarla en todas las partes del flujo para que la experiencia del usuario sea consistente.
    

---

#### **4. Minimizar la posibilidad de caminos infelices**

- **Usar mensajes claros:** Haz preguntas que minimicen la posibilidad de una mala interpretación por parte del _bot_.
    
- **Ofrecer opciones (`options`):** Cuando sea apropiado, ofrece opciones al usuario. Para conversaciones de _chat_, los botones son una buena opción para las respuestas más comunes. Sin embargo, no restrinjas las opciones del usuario cuando hay una gran variedad de respuestas posibles (ej. en la primera pregunta).
    
- **Simplificar para el usuario:** Si es posible, simplifica las tareas. En lugar de leer un nombre de sitio web largo, envía un **SMS** con el enlace.
    
- **Añadir caminos complementarios:** Si hay un camino para una respuesta "sí", asegúrate de que también haya un camino para una respuesta "no".
    
- **Evitar bucles:** Identifica y evita bucles infinitos en los que el usuario se queda atrapado en una página. Puedes usar un contador de parámetros para transferir al usuario a un flujo de respaldo después de un cierto número de intentos fallidos.

---

