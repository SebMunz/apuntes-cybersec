---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones y Redes/Puertos comunes/"}
---

Dado que la cantidad de puertos son 16bits, esto se traduce a 65.536 puertos numerados desde el 0

# Clasificación de puertos:
1. Well-Known Ports o de sistema:
	- Rango 0 ~ 1.023
	- Puertos reservados para aplicaciones bien conocidas como HTTP, FTP, SSH, etc.
		- Asignados y regulados por la IANA
	- Generalmente usados por servicios del SO o aplicaciones con privilegios elevados
2. Registered Ports o de usuario:
	- Rango 1.024 ~49.151
	- Puertos asignados a aplicaciones o servicios especificos por la IANA, no requieren privilegios elevados
		- Se usan para aplicaciones estándar como DDBB y juegos
	- Frecuentemente usados para aplicaciones y servicios que requieren una conexión dedicada
3. Dynamic/Private Ports o efimeros:
	- Rango 49.152 ~ 65.535
	- No están registrados oficialmente y son usados dinámicamente por aplicaciones para conexiones temporales.
	- Conexiones temporales usadas durante una sesión de red como un navegador web conectado a un servidor.

## Puertos importantes
#### Autenticación y Accesos
- 22 TCP SSH
	- Conexiones seguras a través de una red
- 443 TCP HTTPS
	- HTTP seguro
- 636 TCP LDAPS
	- LDAP seguro
- 1812 UDP RADIUS Authentication
	- Autenticación en redes
- 1813 UDP RADIUS Accounting
	- Contabilidad en redes
#### Correo Electrónico
- 25 TCP SMTP
	- Envío de email
- 110 TCP POP3
	- Recepción de email
- 143 TCP IMAP
	- Acceso a email
- 993 TCP IMAPS
	- IMAP seguro
- 995 TCP POP3S
	- POP3 Seguro
#### Servicios web y redes
- 53 TCP/UDP DNS
	- Protocolo para resolución de nombres de dominio
- 80 TCP HTTP
	- Protocolo para navegación web no segura
- 443 TCP HTTPS
	- HTTP Seguro
- 8080 TCP HTTP Alternativo
	- Comunmente usado para proxy y web apps
- 8443 TCP HTTPS Alternativo
	- Para webapps con SSL/TLS
#### Bases de datos
- 1433 TCP Microsoft SQL Server
	- Conexión a DDBB
- 3306 TCP MySQL
	- Conexión a DDBB
- 5432 TCP PostgreSQL
	- Conexión a DDBB
#### Servicios de red y monitoreo
- 514 UDP Syslog
	- Registro de eventos de red
- 161 UDP SNMP
	- Administración de red
- 162 UDP SNMPTRAP
	- Notificaciones SNMP
#### VPN y Secure Tunnel
- 1194 UDP OpenVPN
- 1701 UDP L2TP
	- Protocolo de túnel para redes privadas virtuales
- 1723 TCP PPTP
	- Protocolo de túnel P2P
- 4500 UDP IPsec NAT-T
	- Usado en VPN IPsec para atravesar NAT