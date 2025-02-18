---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/06 Solución de problemas/"}
---

# Conectividad

## ICMP
Internet Control Message Protocol, se usa para enviar mensajes de error y operativos en una red IP. Envía paquetes con mensajes de error y sirve para diagnosticar problemas de conectividad y latencia. En general, su idea es/era la de entregar información interna solamente por lo que sus mensajes no son tan amigables para la lectura humana pero hay cosas que podemos extraer de él.

---

## PING
Ping es un comando disponible en casi todos los terminales. Envía un tipo especial de mensaje ICMP llamado 'echo request', básicamente una pregunta de "estás ahí? (ping)".
El ICMP devolverá un 'echo response' (pong).
A grandes rasgos mide el tiempo de respuesta entre dos dispositivos en red.
Su uso es generalmente así:
`ping [ip/dominio destino]`

![](https://i.imgur.com/ASmGedZ.png)
*Ejemplo de ping a 8.8.8.8 (servidor DNS de google) desde windows.*
``` 
Información:
	Destino (8.8.8.8)
	Largo mensaje ICMP en bytes (32 bytes) pregunta y respuesta.
	Tiempo demora (time)
	TTL restante (TTL)
Estadísticas:
	Paquetes enviados.
	Paquetes recibidos.
	Pérdidas.
	Tiempo promedio ida y vuelta.
```
#to-do 

## Traceroute
Permite descubrir el camino entre dos nodos, dando información sobre cada salto.
trabaja manipulando el campo TTL en el nivel IP. El primer paquete lo envía con TTL 1, luego 2 para el segundo y así sucesivamente.
![](https://i.imgur.com/eZrOC5I.png)
*Ejemplo traceroute a www.google.com desde linux*
```
-Número de salto
-Tiempo de ida y vuelta de los 3 paquetes que envía
-IP del dispositivo en cada salto y nombre de host si es obtenible
```
Importante mencionar que en Linux y mac, traceroute envía paquetes UDP a números de puerto muy altos. En windows (`tracert`) utiliza 'echo request' del ICMP pero en general su funcionamiento es similar.

Similar a traceroute tenemos mtr (linux/mac) y pathping.
mtr es la versión mejorada que combina ping y traceroute:
`mtr [ip/dominio]`
Pathping es la versión de windows con estadísticas detalladas:
`pathping [ip/dominio]`

Su uso general es identificar dónde se producen retrasos o pérdidas de paquetes en la red.

## Netcat (linux/mac) | Test-NetConnection (windows)
Se realiza en la capa de transporte.
`nc host puerto` ej:
`nc -z -v google.com 80` nos devuelve
![](https://i.imgur.com/UbOG5ZZ.png)
-z es zero input y -v de verboso.

En windows, si sólo entregamos `Test-NetConnection google.com` lo hará por defecto con un 'echo request' pero con datos adicionales.
![](https://i.imgur.com/hVuWGCm.png)
*ejemplo sin puerto y con -port 80, respuestas con claras diferencias*

Sirve para probar conexiones TCP/UDP, escaneo de puertos y transferencias de archivos.

Existen muchísimas más opciones para cada comando pero este es el uso más básico.

# Domain name resolution

## Nslookup
Útil para ejecutar las consultas DNS manualmente.
Uso básico: `nslookup host`
Pero además tenemos un uso más interactivo. Si no le damos host, accedemos a él.
Desde aquí podemos dar otras configuraciones para solucionar problemas. En este modo si escribimos `server` y una dirección, usará esa como servidor DNS.
También podemos escribir `set type= tipoderegistro` (como qwerty, MX, TXT, A)

## DIG
Domain Information Groper. Más potente y flexible para consultas DNS, disponible en UNIX.
`dig [dominio] [type]`
*type es tipo de registro, como en nslookup*

Su utilidad es para realizar consultas DNS más detalladas
## Host
Búsqueda de DNS, obteniendo su IP asociada a un dominio (o el dominio asociado a la IP)
`host [dominio]`

## /etc/hosts y C:\\windows\\system32\\drivers\\etc\\hosts
Archivo local que mapea nombres de host a direcciones IP.
Generalmente no es muy usado porque sobreescribe las resoluciones DNS, pero es importante revisarlo para asegurarnos de que no haya algún tipo de sobreescritura maliciosa

## FlushDNS
Limpia la caché DNS local del sistema forzando realizar nuevas consultas DNS

## /etc/resolv.conf
Linux solamente. Especifica los servidores DNS a utilizar.

# Otros comandos útiles
- `cp, copy, xcopy, robocopy`:
	- cp en linux, copy es el copy tradicional, xcopy es más avanzado y robocopy es más seguro, preciso y complejo.
- `fsck, chkdsk`:
	- comprobación del disco y reparación de errores
- `sfc`:
	- busca archivos corruptos de sistema y busca copias en caché para repararlos
- `format`:
	- clásico formateo
- `fdisk, diskpart`:
	- fdisk en linux, particionar disco.
- `shutdown`:
	- Apagar el computador de forma local o remota
- `winver`:
	- Versión de windows usada
- `lsb_release -a, uname -a`:
	- Similar al de windows. lsb_release muestra la ID del distribuidor, descripción, numero de versión y nombre código. uname muestra el kernel y otra información
- `whoami`:
	- muestra la sesión con la que estamos conectados
- `ipconfig, ip`:
	- ip en linux, muestra la configuración de la red.
- `pathping`:
	- envía un request a cada router en el camino del destino, revisa cada paquete para determinar donde se pierden paquetes
- `tracert, traceroute`:
	- traceroute en linux/mac, muestra la ruta de un paquete desde el usuario hasta el destino
- `netstat`:
	- estadísticas sobre la actividad de red y su configuración, como los sockets
- `nslookup`:
	- información de DNS
- [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.\|Gestión de archivos y grupos en linux]]
- [[Fundamentos TI/Sistemas Operativos/Linux/Gestión de servicios y almacenamiento en Linux\|Gestión de servicios y almacenamiento en linux]]
- `net user`:
	- agrega o modifica usuarios
- `net use`
	- desconecta un equipo de recursos compartidos y muestra una lista de conexiones de red
- `gpupdate`
	- actualiza las políticas de grupo
- `gpresult`
	- muestra los RSoP (Resultant set of policy) para un sistema
- `iperf`: mide el ancho de banda máximo TCP/UDP entre dos puntos
	- `iperf -s` para servidor
	- `iperf -c [ip_servidor]` para cliente
