---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/06 Export data to BigQuery/"}
---

### **1. Filtros de exportación**

Antes de exportar, puedes usar los filtros disponibles en la interfaz de usuario de **Conversation Hub** para seleccionar solo las conversaciones que te interesan.

- **Filtros soportados:**
    
    - Conversaciones con un número de turnos específico.
        
    - Conversaciones manejadas por un ID de agente en particular.
        
    - Conversaciones dentro de un rango de fechas y horas determinado.
        
- **Nota:** Aunque es un paso opcional, filtrar te ayuda a manejar grandes volúmenes de datos. Si no aplicas ningún filtro, se exportarán todas las conversaciones.
    

---

### **2. Proceso de exportación a BigQuery**

La exportación puede realizarse tanto a través de la interfaz de usuario como de la API, aunque se recomienda usar la API para operaciones a gran escala.

1. **Crear una tabla de destino en BigQuery:**
    
    - Antes de iniciar la exportación, debes crear una tabla vacía en la consola de BigQuery.
        
    - No es necesario definir el esquema, ya que se generará dinámicamente durante el proceso de exportación.
        
2. **Iniciar la exportación desde la interfaz de usuario de Insights:**
    
    - En **Conversation Hub**, haz clic en el botón `Export`.
        
    - Revisa los filtros aplicados y el recuento de conversaciones.
        
    - Ingresa el conjunto de datos y el nombre de la tabla de BigQuery.
        
    - Inicia el trabajo de exportación, que es una operación de larga duración. Puedes monitorear su progreso en la esquina superior derecha del panel de Insights.
        
3. **Consideraciones adicionales para la API:**
    
    - La API te permite exportar un gran volumen de datos, superando las limitaciones de la interfaz de usuario.
        
    - Se pueden configurar opciones de sobrescritura o de añadir datos:
        
        - `WRITE_TRUNCATE`: Sobrescribe los datos de la tabla de destino (opción por defecto).
            
        - `WRITE_APPEND`: Añade los datos exportados a la tabla de destino existente.
            
    - La exportación es compatible con tablas protegidas por claves de encriptación gestionadas por el cliente (CMEK).
        

---

### **3. Esquema de datos exportados**

Una vez completada la exportación, los datos están disponibles en la tabla de BigQuery y pueden ser explorados.

- **Métricas a nivel de conversación:**
    
    - Nombre del tema (`topic name`).
        
    - Porcentaje de silencio (`silence percentage`).
        
    - Entidades identificadas (`entities`).
        
- **Métricas a nivel de frase/turno (`sentence level`):**
    
    - Puntuación de sentimiento (`sentiment score`).
        
    - Intención (`intent`).
        
    - Marcadores (`highlights`).
        
- **Métricas a nivel de palabra:**
    
    - Identificador del hablante (`speaker tag`).
        
    - Código de idioma (`language code`).