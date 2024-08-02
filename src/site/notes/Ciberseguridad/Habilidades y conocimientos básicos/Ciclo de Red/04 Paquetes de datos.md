---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Ciclo de Red/04 Paquetes de datos/"}
---

# Paquete de datos

Unidad básica de información que va de un dispositivo a otro dentro de una red.

La información transmitida entre equipos se divide en pequeños paquetes que luego son reensamblados en el destino. En ciberseguridad, los paquetes proporcionan información que añade contexto a los eventos.

Los paquetes tienen tres componentes: header, payload y footer.

## Header
Encabezado.

Según el protocolo, el encabezado puede variar. Por ejemplo, un encabezado Ethernet, encabezado IP o encabezado TCP.

![Encabezado IPv4](insertar_enlace_imagen_encabezado_ipv4)

## Payload
Carga útil.

Inmediatamente después del encabezado viene la carga útil que son los datos reales que se entregan.

## Footer
Pie o Avance.

Al final del paquete. Ethernet utiliza el pie para brindar información de verificación de errores y determinar si los datos se dañaron. La mayoría de los protocolos no lo utilizan.

# Analizadores de protocolo de red
Packet sniffer.

Herramientas diseñadas para capturar y analizar el tráfico. Además de un uso de seguridad para monitorear redes, también pueden ser usados para recopilar estadísticas de redes y solucionar problemas de rendimiento. Sin embargo, también pueden usarse de forma maliciosa para capturar paquetes con datos confidenciales.

## Funcionamiento
1. Deben recopilarse a través de la tarjeta de interfaz de red (NIC - Network interface card) que es básicamente lo que conecta el computador a la red, como un router. Las NIC reciben y transmiten tráfico de red pero por defecto sólo consideran el tráfico dirigido a ellas. Para capturar todo el tráfico se debe configurar para que tenga acceso a todos los paquetes de red visibles. Esto suele conocerse como modo monitoreo o modo promiscuo. Esto permite que la NIC acceda a todos los paquetes de datos de red visibles, pero no serán necesariamente accesibles a través de una red. El analizador debe posicionarse en un segmento de red apropiado para acceder a todo el tráfico entre diferentes hosts.
2. El analizador de protocolos de red recopila el tráfico en formato binario sin procesar, para luego formatearlo en un formato comprensible.

## Captura
Packet sniffing es la práctica de capturar e inspeccionar paquetes de datos a través de la red. Un archivo pcap (Packet CAPture) es un archivo que contiene paquetes de datos interceptados desde una interfaz o red. Según la biblioteca de captura de paquetes usada, el formato varía:

- Libpcap
	- Diseñada para usar en sistemas similares a Unix (Linux y Mac). tcpdump utiliza libpcap como formato predeterminado.
- WinPcap
	- Código abierto, diseñada para dispositivos Windows. De los más antiguos y virtualmente obsoleto.
- Npcap
	- Diseñada por la herramienta Nmap que es comúnmente de Windows.
- PCAPng
	- Moderno, captura paquetes y almacena datos en simultáneo. Al hacer ambas se considera "next Generation".

## Recursos adicionales
[Packet Crafting, la práctica de forjar paquetes para penetración](https://resources.infosecinstitute.com/topics/hacking/packet-crafting-a-serious-crime/)
