---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/Ciclo de Red/01 Tráfico de redes/"}
---

# Tráfico de red

Monitorear y comprender las inconsistencias en el tráfico de red es fundamental para garantizar la seguridad de una organización. El análisis de flujos de datos permite identificar anomalías en el tráfico y detectar posibles incidentes de seguridad mediante el uso de Indicadores de Compromiso (IOC), que son evidencias observables de un potencial incidente.

Por ejemplo, la exfiltración de datos, que implica la transmisión no autorizada de información desde un sistema comprometido, puede detectarse al observar un aumento inusual en el tráfico saliente desde un host.

## Formas de monitoreo

1. **Línea base:**
   - Se establece una referencia de tráfico promedio esperado.
   - Se investiga cualquier tráfico que salga excesivamente de esta línea base o se mantenga constantemente cerca de ella.

2. **Análisis de flujo:**
   - Observa el movimiento de comunicaciones en la red, incluyendo paquetes, protocolos y puertos.
   - Detecta actividades sospechosas, como el uso de un comando y control (C2) por parte de un agente de amenazas.

3. **Información de la carga del paquete:**
   - Analiza los detalles de los paquetes, como direcciones de origen y destino, así como la información de su carga.
   - Identifica actividades inusuales que puedan indicar un incidente de seguridad.

4. **Patrones temporales:**
   - Identifica los momentos en que ocurren flujos de tráfico masivos.
   - Las actividades fuera de los patrones temporales normales pueden indicar posibles amenazas.

## Protección

Además de los Centros de Operaciones de Seguridad (SOC), los Centros de Operaciones de Red (NOC) también desempeñan un papel crucial en la monitorización y el mantenimiento de la red.

Algunas herramientas comunes para el monitoreo incluyen:

- **IDS (Sistema de Detección de Intrusiones):**
  - Monitorean la carga útil del paquete para detectar intentos de phishing o malware.

- **Analizadores de protocolo de red (packet sniffer):**
  - Capturan y analizan el tráfico de datos dentro de la red.
  - Herramientas populares incluyen Wireshark y tcpdump.

Las organizaciones pueden monitorear diversos componentes de red y utilizar técnicas específicas para detectar posibles amenazas. Para obtener más información sobre estos componentes y técnicas, se pueden consultar las siguientes referencias:

- [Componentes de red monitoreables por las organizaciones](https://attack.mitre.org/datasources/DS0029/)
