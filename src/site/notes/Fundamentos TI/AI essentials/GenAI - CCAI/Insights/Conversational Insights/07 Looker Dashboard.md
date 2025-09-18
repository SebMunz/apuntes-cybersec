---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Insights/Conversational Insights/07 Looker Dashboard/"}
---

# Utilidad de los dashboards de Looker

- **Visión holística del negocio:** **Conversational Insights** se integra con **Looker Blocks** para agregar datos que van más allá de las fuentes del centro de contacto, lo que te permite tener una visión más completa de la situación del negocio.
    
- **Análisis en profundidad:** La flexibilidad del modelo de datos de Looker te permite combinar los datos de Insights con otros datos propios para obtener información de negocio más profunda.
    
- **Configuración:** Para usar esta integración, necesitas exportar los datos de Insights a **BigQuery** (como se vio en el módulo anterior) y programar un trabajo (`scheduled job`) o integrar **Cloud Data Fusion** para mantener la información actualizada.
    

---

### **Looker Blocks de Google Contact Center**

Looker ofrece **Looker Blocks** prediseñados para **Virtual Agents**, **Agent Assist** e **Insights**, que incluyen visualizaciones y modelos de datos.

Los componentes principales de estos bloques son:

1. **Modelo de datos:**
    
    - Traduce el esquema de exportación de **Conversational Insights** para que sea compatible con Looker.
        
    - Permite la personalización de las métricas para que se ajusten a tus necesidades.
        
2. **`One Explore`:**
    
    - Una interfaz de _point-and-click_ que facilita la exploración de datos sin necesidad de escribir código.
        
    - Permite realizar consultas puntuales de forma rápida y flexible.
        
3. **Dashboards prediseñados:**
    
    - **`Call Center Overview`:** Un _dashboard_ de alto nivel para ejecutivos, que resume los indicadores clave de rendimiento del centro de llamadas.
        
    - **`Agent Performance`:** Muestra métricas detalladas del rendimiento de cada agente, lo que facilita el seguimiento individual.
        
    - **`Conversation Lookup`:** Permite un análisis a nivel granular de las interacciones, mostrando la transcripción completa de la conversación y el análisis de sentimiento.