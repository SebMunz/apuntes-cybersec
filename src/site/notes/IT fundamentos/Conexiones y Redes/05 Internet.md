---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones y Redes/05 Internet/"}
---

# Conceptos desde POTS a WIFI6

## POTS y Dial-UP
Plain Old Telephone Service es un sistema muy antiguo, utilizaba el sistema telefónico tradicional analógico y utiliza cables de cobre.

Dial-Up fue una de las puertas de entrada para la primera oleada de internautas, utilizaba la misma línea que POTS, con velocidades típicas de 56kbps. Bloqueaba la línea telefónica durante su uso y tenía el famoso sonido de dial-up.

## Banda Ancha
### DSL
Digital Subscriber Line, aún se usa en algunos sectores. Utiliza las líneas telefónicas y sus velocidades van desde 1Mbps a 100Mbps.
Encontramos varios tipos con distintos enfoques como el ADSL, el VDSL y el SDSL. El ADSL es el más común en hogares con más descarga que subida pero SDSL es síncrono, por lo tanto tenía la misma velocidad de subida y bajada.

### Cable
El más común actualmente. Usa la infraestructura de TV por cable. Velocidades van desde los 10Mbps al 1Gbps. El ancho de banda se comparte por sectores.

### Fibra óptica
Transformándose de a poco en el nuevo estándar. Utiliza luz para transmitir los datos. Las velocidades van desde los 100Mbps a +10Gbps y subiendo. En general es más estable, rápido y confiable que el DSL y Cable pero su implementación es más cara y delicada.

### Lineas T
Aún en uso en algunas redes empresariales.
T1 tiene 24 canales a 1544Mbps cada uno, mientras que
T3 Tiene 672 canales y 44736Mbps

## WAN y VPN

### WAN
Wide Area Network. Conecta redes en áreas geográficas extensas. Utiliza tecnologías como MPLS, Frame Relay o Internet

Actúa como una sola red pero tiene localizaciones múltiples. Por ejemplo en una red empresarial con diversas oficinas en distintos lugares.
Para su configuración se suele contactar con el ISP. Las diversas redes de un WAN terminan en un punto DEMARC que es donde la red del ISP toma el control. El area entre el DEMARC y la red del ISP se llama ==local loop==. 

Un local loop es la conexión física desde el punto final del usuario al punto de presencia (POP) del proveedor. El cómo se entrega el local depende del proveedor (cobre, fibra, wifi, T, etc.) e instalado al DEMARC. Usualmente se instala por la compañía local pero puede ser instalado por otros proveedores. Al local loop también se le conoce como el enlace físico, linea de subscriptor o el circuito.

#### WAN física y SD-WAN
Las WAN físicas son las que hemos mencionado hasta ahora. Podemos agregar un Router WAN, un dispositivo de hardware que enruta los datos entre los grupos de miembros de LAN de una WAN mediante conexión privada. También conocidos como border routers.

SD-WAN hace referencia a Software defined WAN. Funciona para configurar entornos WAN en la nube. Usualmente se usan solas pero también se puede agregar un hardware. simplifica la implementación, administración, el costo y el mantenimiento de las WAN.

#### Optimización
Para optimizar su uso, se suelen usar varias técnicas:
- Compresión
	- Compresión de archivos y backups para mejorar la eficiencia del tráfico.
- Anulación de duplicación
	- Se centraliza un archivo y el resto de copias en la red, en realidad hacen referencia a este archivo central.
- Almacenamiento en caché local
	- Se almacenan copias locales de archivos de red y así reducir costos de transmisión. En una red LAN dentro de un WAN, podemos generar un caché local para ser compartido por los equipos.
- Control del tráfico
	- Limitación del ancho de banda
	- Límite de frecuencia
	- Uso de algoritmos
		- Podríamos, por ejemplo, priorizar tráfico LAN a LAN por sobre LAN a Internet.

#### Protocolos
- Conmutación de paquetes
	- Divide los mensajes en paquetes, los envía por diferentes rutas y los vuelve a ensamblar en el destino.
	- Los paquetes se triplican, se envían por separado a través de rutas óptimas a través de internet y se usan para comparar la integridad
- Retransmisión de tramas
	- Se usaba en líneas RDSI (ISDN, Integrated services digital network). Se ha reemplazado por DSL.
	- Circuitos virtuales permanentes: Se usan para conexiones de datos a largo plazo. Permanecen abiertos incluso cuando no se transmiten datos
	- Circuitos virtuales conmutados: se usan en conexiones de sesiones temporales para comunicación esporádica
- Modo de transferencia asíncrona
	- Más antigua, utiliza multiplex por división de tiempo asíncrono para codificar datos en celdas pequeñas de tamaño fijo. Útil para WAN a larga distancia
