---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/NIST SP800/"}
---

Del NIST, instituto nacional de estándares y tecnología de EEUU.
El <a href="https://csrc.nist.gov/publications/sp800">NIST SP 800 (Special Publication 800)</a> es una serie de documentos publicados por el Instituto Nacional de Estándares y Tecnología (NIST) de los Estados Unidos que proporciona recomendaciones y guías detalladas en el campo de la seguridad informática y la gestión de riesgos de tecnología de la información.

A grandes rasgos, el NIST SP 800 incluye información sobre:
1. Seguridad de la Información
	- Guías para protección de sistemas informáticos
	- Mejores prácticas para ciberseguridad
	- Metodologías de gestión de riesgos
	- Controles de seguridad para diferentes tipos de sistemas
2. Criptografía
	- Estándares de encriptación
	- Recomendaciones para gestión de claves
	- Protocolos de seguridad criptográfica
3. Gestión de Riesgos
	- Frameworks para identificar y mitigar riesgos de seguridad
	- Evaluación de vulnerabilidades
	- Estrategias de respuesta a incidentes
4. Cumplimiento Normativo
	- Lineamientos para diferentes sectores (gobierno, salud, financiero)
	- Requisitos de seguridad para infraestructuras críticas

Su importancia radica en que:
- Es una referencia global para profesionales de ciberseguridad
- Proporciona estándares consensuados por expertos
- Ayuda a organizaciones a implementar prácticas robustas de seguridad
- Se actualiza constantemente para adaptarse a nuevas amenazas tecnológicas

# NIST 800-53r5
Una importante a mencionar es la <a href="https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf">800-53r5</a>.
Es un catálogo comprehensivo de controles de seguridad y privacidad para sistemas de información.
Posee una estructura compuesta por 20 familias de control de seguridad, aplicable a organizaciones de diversos sectores y fue diseñada pensada en sistemas federales de los EE.UU., sin embargo, es transferible a cualquier sistema.

Tiene un enfoque basado en riesgos, controles adaptables a diferentes niveles de impacto, integración de seguridad física y lógica, consideraciones de privacidad.

Las familias son:
- Administrative Control
	- Audit and Accountability (**AU**)
	- Awareness and Training (**AT**)
	- Configuration Management (**CM**)
	- Contingency Planning (**CP**)
	- Incident Response (**IR**)
	- Maintenance (**MA**)
	- Program Management (**PM**)
	- Risk Assessment (**RA**)
	- Security Assessment and Authorization (**CA**)
- Technical Controls
	- Access Control (**AC**)
	- Identification and Authentication (**IA**)
	- System and communications protection (**SC**)
	- System and information integrity (**SI**)
	- System and services Acquisition (**SA**)
	- System and services development (**SD**)
	- Program system and services development (**DS**)
- Physical Controls
	- Personnel Security (**PS**)
	- Physical and environmental protection (**PE**)
	- Media Protection (**MP**)
- Strategic Controls
	- Planning (**PL**)

Cada uno de ellos se subdividen en subcontroles, por ejemplo **PM** se subdivide en 16 subcontroles como inventario del sistema, arquitectura empresarial, plan de infraestructura crítica, políticas de privacidad en sitios web, etc.

La recomendación de mejores prácticas que nos entrega es el de entender los flujos de datos, dependencias del sistema y vulnerabilidades potenciales.
Los 4 pasos serían:
- **Descubrir y clasificar** la información sensible
- **Mapear** la información y los permisos
- **Administrar** el control de accesos
- **Monitorear** los datos, actividad de archivos y comportamiento de usuarios.

