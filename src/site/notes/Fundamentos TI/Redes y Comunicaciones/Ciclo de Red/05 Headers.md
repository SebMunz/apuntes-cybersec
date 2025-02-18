---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/Ciclo de Red/05 Headers/"}
---

# Headers

Todos los paquetes tienen un encabezado o header. El header contiene información esencial para transferir la información a su destino. Distintos protocolos usan distintos encabezados.

El protocolo de Internet opera como el correo tradicional, utilizando la dirección IP para enviar el paquete y define la mejor ruta para enviarlo.

Hay dos versiones del protocolo de Internet:
- IPv4
	- Considerado el pilar fundamental de la comunicación en Internet.

- IPv6
	- La versión más reciente del protocolo de Internet.

Distintos protocolos usan distintos headers, por lo tanto, los del v4 y los del v6 difieren pero contienen campos similares con diferentes nombres.

## Estructura del paquete IPv4

- Version
	- Especifica la versión de IP siendo usada (IPv4 o IPv6).

- IHL
	- Internet Header Length. El largo del encabezado más alguna opción.

- ToS
	- Type of Service. Si es que ciertos paquetes debiesen ser tratados de forma especial.

- Total Length field
	- Largo del paquete, incluyendo encabezado e información.

Los siguientes 3 campos se relacionan con la fragmentación del paquete. Los paquetes se rompen en pequeños trozos que se transmiten y luego son reensamblados en el destino. Estos campos especifican si la fragmentación fue usada y cómo reensamblarlos.

- Identification
	- Si está fragmentado, cada paquete usará el mismo número de identificación de 16 bits.

- Flags
	- Hay 3 bits usados para la fragmentación.
	- bit 0 inicial.
	- bit DF (Do not Fragment) e indica que no debe estar fragmentado.
	- bit MF (More Fragments) se establece en todos los paquetes fragmentados exceptuando el último.

- Fragment Offset
	- 13 bits que indica la posición específica del fragmento en el paquete original.

- TTL
	- Time to Live. Cuánto vive el paquete antes de ser tirado. Sin este campo, los paquetes hacen loop entre los routers.

- Protocol
	- Protocolo. Cada número representa un protocolo diferente, como el 6 que es TCP.

- Header Checksum
	- Usado para determinar si hay algún error.

- Source Address & Destination Address
	- La IP de donde provienen y la IP a donde deben ir.

- Options
	- No es requerido pero se usa para solucionar problemas o revisiones. Si se usa, el largo del header aumenta.

- Información del paquete

## Estructura del paquete IPv6

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