- Control de enlace de datos de alto nivel (HDLC)
	- Protocolo de encapsulamiento que entrega datos con información de control y corrección de errores. Tiene tres modos:
		- NRM: Nodo principal controla la transmisión
		- ARM: Nodo secundario puede iniciar la comunicación
		- ABM: Ambos pueden iniciar
- Paquete sobre una red óptica síncrona (SONET) o Jerarquía digital síncrona (SDH)
	- Protocolos de comunicación usados para el transporte WAN a través de cables de fibra óptica que definen cómo se comunican los enlaces punto a punto.
- Conmutación de etiquetas multiprotocolo (MPLS)
	- Técnica de optimización de enrutamiento que usa etiquetas cortas para dirigir los datos de manera eficiente, en lugar de búsquedas de tablas en direcciones de redes largas.

### VPN punto a punto
Las WAN son útiles para transportar grandes cantidades de datos por muchos sitios porque la tecnología WAN está diseñada así. El DSL suele ser más económico pero no soporta la requerida para estas situaciones.
Gracias a la movida de la infraestructura a la nube, las empresas pueden usar VPN punto a punto donde se establece un túnel entre estos dos sitios. Funciona similar a la VPN tradicional, sólo que aquí la lógica la manejan los dispositivos de red en ambos lados.
Entre los protocolos usados comunmente:
- IPsec
	- Internet protocol security. Conjunto de protocolos diseñados para asegurar comunicaciones a nivel de red mediante el cifrado de paquetes IP.
	- Dos modos:
		- Transporte donde se cifra sólo el contenido del paquete
		- Túnel donde se cifra todo el paquete
- L2TP
	- Layer2 Tunneling protocol. Tunelización que no proporciona cifrado por sí mismo pero generalmente se combina con IPsec.
	- Crea túneles en redes públicas permitiendo que los datos se transmitan de forma segura
- PPTP
	- Point to point tunneling protocol. Más antiguo, permite la creación de túneles para VPN.
	- Seguridad básica pero menos robusto que los otros y considerado vulnerable actualmente

# Redes Inalámbricas
Básicamente una forma de red sin cables. Los dispositivos se comunican entre sí por ondas de radio, generalmente 2.4GHz y 5GHz.
Las especificaciones más comunes para la comunicación de dispositivos de redes inalámbricas se definen en los estándares IEEE 802.11.
Las especificaciones más comunes son la b, a, g, n y ac. Cada una mejora algún aspecto de la anterior. En general, los protocolos 802.11 definen cómo operar en la capa física y en la de vínculo de datos.

### 802.11 Frame
Se compone de diversos campos:
- Frame control (16bits)
	- Similar a un header común, provee información acerca del frame. Incluye detalles como la versión de 802.11 y como procesar el frame.
- Duration Field (16bits)
	- Largo del frame, así el receptor sabe cuánto tiempo debe escuchar a la transmisión
- Address Fields (48bits o 192bits en total)
	- A diferencia del típico frame de 2 direcciones, este utiliza 4. Esto, por el uso de puntos de acceso en las redes inalámbricas.
		- Source Address: MAC de quien envía
		- Destination Address: MAC destino
		- Receiver Address: MAC del punto de acceso que recibió el frame
		- Transmitter Address: MAC del equipo que transmitió el frame
- Sequence control (16bits)
	- Mantiene el orden de frames con un número de secuencia
- Data Payload (variable hasta 2304bytes)
	- La información transmitida, incluye todo el stack superior
