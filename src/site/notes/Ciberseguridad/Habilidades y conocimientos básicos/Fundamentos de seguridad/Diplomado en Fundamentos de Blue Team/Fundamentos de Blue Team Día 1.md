---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Fundamentos de seguridad/Diplomado en Fundamentos de Blue Team/Fundamentos de Blue Team Día 1/"}
---

Apuntes parte del diplomado de fundamentos de Blue team de la USACH.

---

# Introducción y contexto general

El blue team es un equipo de respuesta y defensa en la ciberseguridad defensiva
Es responsable de la **defensa activa** de los sistemas. Sus funciones incluyen implementar medidas de seguridad, monitoreo de amenazas, respuesta a incidentes, investigación, etc.

Su ejecución es crucial para prevenir, detectar y responder y así mantener la integridad (y disponibilidad) de los sistemas.

La frecuencia y la sofisticación de los ataques cibernéticos va exponencialmente en aumento, como por ejemplos los ransomware que son cada vez más avanzados y amenazas persistentes avanzadas (APT).

La estrategia de seguridad defensiva ha cambiado de un enfoque reactivo a uno proactivo.

---

# Conceptos básicos de defensa

## Defensa en profundidad
Múltiples capas de seguridad para proteger activos críticos.

Hay que implementar controles de seguridad en diferentes niveles como en la red, aplicación, datos, etc. de modo que, si una capa falla, otras puedan detener la amenaza

Por ejemplo los firewalls, antivirus, MFA, cifrado de datos, políticas de seguridad, etc.

## NIST y SANS
Marcos de referencia y mejores prácticas.

[[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/NIST SP800\|NIST SP800]] y [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Marco CSF-NIST\|Marco CSF-NIST]]
Referencia del National Institute of Standards and Technology (EE.UU.) para la gestión de riesgos.
- Para aplicarlo hay que seguir el marco CSF que incluye 5 funciones.
	- Identificar
	- Proteger
	- Detectar
	- Responder
	- Recuperar

SANS es una organización que ofrece formación y recursos de ciberseguridad.
<a href="https://www.cyberaces.org/">Cursos gratuitos del SANS </a>

## Seguridad en capas
Es un enfoque que protege diferentes niveles de la infraestructura con controles específicos.
Las más comunes:
- Físicas: control de acceso a servers
- Red: Firewalls y segmentación
- Aplicación: Autenticación y MFA
- Datos: Cifrado y backups
etc

---
# Roles y Funciones del Blue Team

## Red, Blue & Purple Team

Red team simula ataques
Blue team defiende los sistemas
Purple team colabora con ambos, es un intermedio

Blue team tiene los siguientes enfoques:
- Defensa proactiva
	- Parches, firewalls, monitoreos
	- threat hunting
- Defensa reactiva
	- responde a incidentes (contención, erradicación, recuperación)
- Evaluación de riesgos
	- Identifica y analiza posibles amenazas y vulnerabilidades
- Respuesta a incidentes
	- Sigue protocolos para mitigar y resolver brechas de seguridad (basados en frameworks como el NIST-CSF)

## Roles blue team

### Analista de Seguridad
Monitoreo y análisis de eventos de seguridad.

Utiliza:
- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SIEM\|SIEM]]
	- Splunk, ELK Stack, QRadar
- Forense
	- EnCase, FTK, Autopsy
- Detección de Amenazas
	- Wireshark, Zeek/Bro

### SysAdmin
Configura y mantiene seguros los sistemas y redes
Aplica parches, gestiona firewalls, UAC, etc.

Utiliza:
- Configuración segura:
	- Nessus, OpenVAS
- Mantenimiento:
	- WSUS, Ansible
- Control de acceso
	- Active Directory, Okta

### Especialista en respuesta a incidentes
Lidera la respuesta a brechas de seguridad, coordina mitigación y analisa los ataques.

Utiliza:
- Respuesta a incidentes
	- TheHive, Cortex
- Análisis de ataques
	- [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/MITRE ATT&CK\|MITRE ATT&CK]]
- Coordinacion
	- 🤷‍♀️, Teams, slack, etc.

### Ingeniero de seguridad
Diseña e implementa soluciones de seguridad, analiza vulnerabilidades, integra herramientas defensivas, etc.

Utiliza:
- Diseño de defensas
	- Palo Alto Networks, Cisco Firepower
- Análisis de vulnerabilidades
	- Qualys, Tenable.io
- Integración de herramientas
	- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SOAR\|SOAR]] (Phantom, Demisto, etc)

---

# Herramientas y técnicas de Blue team

- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR\|Herramientas SIEM, ELK, QRadar, etc]]

- EDR/XDR (Endpoint detection and Response / Extended Detection and Response)
	EDR protege endpoints
	XDR extiende dicha protección a redes, nube y crreo
Por ejemplo Crowdstrike Falcon, SentinelOne, Microsoft Defender for Endpoint.

- Firewalls e [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#IDS (Sistema de Detección de Intrusiones)\|IDS]]

- Análisis de logs y detección de amenazas

- Análisis y monitoreo como wireshark para detectar anomalías

# Gestión de Incidentes y Respuesta

- [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Marco CSF-NIST\|Marco CSF-NIST]]
- Según el NIST el proceso de la respuesta de incidentes se realiza así:
	1. Preparación
		1. Desarrollo de planes y capacitación del equipo
	2. Detección y análisis
		1. Identificación de incidentes por monitoreo y análisis de indicadores de compromiso
	3. Contención
		1. Aislamiento del incidente
	4. Erradicación
		1. idem
	5. Recuperación
		1. Restablecimiento de sistemas y operaciones normales
	6. Lecciones aprendidas
		1. Documentación y mejora de procesos

---

# Threat Intelligence y Análisis de Amenazas
Incorporar datos de amenazas (como IoC) en las defensas para mejorar la detección y respuesta.
Por ejemplo ThreatConnect o MISP

[[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/MITRE ATT&CK\|MITRE ATT&CK]]

[[Ciberseguridad/Habilidades y conocimientos básicos/Fundamentos de seguridad/OSINT\|OSINT]]

