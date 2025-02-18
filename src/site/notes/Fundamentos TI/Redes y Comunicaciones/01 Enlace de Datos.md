---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/01 Enlace de Datos/"}
---

# Dominio de Colisión

El dominio de colisión es un segmento de la red donde los datos pueden colisionar cuando dos o más equipos intentan comunicarse al mismo tiempo. En una red ethernet, especialmente conectadas a un hub, pueden sufrir de este problema.
A grandes rasgos cuando las redes interactúan, se envían 0 y 1 en corriente lo cual puede provocar un literal choque de corriente que pone en riesgo la transmisión.

Hoy en día, ya casi no es un problema con la introducción de los switches y las redes full-duplex, ya que cada enlace tiene su propio dominio, pero sigue siendo un tema en redes con hubs.

Este problema se suele solucionar con una técnica llamada CSMACD.

## CSMA/CD

Carrier Sense Multiple Access with Collision Detection.
Protocolo utilizado en redes ethernet para gestionar el acceso al medio de transmisión y minimizar las colisiones.
1. Carrier Sense
	- Los dispositivos escuchan el medio de transmisión para asegurarse que esté disponible antes de enviar datos
2. Multiple Access.
	- Varios dispositivos pueden acceder al mismo medio de transmisión
3. Collision Detection.
	- Si dos (o más) dispositivos envían datos al mismo tiempo, se detecta la colisión.
	- Los dispositivos esperan un tiempo aleatorio antes de volver a enviar información nuevamente.

---

# Unicast, multicast, broadcast

La transmisión Unicast envía información a un equipo específico en la red, para ello utiliza la dirección MAC.
A nivel de Ethernet, esto lo realiza revisando el **bit menos significativo** del primer octeto de la dirección, si este es cero, significa que ese envío es sólo para ese dispositivo. La transmisión la realizará en general, llegará al collision domain y de ahí sólo será recibido y procesado por el equipo destino.

Si el mismo bit es 1, significa que es multicast.
La transmisión Multicast está destinada a un grupo de equipos en la red, dichos equipos pueden unirse o no a estas agrupaciones. En otras palabras, aceptará o descartará la transmisión según criterios ajenos a la dirección MAC. 

Finalmente, la transmisión broadcast se envía a cada dispositivo de una red LAN, utilizando un destino especial conocido como broadcast address, la cual está compuesta sólo de *F*. La importancia de esta dirección es para que "se conozcan entre ellas", descubrimiento de redes y anuncios de red.

---

# Ethernet Frame

Un paquete de datos es un término para repsentar un set de información binaria enviada a través de la conexión de red. A nivel de Ethernet, un paquete de datos se conoce como **Ethernet Frame**.
Un ethernet frame es una colección estructurada de información presentada en un orden específico, de modo que este se pueda traducir a datos relevantes o viceversa.

Casi todas sus secciones son obligatorias y además poseen un tamaño fijo.

![](https://i.imgur.com/jnX90Sm.png)

A grandes rasgos: se inicia el paquete, se marcan las direcciones, se especifica el cómo manejarlo, se añade la información y finalmente una comprobación. Si hay algo distinto en la comprobación, el paquete es eliminado.
## 1. Preamble
8 bytes (64bits de largo) y se puede dividir en dos:
- Los primeros 7 bytes son una alternancia binaria que suele funcionar como buffer entre frames y se usa para sincronizar los relojes internos para regular la velocidad.
- El último byte es conocido como SFD (Start Frame Delimiter). Esto es una bandera para indicar que el preámbulo termina ahí.

## 2. Destination address
La dirección del recipiente, seguida de la MAC fuente.
Cada dirección es de 48 bits (6 bytes)

## 3. Source Address
Dirección de la fuente

## 4. VLAN Header
Virtual LAN. A veces presente. Técnica que permite tener múltiples LAN lógicas operando en el mismo equipo físico. Sirve para segregar el tráfico enviándola sólamente a otros equipos dentro de la misma VLAN. Los switchs se encargan de este encabezado.
## 5. Ether type
Describe el protocolo de los contenidos.

## 6. Payload
Carga útil, es la información enviada en el ethernet frame. Va desde los 46 a los 1500 bytes típicamente. Contiene toda la información de las capas superiores como la ip, transporte y capas de aplicación que se transmiten,

## 7. Frame check sequence (FCS)
Número de 4 bytes que representa una suma de comprobación (checksum) para ese frame. Se calcula usando un cyclical redundancy check sobre el frame (Comprobación de redundancia cíclica).
El CRC es una transformación matemática que usa una división de polinomios para crear un número que representa una cantidad más grande de información. Cada vez que se realiza un CRC sobre la información, deberías siempre recibir la misma checksum. De modo que esta comprobación final comprueba que lo que se recibió es exactamente lo mismo que se envió.

---


