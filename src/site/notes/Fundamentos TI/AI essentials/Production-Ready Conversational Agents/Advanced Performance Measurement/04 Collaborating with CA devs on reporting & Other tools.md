---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Advanced Performance Measurement/04 Collaborating with CA devs on reporting & Other tools/"}
---

# Índice
[[#Colaboración]]
[[#Otras herramientas]]


---

# Colaboración

Para optimizar la analítica del rendimiento del agente, se recomienda trabajar en conjunto con los desarrolladores de **Dialogflow CX**. Se pueden usar **parámetros de sesión** para capturar información clave que haga que los reportes sean más impactantes.

---

### **Mejoras clave en el diseño de Dialogflow CX para _reporting_**

1. **Parámetro de sesión de evento:** Permite registrar el motivo de una llamada de forma de alto nivel, especialmente cuando la conversación tiene un resultado negativo o el usuario toma un camino inesperado. Se pueden usar cuatro categorías principales para clasificar los eventos de escalada:
    
    - **Solicitud de agente:** Cuando el usuario pide explícitamente ser transferido.
        
    - **Intentos máximos (`Max attempts`):**
        
        - **`Maxed intent collection`:** El _bot_ no pudo obtener la intención del usuario después de varios intentos.
            
        - **`Maxed ID collection`:** El _bot_ no pudo obtener la información de identificación del usuario.
            
        - **`Maxed no match`:** Demasiadas respuestas del usuario resultaron en "no coincidencia".
            
        - **`Maxed no input`:** El usuario no respondió después de varios intentos.
            
    - **Reglas de negocio:** El usuario no era elegible para el autoservicio o la lógica de negocio forzó la transferencia a un agente humano.
        
    - **Fallos de _webhook_:** Ocurrió un problema con el _webhook_.
        
        - **Fallo operativo:** Falla técnica con la integración.
            
        - **Fallo funcional:** El _webhook_ devolvió una respuesta incorrecta.
            
2. **Parámetro de sesión de intención principal (`Head Intent`):** Se recomienda que los desarrolladores marquen la **intención principal** en un parámetro de sesión para diferenciarla de las intenciones suplementarias. Esto facilita la correlación de los turnos de conversación con el objetivo principal del usuario.
    
3. **Parámetro de sesión del número de versión (`Version number`):** Añade el número de la versión del _bot_ como parámetro de sesión. Esto ayuda a correlacionar los errores con un despliegue específico, facilitando la resolución de _bugs_. También permite rastrear las nuevas características en el registro de cambios (`changelog`).
    

Estas mejoras permiten obtener datos más granulares y útiles para la analítica, y son el resultado de una colaboración efectiva entre los analistas y los desarrolladores.

---

# Otras herramientas
Hay otras herramientas que pueden complementar el análisis avanzado del _feedback loop_ de un agente conversacional. La principal de estas es **Colab**, un cuaderno **Jupyter** alojado, que en combinación con la **API** de **Dialogflow CX Scripting**, permite realizar un análisis profundo.

---

### **Herramientas para el análisis avanzado**

1. **Colab (Jupyter Notebook):** Es una herramienta de **Google Research** que te permite escribir y ejecutar código **Python** en un navegador, sin necesidad de configuración. Es especialmente útil para el análisis de datos.
    
2. **DFCX SCRAPI (`Dialogflow CX Scripting API`):** Una **API** de alto nivel para **Python** que facilita la construcción y el mantenimiento de _bots_ de **Dialogflow CX** a escala. Te permite realizar las siguientes tareas:
    
    - **Administración de recursos:** Crear, actualizar, eliminar, obtener y listar todos los tipos de recursos de **CX**.
        
    - **Análisis de datos:** Convertir los recursos de **CX** a **DataFrames** de `Pandas` para su análisis.
        
    - **Automatización:** Ejecutar conversaciones completas con un agente **CX** de forma automatizada.
        
    - **Extracción de información:** Obtener datos de validación e historial de cambios.
        
    - **Búsqueda:** Buscar un parámetro o frase específica en todos los flujos, páginas y rutas.
        
    - **Copia de recursos:** Mover recursos entre agentes de manera rápida.
        
3. **BigQuery:** Se usa para exportar los datos de **Dialogflow CX** y analizarlos.
    
4. **Looker Studio:** Se utiliza para crear paneles de visualización a partir de los datos en **BigQuery**.
    

### **Estrategia para el análisis del _feedback loop_**

1. **Integrar:** Conecta **Dialogflow CX** con **BigQuery** para tener los datos listos para el análisis.
    
2. **Analizar:** Usa **Colab Notebooks** y **DFCX SCRAPI** para leer los metadatos del agente y entender su diseño.
    
3. **Visualizar:** Crea paneles en **Looker Studio** a partir de las tablas de **BigQuery** para visualizar las métricas y los _insights_ de diseño.
    

La combinación de estas herramientas te permite ir más allá de las funcionalidades nativas de **Dialogflow** y obtener un entendimiento profundo del rendimiento del agente, lo que lleva a mejoras significativas en la experiencia del usuario.