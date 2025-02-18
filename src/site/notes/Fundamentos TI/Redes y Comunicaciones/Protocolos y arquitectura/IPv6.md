---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/Protocolos y arquitectura/IPv6/"}
---

Busca solucionar el problema de la falta de direcciones IPv4.
IPv4 usa 32bits, que se traduce en 4.2 mil millones de direcciones.
IPv6 en cambio usa 128, lo que nos da un sextillón (o básicamente un número de 39 dígitos), un número tan largo que podríamos darle una ip a cada átomo de la tierra.

Las direcciones IPv6 se escriben en 8 grupos de 16bits, cada uno de estos grupos se compone de 4 números hexadecimales. Por ejemplo:
`2001:0db8:0000:0000:0000:ff00:0012:3456` es una dirección IPv6

Para su mejor lectura o simplicidad tenemos diversos detalles:
- Las direcciones que empiecen `2001:0db8` son exclusivas para documentación, libros, cursos y educación en general.
- Reglas de acortamiento:
	- Se puede sacar cualquier cero inicial de un grupo
	- Cualquier grupo de números consecutivos, compuesto sólo de ceros, se puede reemplazar con dos signos de dos puntos `::`
		- Sólo una vez, de izquierda a derecha, priorizando el grupo más grande.
	- La IP que mencioné quedaría `2001:db8::ff00:12:3456` en su forma corta.
	- O el loopback (127.0.0.1), que son 31 ceros con un 1 final, quedaría `::1`
- `FF00::` se usa para [[Fundamentos TI/Redes y Comunicaciones/01 Enlace de Datos#Unicast, multicast, broadcast\|multicast]]
- `FE80::` se usa para link-local unicast
	- link-local unicast se usan para recibir su configuración de red, similar al [[Fundamentos TI/Redes y Comunicaciones/04 Servicios de Red#DHCP\|DHCP]]
- Los primeros 64bits de cualquier dirección es el ID de red
- Los segundos son el ID del host

## Estructura

![](https://i.imgur.com/atT9x9f.png)

- Version
	- Indica la versión.
- Traffic Class
	- Similar al Type of Service de IPv4; información sobre la prioridad o clase del paquete.
- Flow Label
	- Un flujo es la secuencia de paquetes enviados desde una fuente.
- Payload Length
	- Largo del área de datos.
- Next Header
	- Indica el tipo de encabezado que sigue al IPv6, como por ejemplo, TCP.
- Hop Limit
	- Similar al TTL de IPv4.
- Source Address
	- Desde donde proviene.
- Destination Address
	- A donde va.

# Tunelización

Dado que las direcciones IPv4 y las 6 son incompatibles, se usan protocolos de túnel para transporta el tráfico de un lado a otro.
El túnel encapsula los datagramas IPv6 dentro de un [[Fundamentos TI/Redes y Comunicaciones/02 Capa de red#IP Datagram\|Datagrama IPv4]] permitiendo esta transición.

![](https://i.imgur.com/6gvDdav.png)


Los protocolos son de tres tipos:
- 6in4/Manual
	- Ofrece desempeño predecible pero puede tener problemas con NAT
	- Se puede debugear más simple por su configuración transparente.
- TSP (Tunnel Setup Protocol)
	- Permite configuración flexible y una implementación más amplia
- AYIYA (Anything in anything)
	- Permite túnel estable incluso entre NAT o IP dinámicas. Útiles para equipos móviles