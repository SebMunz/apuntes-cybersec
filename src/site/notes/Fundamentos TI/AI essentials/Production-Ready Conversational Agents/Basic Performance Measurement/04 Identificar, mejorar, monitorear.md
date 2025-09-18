---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Basic Performance Measurement/04 Identificar, mejorar, monitorear/"}
---

# Índice

[[#Ídentificación]]
[[#Mejoramientos]]
[[#Monitoreo]]

---

# Ídentificación
La **fase de identificación** del ciclo de retroalimentación se centra en encontrar la causa raíz de los problemas de rendimiento del agente conversacional, en lugar de solo tratar los síntomas.

---

### **Proceso para identificar y priorizar causas raíz**

1. **Consolidar todos los problemas documentados:** Recopila todos los problemas identificados en las fases anteriores (entendimiento y análisis), incluyendo el _feedback_ de los interesados.
    
2. **Crear una declaración de problema única para cada asunto:** Redacta una declaración clara y concisa para cada problema, utilizando las 5 W (`quién`, `qué`, `cuándo`, `dónde`, `por qué`) para contextualizarlo.
    
3. **Documentar el estado actual:** Describe cómo funciona el sistema o proceso actual. Esto ayuda a identificar dónde se origina el problema.
    
4. **Determinar la causa raíz:** Identifica la razón subyacente de los problemas de rendimiento. Esto es crucial para lograr mejoras duraderas, en lugar de soluciones temporales.
    
5. **Clasificar las causas raíz:** Ordena las causas raíz identificadas según su gravedad e impacto. Una matriz que considere la dificultad de la solución y el tamaño del impacto en el tráfico de producción puede ser útil.
    

### **Cómo priorizar las optimizaciones**

Para optimizar el agente conversacional, prioriza las áreas que tienen un mayor impacto:

- **Áreas de alto tráfico o críticas para el recorrido del usuario:** Incluso las mejoras pequeñas pueden tener un gran impacto en la satisfacción del usuario y las tasas de finalización.
    
- **Optimizar las interacciones iniciales:** Asegúrate de que la claridad, el _engagement_ y la guía del usuario sean efectivos desde el principio.
    
- **Resolver "no coincidencias" (`no-match`):** Analiza las situaciones donde el agente no entiende al usuario para encontrar intenciones faltantes o reformular las existentes.
    
- **Analizar escaladas a agentes humanos:** Investiga las razones detrás de las escaladas, como respuestas confusas o bucles en la conversación.
    
- **Identificar puntos de abandono:** Comprende por qué los usuarios abandonan las conversaciones.
    
- **Mejorar la comunicación del agente:** Haz que el estilo de comunicación sea más claro y atractivo, y aborda las referencias ambiguas.
    
- **Enfocarse en áreas de alto impacto:** Prioriza el **NLP** y la comprensión de intenciones para refinar el _chatbot_ y hacerlo más útil y receptivo.
---

# Mejoramientos

La fase de **mejora** del agente conversacional se enfoca en optimizar cuatro áreas clave para un mejor rendimiento y una experiencia de usuario superior. Se requiere trabajar de cerca con el equipo de desarrollo para aplicar los cambios identificados en las fases anteriores.

---

### **Cómo mejorar el agente conversacional**

1. **Calidad del entendimiento del lenguaje natural (NLU):**
    
    - **Expande su conocimiento:** Mejora su capacidad para entender consultas comunes.
        
    - **Dirige las solicitudes:** Asegúrate de que las peticiones de los usuarios sean dirigidas a la intención correcta.
        
    - **Aprende de ejemplos reales:** Utiliza datos de conversaciones reales para refinar el sistema.
        
    - **Mejora la extracción de entidades:** Perfecciona la capacidad del agente para reconocer y extraer información clave (entidades) del texto.
        
2. **Experiencia del usuario:**
    
    - **Elimina lenguaje confuso:** Haz que las respuestas del agente sean claras y fáciles de entender.
        
    - **Mantén la consistencia:** Asegura que el tono y las respuestas sean consistentes.
        
    - **Recopila retroalimentación:** Usa los comentarios de los usuarios para refinar las interacciones.
        
3. **Integración con sistemas existentes:**
    
    - **Sincroniza respuestas:** Asegúrate de que las respuestas del agente coincidan con la lógica y los datos del _backend_.
        
    - **Maneja errores sin problemas:** Configura el agente para manejar los errores del _backend_ con explicaciones claras para el usuario.
        
    - **Asegura consistencia entre canales:** Mantén una experiencia de usuario consistente en todos los canales donde el agente esté activo.
        
4. **Pruebas y mejora continuas:**
    
    - **Pruebas regulares:** Realiza pruebas constantemente para detectar y corregir problemas de rendimiento.
        
    - **Recrea problemas pasados:** Usa las pruebas para replicar y solucionar errores anteriores.
        
    - **Evalúa el comportamiento:** Prueba el agente en una variedad de situaciones para entender cómo se comporta.
        
    - **Monitorea y mejora:** Rastrea el rendimiento del agente de forma continua para refinarlo a lo largo del tiempo.

---

En el proceso de mejora de un agente conversacional, se sigue un marco de trabajo de seis pasos para abordar un problema de rendimiento de principio a fin.

---

### **Proceso de mejora**

1. **Crea una declaración del problema:** Define el problema de manera clara y específica, incluyendo el dolor del negocio o del cliente y su impacto. Esto establece la base para todo el proceso.
    
2. **Documenta el estado actual:** Reúne datos sobre el rendimiento actual del agente, establece una línea de base y verifica cómo se están midiendo las métricas relevantes. Esto asegura que las mejoras se basen en evidencia concreta.
    
3. **Determina la causa raíz:** Usa técnicas como los **"5 porqués"** para ir más allá de los síntomas y encontrar la causa subyacente del problema. Lo ideal es encontrar una causa que se pueda solucionar de forma práctica.
    
4. **Desarrolla nuevas soluciones:** Con la causa raíz identificada, haz una lluvia de ideas para soluciones potenciales y evalúalas según su **impacto** y **dificultad**. Prioriza las soluciones que ofrezcan la mayor mejora con el menor esfuerzo.
    
5. **Prueba e implementa:** Antes de desplegar la solución a todos los usuarios, haz pruebas rigurosas en un entorno controlado. Puedes usar pruebas **A/B** para comparar el rendimiento antes y después de la implementación.
    
6. **Monitorea y mide los resultados:** Una vez que la solución está en producción, es crucial monitorear continuamente las métricas para asegurar que los cambios tuvieron el efecto deseado y para identificar cualquier consecuencia no intencionada u oportunidades de mejora.
    

---

Este es un proceso iterativo; si la solución no funciona, es importante volver a los pasos iniciales, aprender de los resultados y adaptar el enfoque. La colaboración del equipo es fundamental en cada etapa.

---

# Monitoreo

### **Detección de problemas de rendimiento**

Existen tres métodos comunes para detectar anomalías en el rendimiento:

1. **Umbrales (`Thresholds`):** Define límites absolutos (superiores e inferiores) para el rendimiento aceptable. Es simple, pero inflexible. Si los umbrales son demasiado altos, puedes pasar por alto problemas; si son demasiado bajos, puedes recibir falsas alarmas.
    
2. **Desviaciones estándar:** Analiza el rendimiento histórico y usa la desviación estándar para identificar cuándo un nuevo punto de datos se desvía significativamente de la media. Es más adaptable que los umbrales fijos, pero requiere más procesamiento.
    
3. **`N-daily`:** Compara el dato más reciente con el dato de `N` días atrás. Es ideal para detectar picos o caídas repentinas en el rendimiento, pero no es tan efectivo para detectar cambios graduales.
    

### **Proceso de monitoreo**

Para monitorear las soluciones implementadas y sus resultados, sigue estos pasos:

1. **Establece qué medir:** Define las métricas clave para el éxito (ej. satisfacción del cliente, tasa de finalización de tareas).
    
2. **Determina la frecuencia:** Decide con qué frecuencia se medirán estas métricas (diaria, semanal o mensual).
    
3. **Establece un proceso de revisión:** Crea un sistema para revisar los resultados de forma regular, como reuniones periódicas del equipo.
    
4. **Define las acciones:** Decide qué acciones tomarás si hay cambios inesperados en las métricas (ej. revertir una solución, ajustarla o crear una nueva).
    

Con el tiempo, es importante estar atento a los cambios en el comportamiento del usuario, la deriva en los datos de entrenamiento y los posibles problemas técnicos que puedan afectar el rendimiento del agente.

---

### **Cómo lidiar con los fallos**

Una máxima en Google es **"la esperanza no es una estrategia"** para los sistemas que operan a gran escala. Esto se aplica a los agentes conversacionales, _webhooks_ y APIs, que también son propensos a fallar. Para asegurar la resiliencia del sistema, debes:

- **Identificar riesgos:** Mapea escenarios de fallo comunes (ej. cortes de red, errores de autenticación).
    
- **Implementar estrategias de mitigación:** Desarrolla soluciones para cada riesgo, como implementar reintentos, usar URLs de respaldo y emplear mecanismos de autenticación robustos.
    
- **Evaluar la efectividad:** Usa las métricas del sistema, como la tasa de fallos, la tasa de `timeout` y la latencia promedio, para evaluar el impacto de los fallos y la efectividad de las estrategias de mitigación.
    

La preparación proactiva para los fallos y el uso de análisis de datos son esenciales para mantener la fiabilidad y el rendimiento de los sistemas de **IA conversacional**.