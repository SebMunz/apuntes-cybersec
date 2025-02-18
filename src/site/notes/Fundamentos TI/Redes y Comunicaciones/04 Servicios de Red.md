---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/04 Servicios de Red/"}
---

# Resolución de nombres
## DNS
Domain Name System. Servicio de redes que resuelve cadenas de palabras en direcciones IP.
En palabras sencillas es casi como una guía telefónica donde nosotros le damos el nombre y lo traduce en la dirección IP numérica.
Por ejemplo la dirección www.google.com es más fácil de escribir y recordar que <a href="172.217.192.99">172.217.192.99</a>

A través del uso del DNS una empresa podría simplemente cambiar su dirección IP en el DNS para que redireccione correctamente.

Existen 5 tipos de servidor DNS:
- Caching
	- Almacena respuestas DNS anteriores para agilizar
- Recursive
	- Recibe solicitud del cliente, si no tiene respuesta en caché, consulta otros servidores DNS
- Root
	- Primer servidor consultado por el recursivo. Proporciona información sobre servidores Top-Level domain (TLD)
- TLD
	- Contiene información sobre dominios de nivel superior (.com, .org, .net, etc). Dirige al servidor autoritativo adecuado
- Authorative
	- Servidor con respuesta final sobre nombre de dominio. Devuelve la IP correspondiente.

El paso a paso para la petición es:
1. Cliente realiza solicitud DNS
2. Servidor recursivo recibe solicitud, si no tiene respuesta continua
3. Consulta root DNS
4. Consulta TLD DNS
5. Consulta al authorative DNS
6. Respuesta final
La mayoría de estos pasos se evitan si la respuesta se encuentra en caché.

# DNS Zones
La zona DNS es una porción del espacio DNS gestionada por una organización o administrador. A grandes rasgos es una base de datos que contiene los registros DNS para un dominio.

Los tipos principales son:
- Forward Lookup Zones
	- Convierte nombres de dominio en direcciones IP
- Reverse Lookup Zone:
	- Convierte las IP en nombres de dominio
## Componentes

### DNS Resource Records
Registros dentro del sistema DNS que almacena diferentes tipos de información asociada con un dominio, como direcciones IP, alias, servidores de correo, etc.
- *Un registro que asocia "ejemplo.com" con una dirección IP*

### DNS Round Robin
Técnica de balanceo de carga donde múltiples direcciones IP están asociadas a un solo nombre de dominio. Las solicitudes a ese dominio se distribuyen de manera rotativa
- *Si ejemplo.com tiene dos IP, el DNS alterna entre ambas para cada nueva solicitud, ayudando a distribuir el tráfico*

### Quad A
Registro DNS que mapea un dominio a una dirección IPv6
- *ejemplo.com podría tener asignado además una dirección IPv6*

### CNAME (Canonical Name Record)
Alias que apunta a un nombre de dominio a otro nombre de dominio. Se usa para que varias URL lleven al mismo destino.
- *www.ejemplo.com y shop.ejemplo.com ambos llevarían a ejemplo.com mediante el CNAME*

### MX Record (Mail Exchange)
Registro que indica qué servidores de correo electrónico deben recibir los correos enviados a un dominio.
- *ejemplo.com podría apuntar a mail.ejemplo.com indicando que los correos para ejemplo.com deben ir a ese servidor*

### SRV (Service Record)
Qué servidores específicos proporcionan servicios para un dominio, con puertos y prioridades. Útil para servicios como VoIP, IM, etc.
- *Registro SRV podría indicar que un servidor en el puerto 5060 proporciona el SIP (Session Initiation Protocol) en ejemplo.com*

### TXT Record
Registro que permite almacenar texto asociado a un dominio. Generalmente se usa para verificación de dominio o políticas de correo electrónico (SPF, DKIM)
- *Un registro TXT para ejemplo.com podría contener un valor de verificación para google*

### NS (Name Server Record)
Qué DNS son responsables de un dominio en particular
- *El NS para ejemplo.com puede apuntar a ns1.ejemplo.com y ns2.ejemplo.com que son los DNS responsables de resolver ese dominio*

### SOA (Start of authority record)
Registro que contiene información clave sobre la zona DNS de un dominio, como el servidor principal, información de contacto, número de serie y políticas de actualización del DNS
- *El SOA de ejemplo.com podría especificar que ns1.ejemplo.com es el servidor DNS principal y contiene detalles como cuándo deben actualizarse los registros en caché*

# DHCP
Protocolo de la capa de aplicación que automatiza la configuración de hosts en una red.
Con el DHCP una máquina puede pedirle al servidor DHCP toda la configuración automática.
En casos de que no necesitamos saber la dirección IP o que no la necesitamos fija es bastante útil **PERO** es importante configurarlo correctamente.

