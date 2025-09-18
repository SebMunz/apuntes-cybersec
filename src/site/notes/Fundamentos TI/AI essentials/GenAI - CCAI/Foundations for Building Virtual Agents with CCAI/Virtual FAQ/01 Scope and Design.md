---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Virtual FAQ/01 Scope and Design/"}
---

# Fases de implementación de un agente de almacén de datos

Implementar un agente de almacén de datos implica cuatro fases clave:

1. **Ámbito y diseño:** Definir los casos de uso, las experiencias del usuario y las fuentes de datos.
    
2. **Construcción:** El desarrollo técnico del agente.
    
3. **Pruebas:** Validar que el agente maneja los casos de uso y los escenarios imprevistos.
    
4. **Despliegue y optimización continua:** Recopilar comentarios y mejorar el agente basándose en ellos.
    

Las fases de pruebas y despliegue no se cubren en detalle aquí, pero son esenciales para la producción.

---

### **Fase 1: Ámbito y diseño**

Esta fase se centra en establecer los objetivos y el alcance del agente.

#### **1. Definir el problema y recopilar datos**

- **Declaración del problema:** Describe claramente el problema que el agente resolverá (ej., "Los clientes necesitan respuestas a preguntas complejas en nuestro sitio de asistencia pública que nuestra solución de búsqueda actual no cubre").
    
- **Recopilar datos:** Reúne toda la información relevante para las preguntas que el agente deberá responder (sitios web, documentos internos, materiales de capacitación, etc.).
    

#### **2. Determinar el alcance**

- **Tipo de información:** Decide si el agente debe usar solo información **pública** (disponible en internet) o también información **privada** (no disponible públicamente).
    
- **Capacidades:** Define qué preguntas debe responder el agente y cómo manejará aquellas que no pueda responder directamente.
    

#### **3. Definir la experiencia del usuario**

- **Viaje del cliente (`Critical User Journey` - CUJ):** Entiende la experiencia completa del usuario para los casos de uso más frecuentes (ej., un cliente navegando por productos y recibiendo una oferta de ayuda).
    
- **Canal de experiencia del usuario:** Considera cómo se formateará la respuesta según el canal (ej., listas con viñetas en texto vs. explicaciones verbales para voz).
    

#### **4. Identificar fuentes de datos relevantes**

- **Datos públicos:** Información disponible en internet. Son fáciles de implementar y cubren la mayoría de los casos de uso.
    
- **Datos privados:** Información no pública que requiere recopilación adicional para complementar la base de conocimiento del agente.
    

#### **5. Establecer criterios de éxito**

- **Precisión mínima:** Define un estándar de calidad y seguridad acordado.
    
- **Plan de mejora continua:** Establece un plan para iterar y mejorar el agente basándose en la retroalimentación.