---
{"dg-publish":true,"permalink":"/Ciberseguridad/Herramientas/Nmap/"}
---

Herramienta gratuita de código abierto usado para el descubrimiento de redes y auditoría de seguridad.

La sintaxis básica general es:
`nmap [tipo de escaneo] [opciones] {objetivos}`

Uso común:

Ping de descubrimiento más básico, no siempre funciona porque los dispositivos pueden no responder
`nmap -sn direcciónip`

Comprobación de puertos abiertos:
`nmap -p direccion_target`
Sin especificar puertos, escanea los 1000 más comunes. Generalmente sirve agregar 21 ftp, 22 ssh, 80 http, 443 https, 445 windows samba.

De aquí en adelante sólo son opciones y parámetros adicionales para acotar más la búsqueda.

Algunos ejemplos:
`-Pn` para no realizar el ping, ayuda a descubrir más opciones.
`--open` para entregar solo puertos abiertos
`--exclude` excluye ciertas direcciones o puertos
`-iL archivo` pasarle un archivo de lectura, generalmente para incluir una lista de ip
`-sV` determina el tipo de servicio y versión
`-T` modificar velocidad de escaneo de 0-5, 0 siendo la más lenta.
`--min-rate` imponer una velocidad mínima de x paquetes por segundo.
`-v` verboso, va imprimiendo
`-O` (o de oso), determinar que SO corre el equipo pero suele dar falsos positivos
`-sS`
`-sC` incluir script
	`vuln` escanear usando los scripts con categoría vulnerable
