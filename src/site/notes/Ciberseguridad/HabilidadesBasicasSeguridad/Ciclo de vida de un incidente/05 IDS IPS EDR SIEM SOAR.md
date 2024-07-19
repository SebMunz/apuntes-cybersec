---
{"dg-publish":true,"permalink":"/Ciberseguridad/HabilidadesBasicasSeguridad/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR/"}
---

# IDS, IPS y EDR

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

---

# SIEM

**Security Information and Event Management (SIEM)** es una herramienta integral que recopila, correlaciona y analiza registros (logs) de diferentes fuentes en una red para identificar y responder a amenazas de seguridad. Es fundamental para monitorear actividades críticas en una organización y proporcionar una visión en tiempo real de posibles amenazas.

1. **Recolección y agregación de información:**
   - Recopila registros de diversas fuentes, como sistemas de detección y prevención de intrusiones (IDS/IPS), bases de datos, firewalls, entre otros.
   - Centraliza estos registros en un repositorio central para un análisis más efectivo.

2. **Normalización de la información:**
   - Elimina la información redundante o no esencial de los registros.
   - Normaliza los registros para crear consistencia en el formato y facilitar su análisis.

3. **Análisis basado en reglas:**
   - Utiliza reglas predefinidas para analizar los registros y detectar posibles incidentes de seguridad.
   - Categoriza y/o informa las alertas generadas por estas reglas para su revisión por parte de los analistas de seguridad.

## SOAR

**Security Orchestration, Automation, and Response (SOAR)** es una plataforma que automatiza el análisis y la respuesta a eventos de seguridad e incidentes. Además de la automatización, SOAR también facilita la gestión y el seguimiento de casos de seguridad.

- **Automatización y orquestación:**
   - Permite la automatización de tareas repetitivas relacionadas con la detección y respuesta a incidentes de seguridad.
   - Coordina la ejecución de diferentes herramientas y procesos de seguridad para una respuesta más eficiente y coordinada.

- **Gestión de casos:**
   - Permite la creación y seguimiento de casos de seguridad que involucran múltiples incidentes o actividades relacionadas.
   - Proporciona una vista centralizada de todos los incidentes y acciones tomadas en respuesta a ellos.