---
{"dg-publish":true,"permalink":"/Ciberseguridad/HabilidadesBasicasSeguridad/Ciclo de vida de un incidente/03 Roles/"}
---

## Roles

### CSIRT (Computer security incident response teams)
es el grupo especializado en manejo de incidentes y respuesta.
Su objetivo es el de manejar incidentes, proveer servicio,recursos para la respuesta y recuperación y prevenir futuros incidentes.
**CSIRT** debe colaborar funcionalmente con todos los departamentos.

Roles internos:
- Analista de seguridad
  - Analizar y clasificar alertas
  - Investigar causa raíz
  - Escalar alertas a superiores o resolveras si no es necesario

- Responsable técnico
  - Gestionar aspectos técnicos del proceso (parches/actualizaciones)
  - Según la causa raíz, crear e implementar estrategias para contener, erradicar y recuperar.
  - Colaborar con otros equipos para asegurar la integridad del negocio

- Coordinador de incidentes
  - Coordinar tarea con deptos pertinentes

> Estos roles pueden variar según la organización

### SOC (Security Operations Center)
Unidad organizativa dedicada a monitorear redes, sistemas y dispositivos en busca de amenazas o ataques.
Suelen trabajar de forma independiente y/o dentro del CSIRT. Trabajan en conjunto con el blue team en algunas tareas.

Se organiza en tres niveles:
- Tier 1, **SOC ANALYST L1**
  - Monitoreo, revisión y priorizar alertas según gravedad
  - Crear y cerrar alertas utilizando tickets
  - Escalar tickets a L2 y L3

- Tier 2, **SOC ANALYST L2**
  - Investigación más profunda de los tickets escalados por L1
  - Configurar y perfeccionar herramientas
  - Reportar al lead.

- Tier 3, **SOC LEAD L3**
  - Gestionar las operaciones del equipo
  - Explorar métodos de detección más avanzados, como análisis forenses
  - Reportar al manager.

- Manager
  - Contratación, evaluación y entrenamientos de nuevos miembros
  - Métricas y gestionar rendimiento del equipo
  - Desarrollo de informes de incidentes, auditorías, normativas, etc
  - Comunicación con las partes interesadas

También hay más especializados:
- Forense (usualmente L2/L3)
  - Recopilación, conservación y analizar pruebas digitales relacionadas con incidentes de seguridad
- Threat hunter (usualmente L3)
  - Detección, analisis y defensa contra nuevas amenazas