Para routers, servidores o equipo en general de red, una dirección IP estática es importante, todos los equipos conectados a una red necesitan saber en todo momento la IP de su gateway. Si el servidor DNS local está con problemas, necesitamos una forma de conectarnos a estos equipos a través de su IP. Pero en el resto de los equipos que se conectan no es tan relevante conocer o configurar manualmente su IP.
Tenemos tres configuraciones primordiales:
- Dynamic allocation
	- Otorga las direcciones IP automáticamente según un rango determinado
	- En este caso cada equipo tiene una IP distinta cada vez que se conecta
- Automatic allocation
	- El DHCP server mantiene una lista de IP que ha proporcionado anteriormente
	- En este caso cada equipo tiene una IP asignada dentro del mismo rango, de modo que cuando se conecta nuevamente se le vuelve a asignar la misma
- Fixed Allocation
	- Lista manual de direcciones MAC y su IP.
	- Según la configuración si no encuentra un match le asigna una IP usando dynamic o automatic, o rehusar enteramente la asignación.

## DHCP Discovery
Proceso para configuración del DHCP. Considerando que DHCP es capa de aplicación, necesita configurar cosas dentro de la capa de red. Para realizarlo utiliza el DHCP Discovery el cual consta de los siguientes pasos:

- DHCP client envía un DHCP discover message a la red. Dado que la máquina no tiene una IP y no sabe la IP del servidor DHCP, envía un broadcast específico.
	- El DHCP escucha UDP en el puerto 67 y los mensajes siempre salen del puerto 68
	- El mensaje DHCP se encapsula en un UDP Datagram, esto se encapsula en un IP datagram con destino `255.255.255.255:67` y origen `0.0.0.0:68`. Esto se transmite a toda la red local.
- El servidor DHCP examina su propia configuración y toma una decisión sobre qué IP otorgarle al cliente, si es que es posible.
- La respuesta se envía como un DHCP offer message con destino 255.255.255.255:68 y con la IP de origen con el puerto 67.
- Dado que la oferta es un broadcast, esto llegará a todos los equipos en la red pero el cliente original lo reconocerá como un mensaje dirigido hacia él ya que la oferta tiene un campo que especifica la dirección MAC del emisor.
- El cliente procesa la oferta y revisa qué IP le ofrece. Técnicamente puede rechazarla, por ejemplo en casos con más de un servidor DNS o en casos para aceptar un rango de IP, pero esto no ocurre frecuentemente.
- El cliente responde al DHCP Offer message con un DHCP request message. El DHCPRM básicamente es un "si".
	- Nuevamente se envía desde 0.0.0.0 hacia 255.255.255.255
- Servidor responde con un DHCPACK (DHCP Acknowledgment)
- Cliente recibe el mensaje y el network stack del equipo utiliza la configuración otorgada por el DHCP Server para configurar su propia red.
- Esto se conoce como DHCP Lease porque incluye un tiempo de expiración. Esto puede ser días o incluso menos. Cuando este tiempo acaba, se debe renegociar.

En síntesis:
1. Cliente envía Discover message.
2. Servidor responde con offer message si es posible
3. Cliente responde si acepta o no
4. Servidor envía un ACK y manda la configuración
5. Cliente acepta y configura

# NAT
Network Address Translation.
Modifica las direcciones IP en los paquetes de red mientras pasan por un router o firewall.

Tipos principales:
1. Static NAT: Mapeo 1:1 entre direcciones privadas y públicas
2. Dynamic NAT: Asigna dinámicamente direcciones IP públicas de un pool a direcciones privadas
3. PAT (Port Address Translation) o NAT Overload: Más común. Múltiples dispositivos internos comparten una IP pública (1:many)

Su función en seguridad es ocultar las direcciones internas, dificultando a los atacantes mapear la red interna. También actúa de firewall básico y conserva las IP públicas.
Por ejemplo en una red doméstica con dos o tres IP (por ejemplo 192.168.1.1, .2, .3, .x) salen de la red todas con la misma IP 203.0.113.1.

### Outbound Traffic
Tráfico de red que se origina dentro de una red local y se dirige hacia una red externa, típicamente internet. Se inicia la conexión dentro de la red a servicios externos y generalmente está habilitado por defecto en los firewalls. Podemos configurar sus políticas de seguridad para controlar el acceso a sitios o servicios específicos.
Es importante en seguridad para monitorear el tráfico saliente y detectar comportamientos anómalos.

