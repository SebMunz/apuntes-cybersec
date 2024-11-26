---
{"dg-publish":true,"permalink":"/Ciberseguridad/Herramientas/Nmap/"}
---

Herramienta gratuita de código abierto usado para el descubrimiento de redes y auditoría de seguridad.

Nmap realiza, generalmente, los siguientes pasos:
1. Enumerar los  objetivos
2. Descubrir hosts vivos
3. Hacer una búsqueda DNS reversa
4. Escanear puertos
5. Detectar versiones
6. Detectar sistema operativo
7. Traceroute
8. Ejecutar scripts (si es que los hay)
9. Escribir los resultados

La sintaxis básica general es:
`nmap [tipo de escaneo] [opciones] {objetivos}`

Uso común:

Ping de descubrimiento más básico, no siempre funciona porque los dispositivos pueden no responder
`nmap -sn direcciónip`

Comprobación de puertos abiertos:
`nmap -p direccion_target`
Sin especificar puertos, escanea los 1000 más comunes. Generalmente sirve agregar 21 ftp, 22 ssh, 80 http, 443 https, 445 windows samba.

---
#### Enumeración básica

![](https://i.imgur.com/Y4kAnZV.png)
Lista de hosts que se van a escanear (parámetro `-sL`) sin hacer reverse dns (parámetro `-n`).

#### Nmap host discovery usando ARP

Cuando no se provee de opciones para descubrir hosts, nmap realiza el siguiente procedimiento por defecto: 

1. Cuando un usuario _privilegiado_ (sudo/root) intenta escanear en una red local (ethernet), Nmap usa ARP Request. 
2. Cuando un usuario _privilegiado_ intenta escanear objetivos fuera de la red local, Nmap usa ICMP echo requests, TCP ACK en puerto 80, TCP SYN al puerto 443 e ICMP timestamp request.
3. Cuando un usuario no privilegiado intenta escanear objetivos fuera de la red local, Nmap realiza un [[IT fundamentos/Conexiones y Redes/03 Capa de Transporte y Capa de Aplicación#Three-way handshake\|Three way Handshake]]

---

### Opciones y parámetros

Algunos ejemplos:
`-Pn` para no realizar el ping, ayuda a descubrir más opciones.
`--open` para entregar solo puertos abiertos
`--exclude` excluye ciertas direcciones o puertos
`-iL archivo` pasarle un archivo de lectura, generalmente para incluir una lista de ip
`-sV` determina el tipo de servicio y versión
`-T` modificar velocidad de escaneo de 0-5, 0 siendo la más lenta y segura, 5 la más agresiva.
`--min-rate` imponer una velocidad mínima de x paquetes por segundo.
`-v` verboso, va imprimiendo
`-O` (o de oso), determinar que SO corre el equipo pero suele dar falsos positivos
`-sS`
`-sC` incluir script
	`vuln` escanear usando los scripts con categoría vulnerable
`-sL OBJETIVO` Obtener una lista de hosts que nmap va a escanear (sin escanearlos). Sin embargo, va a realizar un reverse dns resolution para obtener los nombres. Si no queremos dicho escaneo, agregar
	`-n`
`-sn` Omitir el escaneo de puertos de sistemas vivos
`-PR` ARP Scan
`-PE` ICMP echo request
`-PP` ICMP Timestamp Scan
`-PM` ICMP Address Mask Scan
`sudo nmap -PS22,80,443 -sn MACHINE_IP/30` TCP SYN Ping Scan
`sudo nmap -PA22,80,443 -sn MACHINE_IP/30` TCP ACK Ping Scan
`sudo nmap -PU53,161,162 -sn MACHINE_IP/30` UDP Ping Scan
`-R` reverse-DNS lookup para todos los hosts

#to-do 