- Frame Check Sequence (32bits)
	- Usado para detección de errores, similar a como nos aseguramos de la integridad de los datos en [[IT fundamentos/Conexiones y Redes/02 Capa de red#IP Datagram\|Header checksum del paquete IP]] o al [[IT fundamentos/Conexiones y Redes/03 Capa de Transporte y Capa de Aplicación#TCP Segment\|Checksum del paquete TCP]], etc.

## WI-FI 6
802.11ax es el mayor salto a la tecnología wifi desde su concepción. Es más rápido y más eficiente para redes con mayor cantidad de dispositivos conectados.
- Velocidades de datos más altas
- Mayor capacidad de banda: Se aumentó de 80MHz a 160MHz
- Mejor rendimiento: transmisiones de entrada y salida eran de 4 por 4 en WI-FI 5, pero aumentaron de 8 por 8 en WI-FI 6
- Mayor eficiencia energética: Los dispositivos sólo se conectan a la red cuando se envían o reciben datos.

Además mejora la funcionalidad y conectividad:
- Se comparten canales para mejorar eficiencia y acotar el tiempo necesario para envío de datos
- Tiempo de activación objetivo (TWT) mejora la velocidad de la red y aumenta la duración de la batería
- Multi User MIMO (Multiple input Multiple Output) permite que se transfieran más datos de forma simultánea. Aumenta la capacidad y eficiencia de aplicaciones con gran ancho de banda.
- Uso de canales de 160MHz, más espacio para transmitir datos y aumenta la capacidad del ancho de banda
- Modulación de amplitud en cuadratura 1024 combina dos señales en un solo canal para que se codifiquen más datos.
- Acceso múltiple por división de frecuencias ortogonales (OFDMA) permite dividir el ancho de banda, que el punto de acceso asigna de forma dinámica
- Conformación de haces de transmisión, técnica que envía señales que permiten obtener velocidades más eficientes mediante la segmentación a cada dispositivo

Finalmente tenemos WI-FI 6E que extiende las funcionalidades agregando una banda de 6 GHz. Tiene más canales de transmisión (14 canales más de 80MHz y 7 de 160MHz). En proceso está actualmente WI-FI 7 que ofrecería aún mayores cambios.

![](https://i.imgur.com/trvZPrO.png)

## IoT
Internet of Things. Recopilan y transmiten datos sobre su entorno, estado y uso. Usos comunes incluyen sensores, artilugios o electrodomésticos. Por ejemplo controladores por voz (google home, alexa, amazon echo), cámaras inteligentes, smart locks (cierres automáticos y remotos), termostatos, etc. Pero también su uso es cada vez más amplio en industrias, sin embargo, no han logrado reemplazar los PLC (y sinceramente, no creo que lo hagan en el corto plazo).

##### Modelos de protocolos de datos IoT
O a grandes rasgos, cómo los dispositivos comparten datos.
- Solicitud/Respuesta
	- Sistemas distribuidos
	- Comunicación entre servidores y clientes mediante solicitudes y respuestas
	- HTTP, CoAP, etc.
- Publicación/Suscripción
	- Marco de trabajo para intercambio de mensajes
	- Involucra publicadores (Hosts), suscriptores (clientes) y un agente
	- MQTT, AMQP

##### Protocolos Comunes en la capa de aplicación
- HTTP/HTTPS
	- Estándar WWW
	- ASCII, 8bytes
	- puerto 80 u 8080
	- Seguridad adicional en HTTPS
	- Compatible con google cloud IoT Core
- Protocolo M2M (Machine to Machine)
	- Dispositivos de baja potencia
	- Incluye:
		- REST (Representational State Transfer)
		- SOA (Service Oriented Architecture)
		- MOP (Message Oriented Protocol)
- MQTT (Message Queuing Telemetry Transport)
	- Publicación/suscripción
	- Eficiente en IoT
	- TCP, SSL/TLS para seguridad
	- También compatible Google Cloud IoT Core
- CoAP (Protocolo de aplicación restringida)
	- Ideal para nodos y redes IoT con restricciones
	- Similar a HTTP, basado en REST
	- Gestión energética y automatización de edificios
- AMQP (Advanced Message Queuing Protocol)
	- Estándar abierto para mensajería entre aplicaciones
	- Interoperable, confiable y seguro
- XMPP (Extensible Message and Prescence Protocol)
	- Estandar abierto y descentralizado
	- Usado para chats, mensajería, videollamadas, etc.
- DDS (Data Distribution Service)
	- Middleware en la capa de aplicación
	- Modelo Suscripción/Publicación
	- Conectividad de datos de baja latencia
	- Escalable y con control de QoS

## Ad-Hoc y WLAN
Existen diversas formas de configurar una red inalámbrica.
En la red ad hoc los nodos se hablan directamente entre sí. También tenemos la WLAN o LAN inalámbrica que uno o más AP actúan como puente entre una red inalámbrica y una cableada. También tenemos las redes en Mesh que es un híbrido.

##### Ad hoc
Cada dispositivo se comunica con otro dispositivo en alcance directamente y todos los nodos ayudan a pasar los mensajes. Algunos smartphones pueden establecer estas redes para hacer intercambio de datos. En entornos industriales o de almacenamiento, donde algunos equipos pueden necesitar comunicarse entre sí pero no con otro elemento. También se pueden utilizar en caso de desastres por los equipos de emergencia.

##### WLAN
Es el tipo más común en una red empresarial. Uno o más AP actúan como puente entre las redes inalámbricas y cableadas. La cableada funciona como una LAN tradicional, conteniendo la salida a Internet.

##### Mesh
Todos los dispositivos están conectados entre sí de una u otra forma de manera ad hoc pero finalmente hay uno o más AP que funcionan como salida