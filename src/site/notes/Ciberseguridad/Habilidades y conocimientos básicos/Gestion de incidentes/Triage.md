---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Triage/"}
---

## Triage en Ciberseguridad

El triage es un proceso en la gestión de incidentes de seguridad. Permite evaluar, priorizar y asignar recursos para manejar amenazas de manera eficiente.
### Objetivos

1. **Identificación**: Detectar y registrar incidentes.
2. **Priorización**: Evaluar la gravedad e impacto potencial.
3. **Asignación**: Derivar incidentes a los equipos adecuados.

### Pasos

1. **Recepción del Incidente**: Recopilar información inicial.
2. **Evaluación Inicial**: Analizar tipo y alcance del incidente.
3. **Clasificación**: Categorizar según la gravedad (alta, media, baja).
4. **Priorización**: Basar en impacto al negocio y sensibilidad de datos.
5. **Asignación**: Enviar al equipo adecuado para su resolución.

### Herramientas

- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SIEM\|SIEM]]: Recopilación y análisis de datos de seguridad.
- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SOAR\|Plataformas SOAR]]: Orquestación y automatización de respuestas.
- **Herramientas de Ticketing**: Gestión y seguimiento de incidentes.

### Mejores Prácticas

- **Formación Continua**: Mantener al equipo actualizado en amenazas y técnicas.
- **Automatización**: Implementar soluciones para incidentes repetitivos y de bajo riesgo.
- **Revisión Periódica**: Evaluar y actualizar procesos regularmente.

### Recepción y evaluación

En este paso debemos recopilar la información, logs, revisión de la alerta de un IDS y validarla.
Para validarla debemos evaluar, según la información recopilada, si es que es algo a lo que debemos poner atención. Por ejemplo podemos preguntarnos:
- ¿Es un falso positivo?
- ¿Cual es la gravedad de la alerta?
- Dicha alerta, ¿es por una vulnerabilidad conocida?

### Asignar

Asignamos la prioridad según lo evaluado y según los criterios que generalmente se manejan internamente. Por ejemplo:
- Impacto funcional: ej. un [[Ciberseguridad/Ataques/Malware#**Ransomware **\|Ransomware]] impacta la confidencialidad, disponibilidad e integridad de los sistemas.
- Impacto informacional: ej. durante una [[Fundamentos TI/Redes y Comunicaciones/Ciclo de Red/02 Exfiltracion\|Exfiltración]] los atacantes pueden robar datos confidenciales que pueden pertenecer a entidades externas.
- Recuperabilidad: En algunos casos la recuperación de un ataque no puede ser posible, como cuando dichos datos exfiltrados son hechos públicos. En este caso puede ser un desperdicio dedicar recursos y tiempo a la recuperación de dichos datos, ya han sido públicos.

### Recopilar y analizar

Realizar un análisis exhaustivo del incidente. Implica recopilar de pruebas, investigaciones externas y documentación del proceso. El objetivo es recopilar lo suficiente para tomar una decisión informada para atender el incidente.

---
En síntesis, es lo mismo que el Triage en salud pero llevado y aplicado a la ciberseguridad, categorizando los incidentes en gravedad y derivando a quien sea más acorde en la escala al incidente.