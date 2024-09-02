---
{"dg-publish":true,"permalink":"/IT fundamentos/Nubes/Servicios en la nube/"}
---

### Servicios basados en la nube

Colección de recursos y capabilidades entregadas por internet a usuarios y organizaciones. Permite acceder, manejar, guardar, procesar información y aplicaciones remotamente sin preocuparse de comprar, mantener y sostener infraestructura física.

###### Categorías principales
- Software as a Service (SaaS)
- Platform as a Service (PaaS)
- Infrastructure as a Service (IaaS)


> SaaS
Aplicaciones front-end que los usuarios acceden a través del navegador web. El proovedor aloja, gestiona y mantiene el sistema de backend. Por ejemplo Google workspace, office 365, Salesforce

> PaaS
Herramientas de desarrollo de aplicaciones de backend para clientes. 
El proveedor aloja y mantiene el hardware y el software que las aplicaciones usan para funcionar.
Ejemplo Google App Engine, Heroku, VMWare Cloud

> IaaS
Acceso a una variedad de sistemas de backend alojados por el proovedor. Como procesamiento de datos, almacenamiento, recursos de redes y otros. Se suelen licensiar según necesidad (escalable).
Ejemplo Google Cloud, Azure, AWS

---

### Beneficios
Se elimina la necesidad de inversiones en hardware, software y mantención, sólo se paga lo que se usa y puede ser escalado o descalado.
Al ser escalable, los usuarios tienen virtualmente recursos ilimitados, por lo tanto pueden escalar o descalar sus organizaciones según necesidad.
Facilita el trrabajo remoto y la colaboración en equipo.
Son sistemas altamente fiables y redundantes.

### Consideraciones de seguridad
Crucial entender la responsabilidad del modelo compartido. Es decir, el proveedor se encarga de asegurar la infraestructura y el usuario de asegurar su propia información.

_Algunos puntos a considerar_
- Privacidad y protección
  - Asegurarse que el proveedor tiene medidas de seguridad adecuadas
- Control de acceso
  - Implementar sistemas fuertes de autenticación y mecanismos de control de acceso para evitar accesos no autorizados
- Encriptación
  - Utilizar la encriptación para proteger la información en tránsito y en descanso
- Monitoreo y alertas
  - Monitorear activamente los incidentes de seguridad y colocar alertas para identificar posibles errores
- Cumplimiento
  - Asegurarse que el proveedor cumple con los estandares regulatorios e industriales para tu organización

---

### SaaS
Software as a Service (SaaS - Software como servicio) es un sistema de software en la nube donde las aplicaciones se proveen a través de la internet.
No se instala ni se mantiene localmente en los computadores o servidores locales, los usuarios acceden a través de un navegador web.

###### Qué ofrece
- Accesibilidad
- Bajo Costo
- Actualizaciones automáticas
- Escalabilidad
- Modificación

###### Consideraciones de seguridad
- Guardado de la información
  - Asegurarse de utilizar un proveedor confiable
- Transmisión de información
  - Asegurarse de la encriptación durante su transmisión
- Control de acceso
- Disponibilidad del servicio
  - Asegurarse de tener planes de contingencia por si el proveedor tiene problemas

###### Consideraciones de proveedor
- Cumplimiento
- SLA
  - Revisar los Service Level Agreements del proveedor para entender sus garantias, estandares de funcionamiento y multas/regalias en caso de incumplimiento

---

### PaaS
Platform as a Service (PaaS - Plataforma como servicio), es un servicio en la nube que los desarrolladores usan para crear, subir o mantener aplicaciones.
Provee la plataforma de desarrollo y la infraestructura interna, como servidores, almacenamiento y recursos de internet.

###### Qué ofrece
- Escalabilidad
- Herramientas de desarrollo
- Gestión automatizada
- Económico

###### Usos comunes
- Desarrollo de aplicaciones
- Web Hosting
- Análisis de datos
- Desarrollo IoT

---

### IaaS
Infraestructure as a Service (IaaS - Infraestructura como servicio), servicio de computación en la nube que ofrece recursos virtualizados de computación a través de internet. Básicamente te permite arrendar infraestructura IT, como máquinas virtuales, almacenamiento y ancho de banda en una base de pagar-lo-que-se-usa.

###### Qué ofrece
- Máquinas virtuales escalables
- Almacenamiento gestionado
- Funciones de red flexibles
  - Como redes virtuales, subnets, configuración de IPs, VPN, etc.
- Seguridad
- Automatización e integración

###### Beneficios
- Económicos
- Flexibilidad y escalabilidad
- Despliegue rápido
- Confiable

###### Usos comunes
- Web Apps
- Desarrollo y pruebas
- Almacenamiento
- Big data y análisis