### Port Preservation
Técnica en NAT que intenta mantener el mismo número de puerto en la traducción de direcciones.
Cuando un equipo inicia una conexión, NAT intenta usar el mismo puerto en la IP pública, pero si el puerto está ocupado, asigna el siguiente disponible. Esto de modo de facilitar la resolución de problemas y el rendimiento.

### Port Forwarding
En este caso redirige la comunicación de red de un puerto a otro. Esto permite que los servicios internos (como web server y juegos) sean accesibles desde internet. Su uso común es el de mapear puertos externos a servicios internos específicos, por ejemplo el puerto 8080 se podría configurar el router para enviar el tráfico de ese puerto a una IP interna + un puerto específico.
Esto permite exponer servicios internos de manera controlada.


## VPN
Tecnología que crea una conexión segura y encriptada sobre una red menos segura. Tiene diversos usos pero los tres más usados son el de acceso remoto seguro a redes corporativas, protección de datos en redes públicas y evasión de restricciones geográficas.

Su funcionamiento básico es:
1. Establece un túnel encriptado entre dispositivo del usuario y servidor VPN
2. Todo el tráfico del usuario se enruta a través del túnel
3. El tráfico sale desde el servidor VPN ocultando la ubicación real del usuario
Existe el site-to-site VPN que conecta redes enteras entre sí y el Remote Access VPN que permite a usuarios individuales conectarse a una red remota.

#### Tunneling
Proceso de encapsular un protocolo de red dentro de otro. Básicamente se encapsulan los datos de un paquete dentro de un nuevo paquete, esto se transmite a través de la red y se desencapsula en el punto de destino. Su uso más común es el de los VPN pero también sirve para atravesar firewalls con protocolos no permitidos y la de conectar redes incompatibles.
Protocolos comunes:
- IPsec
- L2TP
- PPTP
- OpenVPN

### Encapsulamiento
1. Los datos de la aplicación se pasan a la capa de transporte.
2. La capa de transporte añade su header (TCP, UDP, etc)
3. La capa de red añade su header (IP, etc)
4. La capa de enlace de datos añade su header y trailer
5. La capa física convierte los datos en señales.
#### Desencapsulamiento
1. La capa física recibe las señales y las convierte en datos
2. Cada capa subsiguiente elimina su cabecera y pasa los datos a la capa superior
3. Llegan los datos finales.

## Proxies
Servidor intermediario que actúa en nombre de los clientes para acceder a recursos de otros servidores. Comúnmente usado por usuarios para mantener anonimato y preservar la privacidad pero también es usado ampliamente por servidores para mejorar el rendimiento de sus servicios.
Más comunes:
1. HTTP Proxy:
	- Manejo de tráfico web HTTP/HTTPS
	- Comúnmente usado para filtrar contenido web
2. SOCKS Proxy:
	- Versátil, puede manejar varios tipos de tráfico
	- Útil para aplicaciones que no son web.
3. Transparent Proxy:
	- Intercepta y redirige el tráfico sin configuración del cliente
	- A menudo es usado por ISP para caché y filtrado
4. Anonymous Proxy:
	- Oculta la información del cliente al servidor de destino
	- Usado para proteger la privacidad en linea
#### Reverse Proxy
Actúa en nombre de los servidores manejando solicitudes de clientes antes de enviarlas a los servidores.
1. El cliente envía una solicitud que va dirigida al servidor.
2. Reverse Proxy intercepta la solicitud
3. Se reenvía al servidor apropiado
4. Servidor responde al proxy
5. Proxy envía la respuesta al cliente
Esto para el balanceo de cargas, caché de contenido estático, protección contra ataques [[Ciberseguridad/Ataques/Red#DDoS\|DDoS]], SSL termination (proceso de desencriptación del tráfico antes de pasarlo al servidor).

#### Load Balancing
Balanceo de cargas. Distribución del tráfico de red o solicitudes de aplicaciones entre varios servidores.
Su funcionamiento básico:
1. Solicitud llega al load balancer (generalmente un proxy)
2. El balanceador decide a qué servidor enviar cada solicitud según la siguiente configuración:
	- Round Robin: Distribución secuencial
	- Least Connections: Se envía a servidor con menos conexiones activas.
	- IP Hash: Asigna basándose en IP del cliente
3. Solicitud se procesa en el servidor
4. Respuesta se devuelve por el balanceador
Mejora el rendimiento, permite escalar horizontalmente añadiendo más servidores y facilita el mantenimiento sin tiempo de inactividad.

Los tres tipos más comunes son dispositivos físicos dedicados, soluciones software (como NGINX, HAProxy) y balanceadores [[Fundamentos TI/Servicios Cloud/Servicios en la nube\|Cloud]]

