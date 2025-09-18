---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Advanced Performance Measurement/03 Creating custom dashboards in Looker studio/"}
---

# Índice

[[#Transición]]
[[#Intent]]
[[#Webhook Performance]]

---

# Transición

Puedes crear **paneles reutilizables** (`reusable dashboards`) para que otros equipos puedan auto-servirse en su propio análisis. Uno de los más flexibles se centra en las **transiciones del agente**, que son intercambios específicos entre el usuario y el agente.

---

### **Panel de transiciones del agente**

Una **transición** se define por tres elementos clave:

1. **El turno anterior del agente:** Lo que el agente preguntó.
    
2. **La entrada actual del usuario:** Lo que el usuario respondió.
    
3. **El siguiente turno del agente:** Adónde va el agente en la conversación.
    

Este panel se puede usar para entender:

- La efectividad del agente para entender la intención del usuario.
    
- La capacidad del agente para manejar el contexto y mantener una conversación coherente.
    
- La fluidez y naturalidad del diálogo.
    

El panel está organizado en dos partes:

- **Parte superior:** Muestra las páginas y la intención detectada en el medio. Puedes ver lo que el agente preguntó y adónde fue en el flujo.
    
- **Parte inferior:** Muestra las respuestas más comunes del agente y las frases de los usuarios.
    

Este panel es versátil. Puedes usar filtros para:

- Investigar qué páginas llevan más a menudo a la finalización de la sesión.
    
- Entender las frases del usuario que causan un comportamiento específico, como los casos de "no coincidencia" (`no match`).
    
- Realizar un análisis de agrupación simple para ver la frecuencia de ciertas conversaciones.

---

# Intent

El panel **`Intent Launch`** (`Lanzamiento de Intención`) es una herramienta para monitorear el rendimiento del agente conversacional en función de diferentes métricas, desglosadas por intenciones principales. Se divide en tres secciones principales para dar una visión completa y detallada.

---

### **Secciones del panel `Intent Launch`**

1. **Resumen de alto nivel:** Muestra una visión general del rendimiento del agente. Compara las métricas clave, como el volumen de conversaciones, las tasas de intento y éxito de autoservicio, y la tasa de escalada, con un período anterior. Esto permite identificar rápidamente si el rendimiento está mejorando o empeorando.
    
2. **Métricas por intención principal (`Head Intent`):** Desglosa las mismas métricas de la sección anterior por intención principal. Ayuda a ver qué intenciones tienen el mayor impacto en la experiencia del usuario. Por ejemplo, te permite identificar si una intención específica está causando una alta tasa de escalada.
    
3. **Rendimiento de intenciones específicas a lo largo del tiempo:** Permite profundizar en el rendimiento de una intención individual. Al seleccionar una intención, puedes ver una cronología detallada de sus métricas. Esto es útil para detectar tendencias a largo plazo y encontrar áreas precisas para optimizar.
    

El panel también incluye opciones para dividir los datos por dimensiones adicionales, como el producto, el tipo de facturador o el evento, para investigar las causas detrás de los cambios en el rendimiento. En resumen, esta herramienta te ayuda a tomar decisiones basadas en datos para optimizar el agente y mejorar la experiencia del usuario.

---

# Webhook Performance

Para supervisar la funcionalidad del agente conversacional, se puede usar un panel de rendimiento de _webhook_ que analiza las métricas clave de estos canales de comunicación. Esto ayuda a identificar cuellos de botella y garantizar una experiencia fluida para el usuario.

---

### **Panel de rendimiento de _webhooks_**

Este panel se enfoca en tres áreas principales:

1. **Estado general del _webhook_:**
    
    - **`Trigger Count` (Conteo de activaciones):** Mide la frecuencia con la que un _webhook_ se activa. Un número alto indica una actividad intensa del agente.
        
    - **`Failure Rate` (Tasa de fallos):** Rastrea el porcentaje de envíos que fallan. Una tasa elevada sugiere problemas con la configuración o con la aplicación que recibe la información.
        
2. **Rendimiento de entrega:**
    
    - **Percentiles:** Los percentiles **P50**, **P90** y **P99** muestran la distribución de la latencia (el tiempo que tarda en llegar la información a su destino). Esto permite entender la velocidad típica de entrega e identificar valores atípicos que causan retrasos.
        
3. **Análisis de fallos:**
    
    - **Fallas operativas:** Ocurren cuando el _webhook_ no funciona correctamente (ej. errores de red o de servidor).
        
    - **Fallas funcionales:** Ocurren cuando el _webhook_ se entrega con éxito, pero no produce el resultado deseado debido a problemas como una carga de datos incorrecta (`payload`) o errores de lógica.
        

El panel también puede mostrar qué parámetros de sesión fueron actualizados por un _webhook_, lo que ayuda a ver cuán común es un valor específico.


---

