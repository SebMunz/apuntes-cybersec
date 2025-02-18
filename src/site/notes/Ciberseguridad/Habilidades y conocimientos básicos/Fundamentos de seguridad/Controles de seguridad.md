---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Fundamentos de seguridad/Controles de seguridad/"}
---

# Security Controls
#### Controles de seguridad

Son protecciones diseñadas para reducir riesgos de seguridad. Incluye una amplia gama de herramientas para proteger activos antes, durante y después de un evento.

> Se organizan en tres tipos:
- Technical (Técnico):
  - Los controles técnicos incluyen tecnologías usadas para proteger activos. Como encriptación o sistemas de authenticación.

- Operational (Operacional)
  - Los controles operacionales mantinen el entorno seguro. Como por ejemplo entrenamientos al personal o respuestas de incidente.

- Managerial (Administrativo)
  - Los controles administrativos se centran en los otros dos para reducir riesgos. Como los procedimientos, políticas y estándares.
  
---

La privacidad de la información es importante en estas decisiones.
Los controles de seguridad se usan para regular la privacidad de la información.
La intención es siempre mantener el principio del mínimo privilegio ( *PoLP* )

Al aplicar el principio, es importante diferenciar entre el __dueño__ de la información y el __cuidador__ de la información.

El __dueño__ es quien puede acceder, editar, usar o destruir la información (salvo casos donde existen multiples dueños, como en propiedad intelectual).

El __cuidador__ es alguien -o algo- responsable del manejo seguro, transporte y almacenamiento de la información.

---
---
---
---

# PoLP
### Principle of Least Privilege (Principio del mínimo privilegio)

A grandes rasgos es un principio de otorgar la autorización y el acceso mínimo que requiere un agente para ejecutar una tarea. Es decir, limitar su acceso a la información sólo a lo que sea estrictamente necesario.
El principio se acomoda perfectamente a la [CIA TRIAD](https://github.com/SebMunz/Cybersec/blob/main/HabilidadesSeguridad/CIA%20triad.md).

#### La correcta aplicación de esto, implica:
    - Limitar el acceso a la información confidencial
    - Reducir la posibilidad de modificación, alteración o pérdida accidental de datos
    - Facilitar la supervisión y administración del sistema

Esto ayuda a disminuir considerablemente la probabilidad de ataque exitoso al conectar recursos específicos a determinados usuarios y limitar sus acciones.

---

#### Para implementarlo efectivamente son fundamentales las siguientes preguntas:
    - ¿Quién es el usuario en cuestión?
    - ¿Cuánto acceso requiere a un recurso específico?

Al responder estas preguntas, podemos definir correctamente los privilegios de cada usuario.
Sin embargo, es importante realizar auditorías periódicas de estas cuentas para mantener los sistemas seguros.

#### Los tres enfoques comunes para auditar:
  - Auditoría de uso
    - Se revisa qué recursos está accediendo cada cuenta y de que forma interactúan con estos recursos.
    - Ayuda a determinar si los usuarios están cumpliendo con las políticas de seguridad.
    - Permite identificar si un usuario tiene permisos que deberían ser revocados

  - Auditoría de privilegios
    - Su objetivo es evaluar si el rol de un usuario es acorde con los recursos que actualmente tiene acceso
    - Útil para eliminar el __arrastre de privilegios__

  - Auditoría de cambios de cuentas
    - Ayuda a asegurar que todas las modificaciones en las cuentas sean realizadas por usuarios autorizados
    - Suele realizarse a través del servicio de directorio de cuentas, utilizando los registros.
    - Un servicio de directorio óptimo se puede configurar para alertar sobre actividades sospechosas.

---
---
---
---

# Privacidad de la información

La privacidad se refiere a la protección contra el acceso y la difusión no autorizada.
La seguridad de la información (InfoSec) se refiere a la práctica de mantener los datos, en todas sus formas, alejados de usuarios no autorizados.

La diferencia clave está en que la privacidad proporciona a las personas control sobre su información personal y cómo ésta se comparte. La seguridad, en cambio, se trata de proteger las decisiones de las personas y mantener su información a salvo.


### Regulaciones

Existen ciertas leyes que se deben cumplir. Las regulaciones son normas establecidas por un gobierno u otra autoridad. Las regulaciones de privacidad existen para proteger a los usuarios de que su información sea recopilada, utilizada o divulgada sin su consentimiento. Dichas regulaciones suelen describir las medidas de seguridad mínimas que deben implementarse.

Algunas regulaciones más relevantes:

- [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Otras normativas e información susceptible#GDPR\|GDPR]] (Reglamento general de protección de datos)
  - Desarrollado por la UE, otorga a los propietaros de los datos el control total sobre su información personal (nombre, dirección, número de teléfono, información financiera e información médica. A veces se incluyen otras)
  - La normativa se aplica a cualquier empresa que maneje datos de ciudadanos o habitantes de la UE, sin importar dónde opere dicha compañía

- [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Otras normativas e información susceptible#PCI-DSS\|PCI-DSS]] (Estándar de seguridad de datos para la industria de tarjetas de pago)
  - Conjunto de normas de seguridad establecidas por organizaciones de la industria financiera
  - Su objetivo es asegurar las transacciones con tarjetas de crédito y débito contra el robo de datos y fraude

- [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Otras normativas e información susceptible#HIPAA\|HIPAA]] (Ley de transferencia y responsabilidad de los seguros médicos)
  - Ley de EEUU que obliga a proteger la información sensible de salud de la gente.
  - Prohíbe la divulgación de información médica de una persona sin su conocimiento y consentimiento.
  - A pesar de ser elaborada por EEUU para su mercado específico, sirve como base para muchas organizaciones del mundo.