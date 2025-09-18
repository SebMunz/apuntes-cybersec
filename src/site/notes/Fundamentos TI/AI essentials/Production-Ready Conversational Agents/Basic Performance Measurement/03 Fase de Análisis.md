---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Basic Performance Measurement/03 Fase de Análisis/"}
---

# Índice
[[#Métricas capturables]]
[[#Herramientas]]
[[#Troubleshoot]]
[[#Errores de webhook]]
[[#Análisis de flujo]]

---

# Métricas capturables

### **Métricas clave en el recorrido del cliente**

Las métricas varían según la etapa del recorrido del cliente y el rol de quien las revisa.

- **Volumen de llamadas entrantes:** Una métrica inicial clave al inicio del recorrido, útil para entender el comportamiento de los clientes. El volumen puede fluctuar por día de la semana u hora.
    
- **Tasas de "No Coincidencia" (`No Match`) y "No Entrada" (`No Input`):** Indican si el agente está obteniendo la intención inicial del cliente en las primeras etapas de la conversación.
    
- **Métricas de éxito/fracaso:** Miden la efectividad del autoservicio, como si un pago fue procesado correctamente.
    
- **Tasa de escalada:** Una métrica de alto nivel que interesa a la gerencia, ya que indica cuántos problemas el _bot_ no pudo resolver.
    

### **Clasificación de métricas**

Clasificar las métricas ayuda a entender qué se debe medir, identificar las métricas más importantes y hacer seguimiento del progreso. Las métricas se pueden dividir en tres categorías:

1. **Métricas de experiencia de interacción:** Miden la interacción de los usuarios con el agente conversacional.
    
    - **Ejemplos:** Volumen por canal, intención, tiempo de manejo, número de turnos, tasa de escalada y tasa de abandono.
        
    - **Importancia:** Ayudan a seguir los objetivos estratégicos del negocio y a entender cómo el agente cumple con las metas.
        
2. **Métricas de diseño del agente:** Miden la calidad del agente en sí mismo.
    
    - **Ejemplos:** Tasa de "No Coincidencia" (`No Match`) y volumen de tráfico en páginas específicas.
        
    - **Importancia:** Indican dónde se pueden hacer mejoras y cómo el rendimiento cambia con nuevos lanzamientos.
        
3. **Métricas de preparación del _backend_:** Miden la capacidad de los sistemas de soporte para mantener las operaciones del agente.
    
    - **Ejemplos:** Fallos de _webhook_ y latencia.
        
    - **Importancia:** Están vinculadas a acuerdos de nivel de servicio (`SLA`) y son monitoreadas por sistemas de supervisión avanzados.

---

# Herramientas

### **Métricas y herramientas para el análisis**

- **Visión general de los resultados:** Muestra datos generales sobre las conversaciones, como las que tuvieron éxito, las que escalaron a un agente humano, o las que tuvieron errores de _webhook_.
    
- **Escalada de intenciones:** Permite identificar las intenciones que más a menudo llevan a una escalada humana. Puedes ver una tabla de las intenciones con más escaladas, así como un gráfico de series de tiempo para analizar la tendencia de escalada de una intención específica.
    
- **Sesiones:** El número total de veces que se detectó una intención. Un número alto indica que la intención se usa con frecuencia.
    
- **Tasa de escalada:** El porcentaje de sesiones donde una intención llevó a una escalada. Una tasa alta sugiere que el sistema tiene problemas para manejar esa intención, lo que causa frustración y requiere intervención humana.
    
- **Número de turnos (`Turns`):** El número de intercambios conversacionales donde se detectó una intención. Un número alto puede indicar que la intención es relevante para varios temas o que los usuarios la repiten de diferentes maneras.
    
- **Tasa de escalada de intención principal (`Head Intent Escalated`):** El porcentaje de escaladas para sesiones en las que la intención fue la "intención principal" (`head intent`). La intención principal es la que impulsa la conversación. Una tasa alta indica que es una intención crítica y que los errores en su manejo pueden tener un gran impacto en la satisfacción del cliente.
    

### **Cómo usar las métricas para optimizar**

- **Prioriza la mejora:** Al identificar las intenciones con la tasa de escalada más alta, puedes priorizar la refinación de su definición o la mejora de sus capacidades de **NLP** (`Natural Language Processing`).
    
- **Analiza tendencias:** Los gráficos de series de tiempo te ayudan a entender si la tasa de escalada está aumentando, disminuyendo o se mantiene estable.
    
- **Identifica patrones:** Analizando estas métricas juntas, puedes obtener una comprensión completa del rendimiento de una intención. Por ejemplo, una alta tasa de escalada en una intención muy usada sugiere que es una prioridad para mejorar el sistema.
    
- **Optimización:** Al abordar las intenciones con la mayor tasa de escalada, puedes reducir la frustración del usuario, mejorar la satisfacción del cliente y optimizar la capacidad del sistema para manejar consultas de manera efectiva.

---

# Troubleshoot
La **fase de diagnóstico (`Troubleshooting`)** se enfoca en identificar y resolver problemas comunes relacionados con el diseño del agente conversacional, como intenciones fuera de alcance, falta de coincidencias o respuestas faltantes.

---

### **Áreas de diagnóstico comunes**

Estas herramientas ayudan a depurar problemas en flujos de conversación y páginas:

- **Nombre de la intención (`Intent Name`):** Muestra el nombre de la intención que debería haber coincidido si estuviera dentro del contexto de la página actual. Ayuda a identificar intenciones faltantes o que necesitan ser refinadas.
    
- **Número de turnos (`Turns`):** Indica cuántas veces una intención debería haber sido activada. Ayuda a priorizar esfuerzos de solución de problemas.
    
- **Tasa de "No Coincidencia" (`No Match Rate`):** El porcentaje de turnos de conversación en una página que no resultaron en una coincidencia de intención. Una tasa alta indica que el sistema falla con frecuencia al identificar la intención del usuario en esa página, lo que puede llevar a respuestas irrelevantes o frustración.
    
- **Turnos de "No Coincidencia" (`No Match Turns`):** El número total de turnos sin coincidencia de intención en una página. Ofrece una medida cuantitativa de la frecuencia de estos eventos.
    
- **Respuestas vacías (`Empty Responses`):** El número de interacciones en una página donde el sistema no proporcionó ninguna respuesta. Esto puede deberse a definiciones de flujo incompletas, errores de configuración de enrutamiento o limitaciones del sistema. Una alta cantidad de respuestas vacías indica que el sistema no está manejando las interacciones de manera efectiva.
    
- **Sesiones de bucle de página (`Page Loop Sessions`):** El número de sesiones donde el sistema produjo la misma respuesta del agente al menos tres veces en la misma página. Esto sugiere que el sistema está atascado en un bucle, repitiendo la misma respuesta sin avanzar la conversación.
    

### **Factores que contribuyen a los problemas**

- **Coincidencia de intenciones:** Configuraciones de enrutamiento incompletas, definiciones de intenciones demasiado restrictivas, limitaciones en el **NLP** o uso insuficiente de información contextual.
    
- **Alta tasa de "No Coincidencia":** Definiciones de intenciones faltantes o restrictivas, capacidades limitadas de **NLP** o falta de pistas contextuales.
    
- **Respuestas vacías:** Definiciones de flujo faltantes, problemas de enrutamiento o limitaciones del sistema.
    
- **Bucles de página:** Errores en la lógica del flujo, definiciones de intenciones conflictivas o rutas de salida faltantes.
    

Abordar estos problemas puede mejorar la precisión de la coincidencia de intenciones, la eficacia de las respuestas, y asegurar una experiencia de usuario fluida y sin frustraciones.

---
# Errores de webhook

### **Áreas de solución de problemas**

La sección de solución de problemas ayuda a identificar y resolver problemas en flujos de conversación y páginas:

- **Nombre de la intención (`Intent Name`):** Muestra el nombre de la intención que debería haber coincidido si estuviera dentro del contexto actual. Esto ayuda a identificar lagunas en el flujo conversacional.
    
- **Giros (`Turns`):** Indica cuántas veces debería haberse activado una intención. Ayuda a priorizar esfuerzos de solución de problemas.
    
- **Tasa de "No Coincidencia" (`No Match Rate`):** El porcentaje de giros conversacionales que no resultaron en una coincidencia de intención para la página. Una tasa alta indica que el sistema falla frecuentemente en identificar la intención del usuario.
    
- **Giros con "No Coincidencia" (`No Match Turns`):** El número total de giros sin coincidencias de intención. Proporciona una medida cuantitativa de la frecuencia de estos eventos.
    
- **Respuestas vacías (`Empty Responses`):** El número de interacciones en una página donde el sistema no proporcionó ninguna respuesta del agente. Esto puede ocurrir por flujos incompletos o errores de configuración.
    
- **Sesiones en bucle en la página (`Page Loop Sessions`):** El número de sesiones donde el sistema repitió la misma respuesta al menos tres veces en la misma página, indicando que el sistema podría estar atascado en un bucle.
    

---

### **Errores de Webhook**

Los errores de _webhook_ ocurren cuando el sistema de IA conversacional falla al comunicarse con sistemas externos. Las causas comunes incluyen URL mal configuradas, problemas de red, discrepancias en el _payload_ o problemas de autorización.

**Métricas disponibles para analizar errores de Webhook:**

- **Nombre/etiqueta del _webhook_:** Identifica el _webhook_ específico que se está analizando.
    
- **Llamadas (`Calls`):** El número total de veces que se invocó el _webhook_.
    
- **Tasa de fallos (`Failure Rate`):** El porcentaje de invocaciones de _webhook_ que fallaron (excluyendo los tiempos de espera).
    
- **Tasa de tiempo de espera (`Timeout Rate`):** La proporción de invocaciones que excedieron el límite de tiempo de espera especificado.
    
- **Latencia promedio (`Average Latency`):** El tiempo promedio (en milisegundos) que tarda una invocación de _webhook_ exitosa en completarse (excluyendo tiempos de espera y errores).

---

# Análisis de flujo

### **Cómo analizar grandes volúmenes de tráfico**

Para obtener _insights_ valiosos de los datos, necesitas ir más allá de los números y hacer preguntas específicas.

1. **Define el problema:** Formula preguntas dirigidas basadas en métricas clave como patrones de tráfico, tasas de escalada y transferencias a agentes humanos.
    
2. **Consulta la documentación:** Familiarízate con los estándares de nombres de flujos e intenciones. Obtén la documentación de diseño del equipo de desarrollo, como el documento de requerimientos, el diseño lógico y físico, y las especificaciones del _webhook_.
    
3. **Determina un rango de rendimiento esperado:** Establece un rango aceptable para cada métrica. Por ejemplo:
    
    - Tasa de escalada de intención: Menos del 40%.
        
    - Tasa de escalada de página: Menos del 20% para páginas que no son de finalización.
        
    - Tasa de "No Coincidencia": Menos del 20%.
        
    - `No Responses / Loops`: Idealmente, cero.
        
    - Tasa de fallos de _webhook_: Menos del 1%.
        
    - Latencia de _webhook_: Menos de 500 milisegundos.
        
4. **Analiza métricas específicas:** Revisa las métricas asociadas a los flujos e intenciones más utilizados.
    
5. **Documenta observaciones:** Registra las observaciones clave para identificar tendencias y patrones que te ayuden a mejorar el agente.
    

### **Limitaciones del análisis**

- **Lectura manual:** Ofrece una comprensión profunda de las interacciones, pero es subjetiva y consume mucho tiempo.
    
- **Análisis de tendencias:** Identifica patrones generales y puede ser automatizado, pero podría pasar por alto conversaciones individuales.
    

Ambos métodos son útiles para entender y mejorar los agentes conversacionales, y la mejor opción es un enfoque híbrido que combine las dos.