---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/06 Model Evaluation/"}
---

- **Objetivo:** Entender cómo identificar las métricas clave para determinar el éxito de los resúmenes de conversaciones.
    
- **Métricas clave de evaluación:**
    
    1. **Precisión (`Accuracy`):**
        
        - Mide la veracidad del resumen.
            
        - **Escala:** 1 (No tiene relación con la conversación) a 5 (Cada detalle es verdadero).
            
    2. **Integridad (`Completeness`):**
        
        - Evalúa si se omitieron detalles importantes.
            
        - **Escala:** 1 (Se omitieron todos los detalles importantes) a 5 (Es un resumen completo).
            
    3. **Cumplimiento (`Compliance`):**
        
        - Mide si el resumen se adhiere a las reglas de escritura predefinidas (ej. formato, secciones).
            
        - **Escala:** 1 (Incumplimiento total) a 5 (Adherencia perfecta).
            
    4. **Gramática y ortografía (`Grammar and Spelling`):**
        
        - Mide la calidad lingüística del resumen.
            
        - **Escala:** 1 (Oraciones sin sentido) a 5 (Gramática y ortografía perfectas).
            
- **Consideraciones adicionales:**
    
    - Estas métricas son pautas para asegurar que los resúmenes sean coherentes, respetuosos, imparciales e informativos.
        
    - Ayudan a mantener un alto estándar de calidad.
        
    - El sistema también utiliza la métrica **ROUGE-L** para la evaluación automática, que mide la superposición de unidades (palabras, frases) entre el resumen generado por el modelo y los resúmenes de referencia creados por humanos.
        
    - Un puntaje de **ROUGE-L** superior a 40% se considera un buen resultado para un modelo de resumen personalizado.