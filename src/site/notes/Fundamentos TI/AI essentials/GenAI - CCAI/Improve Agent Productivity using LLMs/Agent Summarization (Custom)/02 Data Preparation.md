---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Agent Summarization (Custom)/02 Data Preparation/"}
---

#### **Fase de preparación de datos**

- Es una etapa crucial que establece la base para un resumen de conversaciones efectivo.
#### **Pasos principales**

1. **Adquisición de datos de conversaciones:**
    - **Cantidad ideal:** Se necesitan 2,000 conversaciones con resúmenes de alta calidad.
    - **Cantidad mínima para empezar:** Con 1,000 conversaciones también se puede comenzar.
2. **Etiquetado de los datos:**
    - El objetivo es crear resúmenes que sean **concisos**, **precisos** y que estén bien escritos.
    - No es problema si la conversación original contiene algo de "ruido".
3. **Revisión de los datos etiquetados:**
    - Es un control de calidad.
    - El formato requerido para los datos de conversación de texto es **archivos JSON**, donde cada archivo contiene una sola conversación.
4. **Conversión a TF Record y JSON Conversations:**
    - Los datos se convierten a estos formatos.
    - Posteriormente, se almacenan en **Google Cloud buckets** para que estén listos para los siguientes pasos.

