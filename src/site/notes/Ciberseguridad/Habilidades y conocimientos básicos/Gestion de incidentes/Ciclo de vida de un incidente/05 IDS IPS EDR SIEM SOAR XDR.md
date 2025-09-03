---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR XDR/"}
---

# IDS, IPS, EDR, XDR

## IDS (Sistema de Detección de Intrusiones)

Un IDS, por sus siglas en inglés Intrusion Detection System, es una aplicación que monitorea los sistemas y la actividad de red, y produce alertas sobre posibles intrusos. Recolecta y analiza la información del sistema en busca de actividades anormales. Si detecta algo inusual, envía una alerta.

## IPS (Sistema de Prevención de Intrusiones)

Similar al IDS, un IPS (Intrusion Prevention System) no solo detecta intrusiones, sino que también proporciona acciones automatizadas para detenerlas. Es una medida más proactiva que no solo alerta sobre posibles amenazas, sino que también toma medidas para bloquearlas y prevenir daños.

## EDR (Detección y Respuesta de Puntos de Conexión)

EDR, por sus siglas en inglés Endpoint Detection and Response, es una aplicación que monitorea la actividad maliciosa en un punto de conexión. Se instalan en dispositivos conectados a una red, como computadoras, teléfonos, entre otros. Identifican, alertan y responden a actividades sospechosas. 

La principal diferencia con los IDS/IPS es que las EDR recopilan datos de actividad y realizan análisis de comportamiento para identificar patrones de amenazas. Además, utilizan automatización para detener ataques sin intervención manual.

Algunas herramientas populares de IDS/IPS/EDR incluyen:
- [Snort](https://www.snort.org/)
- [Zeek](https://zeek.org/)
- [Kismet](https://www.kismetwireless.net/)
- [Sagan](https://github.com/beave/sagan)
- [Suricata](https://suricata-ids.org/)

Algunas soluciones de EDR reconocidas incluyen:
- [Open EDR](https://www.opendedr.com/)
- [Bitdefender EDR](https://www.bitdefender.com/business/endpoint-detection-response/)
- [FortiEDR](https://www.fortinet.com/products/endpoint-security/fortiedr)

## XDR
Extended Detection and Response.



---

# SIEM

**Security Information and Event Management (SIEM)** es una herramienta integral que recopila, correlaciona y analiza registros (logs) de diferentes fuentes en una red para identificar y responder a amenazas de seguridad. Es fundamental para monitorear actividades críticas en una organización y proporcionar una visión en tiempo real de posibles amenazas.

## Características
1. **Recolección y agregación de información:**
   - Recopila registros de diversas fuentes, como sistemas de detección y prevención de intrusiones (IDS/IPS), bases de datos, firewalls, entre otros.
   - Centraliza estos registros en un repositorio central para un análisis más efectivo.

2. **Normalización de la información:**
   - Elimina la información redundante o no esencial de los registros.
   - Normaliza los registros para crear consistencia en el formato y facilitar su análisis.

3. **Análisis basado en reglas:**
   - Utiliza reglas predefinidas para analizar los registros y detectar posibles incidentes de seguridad.
   - Categoriza y/o informa las alertas generadas por estas reglas para su revisión por parte de los analistas de seguridad.

## Logs
Cada sistema SIEM tiene una forma diferente de ingerir logs.
- Agent / Forwarder: En estos casos la solución SIEM provee de una herramienta llamada Agent (forwarder en Splunk) que se instala en el Endpoint. Se configura para capturar todos los logs importantes y reenviarlos al servidor SIEM
- Syslog: Más común de los protocolos para recolectar información de varios sistemas como bases de datos, servidores web, etc. Todos ellos se envían en tiempo real al sistema centralizado.
- Subida manual: Algunas soluciones (como SPLUNK y ELK) permiten a un usuario enviarle información de forma offline para un análisis rápido. Cuando se ingresan los datos, estos son normalizados.
- Port-Forwarding: Se pueden configurar las soluciones SIEM para escuchar puertos específicos.
![](https://i.imgur.com/nz3v768.png)
Splunk

## Análista SOC y SIEM
SIEM es uno de los componentes más importantes de un centro de operaciones de seguridad
([[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/03 Roles#SOC (Security Operations Center)\|SOC]]).

Como analista SOC, utilizamos los SIEM para tener mejor visibilidad de lo que sucede en la red.
- Monitoreo e investigación
- Identificación de falsos positivos
- Modificación de reglas que provocan ruido o falsos positivos
- Reportes
- Identificación de puntos ciegos

![](https://i.imgur.com/pFI7JFc.png)
Qradar dashboard

En los dashboards de un SIEM podemos encontrar una diversidad de información como por ejemplo:
- Alertas notables
- Notificaciones de sistema
- Alertas de salud del sistema
- Listado de intentos de login fallidos
- Reglas disparadas
- [[PEGA/wip folder/TOP LEVEL DOMAINS (TLD)\|TOP LEVEL DOMAINS (TLD)]] visitados

## Reglas de correlación
Básicamente son expresiones lógicas que al ser gatilladas, disparan una alerta o ejecutan una acción particular.
Por ejemplo:
- Un atacante intenta eliminar logs para limpiar huellas. Un EVENT ID 104 ocurre cuando un usuario intenta eliminar logs de eventos. Para ello podriamos crear una regla que dispare una alerta cuando ocurre un event id 104:
	- `IF (log source = WinEventLog AND EventID = 104) {TRIGGER ALERT = "Event Log Cleared"} `
- Atacantes suelen usar el comando `whoami`, cosa que normalmente un usuario promedio no realiza. Podriamos crear una regla que dispare una alerta cuando se use el comando.
	- `IF (log source = WinEventLog AND EventID = 4688 AND NewProcessName HAS "whoami"){TRIGGER ALERT = "whoami command detected"`
*nota: usé pseudocódigo para claridad*

---

## SOAR

**Security Orchestration, Automation, and Response (SOAR)** es una plataforma que automatiza el análisis y la respuesta a eventos de seguridad e incidentes. Además de la automatización, SOAR también facilita la gestión y el seguimiento de casos de seguridad.

- **Automatización y orquestación:**
   - Permite la automatización de tareas repetitivas relacionadas con la detección y respuesta a incidentes de seguridad.
   - Coordina la ejecución de diferentes herramientas y procesos de seguridad para una respuesta más eficiente y coordinada.

- **Gestión de casos:**
   - Permite la creación y seguimiento de casos de seguridad que involucran múltiples incidentes o actividades relacionadas.
   - Proporciona una vista centralizada de todos los incidentes y acciones tomadas en respuesta a ellos.