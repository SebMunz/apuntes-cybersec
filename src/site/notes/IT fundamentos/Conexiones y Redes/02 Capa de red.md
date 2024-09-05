---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones y Redes/02 Capa de red/"}
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

---
# Capa de Red

## IPv4
Número de 32bit distribuidos en hasta 4 octetos descritos normalmente en numeros decimales. Estas se distribuyen ampliamente a todo el espectro. Por ejemplo, IBM tiene todas las IP que tienen el número 9 como el primer octeto, de este modo, si un equipo debe enviar información a una dirección 90.0.0.1, sólo debe saber que debe llegar a un router de IBM, y ese router se preocupará del resto.

Las IP corresponden a las redes y no a los equipos. El equipo posee una dirección MAC que nunca cambia, independiente del lugar; pero su dirección IP será asignada de forma distinta según dónde se encuentre, generalmente asignada por un protocolo DHCP.

### IP Datagram
Similarmente al [[IT fundamentos/Conexiones y Redes/01 Enlace de Datos#Ethernet Frame\|Ethernet Frame]], el IP Datagram es una serie de campos estructurados estrictamente definidos.
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
	- El recomendado es 64
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

### ARP - Address Resolution Protocol
Protocolo usado para descubrir la dirección del hardware en un nodo con una cierta dirección IP. Cuando el paquete IP se forma, debe ser encapsulado dentro de un [[IT fundamentos/Conexiones y Redes/01 Enlace de Datos#Ethernet Frame\|Ethernet Frame]]. Es decir, necesita la dirección MAC de destino para completar el encabezado.
Casi todas las redes conectadas retienen una tabla ARP local, la cual es una lista de direcciones IP y sus direcciones MAC asociadas.

En el caso de que quisiera contactar una dirección IP que no encuentra en la tabla ARP, el nodo envía un ARP Broadcast que es un mensaje compuesto por F. Este broadcast se transmite a todos los equipos conectados a la red, los cuales responden con un ARP Response que incluye la dirección MAC.
Realizado esto, la dirección se asocia en la tabla.
Estas tablas se almacenan a nivel local y generalmente expiran en un tiempo determinado para contabilizar cambios en la red.

---

# Subnets
>Básicamente es la subdivisión de las redes. Cada subnet tiene su propio gateway que maneja las entradas y salidas.
## Subnet ID
Dentro de una subnet, parte del [[IT fundamentos/Conexiones y Redes/02 Capa de red#Host ID & Network ID\|Host ID]] se usa para el SID.
La jerarquía es que primero va el NID para moverse por toda la red, cuando llega al último punto se usa el HID para derivar el paquete. Últimamente tenemos el SID para moverse dentro de la subnet cuando es necesario.
Las SID se calculan con **el uso de la subnet mask**, un número de 32bit - 4octetos en decimales generalmente.

Usando de ejemplo la IP 9.100.100.100, una red clase A - el 9 en binario es 1001 y con su padding al principio se vería así: ==0000 1001== mientras que el 100 se ve: ==0110 0100==.
Osea, básicamente la dirección IP en su formato binario se vería como `0000 1001 0110 0100 0110 0100 0110 0100`

La máscara de subnet tiene dos secciones:
- Principio: La máscara como tal, que es una serie de `1`
- Final: una serie de `0`
Para una de las máscaras más comunes: 255.255.255.0 nos da `1111 1111 1111 1111 1111 1111 0000 0000`
El propósito de la máscara (la parte de los `1111 1111`) es decirle al router que parte de la IP es la SID.
Para encontrar el SID, se realiza una operación AND a nivel de bit entre la dirección IP y la máscara. Sólo da como resultado 1 si ambos bits comparados son 1, si uno es 0, el resultado es cero, es decir ==1100 0000 1010 1000 0000 0001 0000 0000==. En este caso entonces el resultado del SID es 192.168.1.0.
Esto nos indica desde dónde empieza la red. El último octeto, que es el del HID, nos indica que se permite 256 direcciones posibles pero generalmente la 0 y la 255 están reservadas.

En el caso de que la máscara no termine en un octeto completo, como 255.255.255.224 (27bits en 1), 5 bits están reservados para hosts (32 direcciones - 2 direcciones reservadas = 30 total).
La forma corta de referenciar esto sería `255.255.255.224/27` lo cual nos indica la máscara y los bits.

---

## Routing
Un router es básicamente un dispositivo de red que envía el tráfico a su destino según los parámetros entregados. Los pasos básicos son:
1. Recepción del paquete
2. Examinación del destino del paquete
3. Buscar el destino en la tabla de enrutamiento
4. Enviar el paquete a través de la interfaz que esté más cerca a la red remota según se determine por la información de la tabla.
Repetir según sea necesario. El funcionamiento interno es más complejo, lógicamente.
O de otra forma:
1. Inicio de comunicación
2. Fragmentación y etiquetado de paquetes
3. Cálculo de ruta
4. Enrutamiento
5. Recepción/Entrega
### Tipos de enrutamiento
#### Estático:
O no adaptativo. Configuración se realiza manualmente, esto nos otorga total control sobre la red, direccionando los paquetes a donde nosotros queramos. El problema la escalabilidad que se vuelve un caos en redes con miles de equipos.

#### Dinámico:
O adaptativo. Proceso autónomo sin intervención humana. Se calcula el trayecto más corto con algoritmos y métricas predeterminadas. Es el más moderno y popular al ser más flexible y versátil.
El router agrega nuevas rutas a la table de enrutamiento basado en cambios en la topología de red.

#### Por Defecto:
Técnica en la que un router se configura para transmitir paquetes a una ruta por defecto, un gateway o el próximo dispositivo en linea si ninguna ruta es definida. Usado comúnmente  cuando la red tiene una sola salida, usando la ruta 0.0.0.0/0

### Protocolos
- RIP (Routing Information Protocol)
	- protocolo de distancia-vector que usa la cantidad de saltos necesarios como métrica
- OSPF (Open Shortest Path First)
	- protocolo conexión-estado que  encuentra el camino más corto según el <a href="https://es.wikipedia.org/wiki/Algoritmo_de_Dijkstra">Algoritmo de Dijkstra</a>
- EIGRP (Enhanced Interior Gateway Routing Protocol)
	- protocolo híbrido entre RIP y OSPF
- BGP (Border Gateway Protocol)
	- Protocolo ruta-vector que se usa para enrutamiento entre diferentes sistemas autónomos en internet
- IS-IS (Intermediate System to Intermediate System)
	- Usado principalmente en redes grandes (como ISP), del tipo conexión-estado

#### Métricas de enrutamiento
- Enrutamiento Distance-Vector.
Todos los nodos que son parte de la red dan aviso de su tabla de enrutamiento a sus nodos adyacentes según intervalos regulares. Con cada router siendo actualizado a intervalos regulares, toma tiempo que todos los nodos tengan la misma vista de la red.
Utiliza subredes de largo definido, por lo tanto no son buenas escalando. Utiliza el <a href="https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm"> algoritmo de Bellman-Ford</a> para encontrar el camino más corto.

- Enrutamiento Link-State.
Las rutas anuncian sus tablas de enrutamiento sólo cuando se actualiza la topografía. Se intercambia información de forma dinámica, incluyendo conexiones, costo y cantidad de saltos para encontrar la ruta más rápida.

<a href="https://www.geeksforgeeks.org/what-is-routing/">Algunos recursos extraidos de aquí, información más detallada</a>.

## Tablas de enrutamiento

Una tabla de enrutamiento es una tabla donde aparecen al menos 4 campos escenciales:
1. Red de destino: Identifica cada red que el router conoce
2. Next Hop: dirección ip del siguiente router al que se deben enviar los datos para llegar al destino. Si es la próxima, indicará 0
3. Total Hops: el número de routers por los que debe pasar antes de llegar al destino.
4. Interface: Identifica la interfaz específica del router a utilizar para reenviar el tráfico destinado a la red de destino.

### Protocolos de enrutamiento
Los protocolos internos usados para comunicarse entre routers.
Tenemos dos categorías principales:
- Interior Gateway Protocols
- Exterior Gateway Protocols

Los protocolos internos los mencioné en [[IT fundamentos/Conexiones y Redes/02 Capa de red#Tipos de enrutamiento\| este punto]]
Los protocolos externos se usan para comunicarse con los routers que representan el exterior de un sistema autónomo. Osea, nuestro objetivo es comunicarnos con esos routers que luego usarán protocolos más internos para ir acotando nuestro destino.

Básicamente: Internos se usan en redes internas de organizaciones. Externos se usan para compartir información entre organizaciones.

Es ahí donde entra la IANA (Internet Assigned Numbers Authority), organización sin fines de lucro que se encarga de la administración y asignación de estas IP. Además de ello, también administran el ASN (Autonomous System Number allocation) que se asignan a los sistemas autónomos. Por ejemplo, son los encargados de asignar el AS19604 (IBM) o el AS22047 (VTR Banda Ancha)

