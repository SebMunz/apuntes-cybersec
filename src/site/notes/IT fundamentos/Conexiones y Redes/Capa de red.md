---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones y Redes/Capa de red/"}
---

# Operaciones en la Capa de Red

**Funciones en la Capa de Red**

> Las funciones en la capa de red se centran en organizar la dirección y entrega de paquetes de datos a través de la red e Internet. Esto implica dirigir paquetes de un enrutador a otro mediante la dirección IP de destino y almacenar esta información en tablas de enrutamiento. Todos los paquetes de datos incluyen una dirección IP, y un router utiliza esta dirección para enrutarlos.

### Diferencia entre IPv4 e IPv6

- *Longitud de Direcciones:*
  - IPv4: 4 bytes, hasta 4.3 mil millones de direcciones.
  - IPv6: 16 bytes, hasta 340 undecillones de direcciones.
- *Encabezado del Paquete IPv6:*
  - Más simple que el IPv4, con campos como etiqueta de flujo y clase de tráfico.
- *Seguridad:*
  - IPv6 ofrece enrutamiento más eficiente y elimina colisiones de direcciones privadas.

# Capa de Red

# IPv4
Número de 32bit distribuidos en hasta 4 octetos descritos normalmente en numeros decimales. Estas se distribuyen ampliamente a todo el espectro. Por ejemplo, IBM tiene todas las IP que tienen el número 9 como el primer octeto, de este modo, si un equipo debe enviar información a una dirección 90.0.0.1, sólo debe saber que debe llegar a un router de IBM, y ese router se preocupará del resto.

Las IP corresponden a las redes y no a los equipos. El equipo posee una dirección MAC que nunca cambia, independiente del lugar; pero su dirección IP será asignada de forma distinta según dónde se encuentre, generalmente asignada por un protocolo DHCP.

## IP Datagram
Similarmente al [[IT fundamentos/Conexiones y Redes/Enlace de Datos#Ethernet Frame\|Ethernet Frame]], el IP Datagram es una serie de campos estructurados estrictamente definidos.
![](https://i.imgur.com/ypKmdlA.png)

Las dos secciones principales son el encabezado (Header) y la carga útil (payload).

- Version
	- 4bits, Indica qué protocolo se está usando: IPv4 o [[IPv6\|IPv6]] 
- Header Length
	- 4bits, Indica el largo del encabezado. Casi siempre indica ser de 20bytes en IPv4 (el mínimo)
- Service Type
	- 8bits, Incluye detalles para el quality of service (QoS), básicamente un indicativo para los servicios que permiten a los routers acerca de qué paquetes son más importantes.
- Total Length
	- 16bits, indica el largo total del paquete en bytes. Mínimo es 20 sin información y el máxima es 65.535bytes (máximo en 16bits)
- Identification
	- 16bits, cuando fragmentamos los paquetes (porque su largo era mayor a 65.535) se le asigna un identificador el cual será el mismo en todos los paquetes del mismo grupo
- IP Flags
	- 3bits, el primero siempre es 0
	- El segundo es DF (Don't fragment) que indica que es un paquete que no debe ser fragmentado
	- El tercero es MF (More fragment) que está en todos los fragmentos menos en el último
- Fragment Offset
	- 13bits, especifica la posición del fragmento en el paquete original
- Time to Live
	- TTL, 8bits, indica cuantas veces un paquete puede pasar por los routers antes de morir. Cada vez que pasa por un router su valor se reduce en 1, cuando llega a 0 el router lo descarta y envia un ICMP time exceeded al emisor. Esto para evitar que un paquete se quede eternamente dando vueltas si tienes una red mal configurada.
- Protocol
	- 8bits, indica el protocolo del paquete, por ejemplo TCP tiene valor 6 y UDP valor 17
- Header Checksum
	- 16bits, guarda la suma de comprobación del paquete para alertar sobre errores al receptor.
- Source Address
	- 32bit, dirección del emisor
- Destination Address
	- 32bit, dirección del receptor
- IP Option
	- poco común, opcional, largo variable según las opciones usadas. Una opción de ejemplo sería 'source route' donde el emisor exige una cierta ruta de routers.
- Padding
	- Finalmente, y a veces, encontramos el padding que es un relleno de ceros para completar el tamaño final del paquete.

![](https://i.imgur.com/GBLadjq.png)
Paquete de ejemplo en wireshark, <a href="https://networklessons.com/cisco/ccna-routing-switching-icnd1-100-105/ipv4-packet-header">Fuente</a>

### Host ID & Network ID
![](https://i.imgur.com/cu8tctP.png)

NetID es un tramo fijo de la dirección IP que representa la red entera de un host conectado a un red. Osea, nos indica la red del host a la cual el host está conectada.
El HostID es el fragmento que identifica un host dentro de una red
Dado que la IP son 32 bits dividido en 4 octetos de 8bits, lo podemos dividir en 5 clases:
- Clase A: El primer octeto representa el NID. 8bits para el NID y 24bits para el HID, el primer bit del octeto siempre es 0
	- Usadas por grandes redes como las ISP
- Clase B: Los primeros dos octetos son el NID, 16bit para NID y 16 para HID. Los primeros dos bit son fijos.
	- Organizaciones grandes
- Clase C: Los primeros tres son el NID, 24bit para NID y 8 para HID. Los primeros tres bits del primer octeto son fijos.
	- Organizaciones pequeñas
- Clase D: Todos los bits son fijos para NID
	- Los 28 bits definen la dirección multicast
- Clase E: Todos los bits son fijos para el NID.
	- Reservadas para investigación y futuras compras.
![](https://i.imgur.com/KW5p2jv.png)

**Hoy en día, este sistema se ha ido desplazando por CIDR (Classless Inter-Domain Routing)**

#### CIDR
Classless Inter-Domain Routing, es un método más flexible para dividir las direcciones en subredes de cualquier tamaño. En lugar de clases fijas, se usa un prefijo de red que indica cuántos bits de la dirección son usados para el NID y cuántos para el HID, esto usa un slash que indica el número de bits. Por ejemplo:
192.168.1.0/24 nos indica que los primeros 24 bits son para el NID y los últimos 8 son para el host. En comparativa esto sería una clase C, pero CIDR permite cualquier tamaño de red. Osea tenemos una red con 256 direcciones (192.168.1.0 al 192.168.255) donde 0 es la red y 255 es la broadcast.

---

## ARP - Address Resolution Protocol
Protocolo usado para descubrir la dirección del hardware en un nodo con una cierta dirección IP. Cuando el paquete IP se forma, debe ser encapsulado dentro de un [[IT fundamentos/Conexiones y Redes/Enlace de Datos#Ethernet Frame\|Ethernet Frame]]. Es decir, necesita la dirección MAC de destino para completar el encabezado.
Casi todas las redes conectadas retienen una tabla ARP local, la cual es una lista de direcciones IP y sus direcciones MAC asociadas.

En el caso de que quisiera contactar una dirección IP que no encuentra en la tabla ARP, el nodo envía un ARP Broadcast que es un mensaje compuesto por F. Este broadcast se transmite a todos los equipos conectados a la red, los cuales responden con un ARP Response que incluye la dirección MAC.
Realizado esto, la dirección se asocia en la tabla.
Estas tablas se almacenan a nivel local y generalmente expiran en un tiempo determinado para contabilizar cambios en la red.