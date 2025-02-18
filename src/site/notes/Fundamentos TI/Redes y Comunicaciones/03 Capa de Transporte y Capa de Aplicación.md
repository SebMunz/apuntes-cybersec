---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/03 Capa de Transporte y Capa de Aplicación/"}
---

# Capa de transporte

## Multiplex y Demultiplex
Multiplex en la capa de transporte significa que los nodos en una red tienen la habilidad de dirigir el tráfico a distintos servicios receptores.
Demultiplex es el mismo concepto pero como receptor, recibiendo el tráfico dirigido a un nodo y dirigiéndolo a los servicios correspondientes.

Esto se realiza a través de puertos. Un [[Fundamentos TI/Redes y Comunicaciones/Protocolos y arquitectura/Puertos comunes\|puerto]] es un número de 16bit usado para dirigir el tráfico a servicios específicos de un computador.

---
## TCP Segment
TCP acepta información, la fragmenta y agrega un TCP Header así creando un TCP Segment.
Este es encapsulado en el datagrama IP e intercambiado.
En la jerga se usa 'paquete TCP' pero para ser más precisos:
- *segment* se refiere a TCP Protocol Data Unit (TCP PDU)
- *datagram* se refiere a IP Protocol Data Unit (IP PDU)
- *frame* se refiere al Data Link PDU.

El segmento TCP consta de una sección de encabezado y una de data. También posee 10 campos obligatorios y el campo opcional de opciones.
![](https://i.imgur.com/XesGAlG.png)

- Source y Destination Port
	- Indican puerto de origen y de destino
- Sequence number
	- Muestra *dónde* en la secuencia de segmentos TCP debería ir
- Acknowledgment number
	- Muestra el número del siguiente segmento esperado.
- Header Length
	- Largo del encabezado
- Empty
	- 6 bits vacios
- Control Flags
	- Banderas de control TCP
- TCP Window
	- Especifica el rango de numeros secuenciales que se podrían enviar antes de que una respuesta sea requerida.
- Checksum
	- Comprobación
- Urgent
	- Usado en conjunto a los control flags para indicar segmentos que podrían ser más importantes. (aparentemente casi no se ha usado ¿?)
- Options
	- Similar a las opciones del paquete IP para mayor control y control de flujo
- Padding
	- Serie de ceros para asegurar que la carga útil comience en el lugar esperado

---
## Banderas TCP
O puntos de control

En el encabezado TCP aparecen en el orden que los plantearé, un valor de 1 es 'activo'.
### 1. URG
Urgent. El segmento se considera urgente, habrá más información en el segmento Urgent del paquete.
### 2. ACK
Acknowledged. Es básicamente un flag de 'recibido'
### 3. PSH
Push. Indica que el equipo transmisor quiere empujar la información del buffer a la aplicación lo más pronto posible.
### 4. RST
Reset. Uno de los puntos de la conexión no ha logrado recuperarse del haber perdido segmentos o haberlos recibido de forma errónea. De esta forma se resetea la conexión
### 5. SYN
Synchronize. Se usa al principio de la conexión para asegurar que la conexión está establecida y se mantenga así.
### 6. FIN
Finish. Cuando se coloca en 1, se indica que este es el último paquete.

### Three-way handshake
El proceso es básicamente el siguiente:
- X envía un paquete con el SYN activo y el sequence number, de modo que Y lo recibe.
- Y responde con un paquete propio que incluye un ACK
- X nuevamente responde con un ACK. Básicamente se dicen "reconozco tu reconocimiento"
	- SYN-SYN/ACK-ACK Esto es el THREE WAY HANDSHAKE
- Ahora la conexión está realizada por lo que el intercambio de datos se puede realizar. Esto es también una conexión Full Duplex
-  Cada segmento enviado repite el ACK cada vez que se envían paquetes.
- Cuando X o Y está listo para terminar conexión, se envía un FOUR-WAY HANDSHAKE:
- Se envía un último paquete con el flag FIN y el receptor envía un ACK.
	- Hipotéticamente se puede mantener una conexión Simplex pero no es frecuente.

---
## TCP Socket
Instancia del end-point en una posible conexión TCP.
Requieren que un programa los instancie.
- LISTEN:
	- El socket está listo y escuchando para conexiones entrantes
	- Server-side
- SYN_SENT:
	- Se ha enviado solicitud de sincronización
	- Client-side
- SYN_RECEIVED:
	- Un socket en LISTEN recibió un request de comunicación y envió un SYN/ACK pero no ha recibido un ACK del cliente
	- Server-side
- ESTABLISHED:
	- Conexión establecida
	- Server y Client-side
- FIN_WAIT:
	- Se envió un FIN pero no se ha recibido un ACK por el otro punto
	- Cliente o Servidor, según quién inició el cierre
- CLOSE_WAIT:
	- Se cerró la conexión TCP pero la aplicación que lo abrió aún no suelta el socket.
	- Server-side
- CLOSING:
	- Ambos enviaron un FIN pero no se ha recibido el ACK
	- Ambos (cliente-servidor)
- LAST_ACK:
	- Después de recibido el FIN y enviado el ACK, el socket espera el ACK final del otro lado antes de cerrarse
	- Cliente o servidor (quien no inició el cierre)
- TIME_WAIT:
	- Después del último ACK el socket espera para asegurarse que el otro extremo recibió el ACK final
	- Quien inició el cierre
- CLOSED:
	- Conexión completamente terminada y no hay más comunicación.
	- Ambos.

---
## UDP
User Datagram Protocol.

A diferencia de TCP, que es orientada a conexión, UDP no lo es.
Esto significa que no establece conexión persistente entre emisor y receptor. Esto lo hace más rápido y eficiente en ciertos casos pero sacrifica fiabilidad y control de flujo que ofrece TCP.

En general:
Baja latencia pero no necesitan confirmación de recepción por lo que pueden duplicarse, perderse y llegar desordenados y son útil para streaming, juegos o transmisiones multicast.

Los pasos de uso son:
1. Emisión
2. Encapsulación
3. Recepción
4. Procesamiento

Los estados y procesos son más simples en UDP por la no necesidad de una conexión formal. Sin embargo tiene algunos conceptos clave:
- Bind
	- Se asocia el socket a un puerto local específico en el host para escuchar
- Sendto:
	- Se envia un datagrama a una IP y puerto específico
- Recvfrom:
	- Recepción del datagrama en una IP y puerto específico
- Multiplex/Demultiplex
	- Proceso de asignar los datagramas a la app correcta en el host, según puerto de destino

El ejemplo más común es los juegos en linea porque la prioridad es la baja latencia. El usar UDP para los movimientos del jugador permite una actualización rápida de los mismos pero si se pierde un paquete no es crítico porque llegará un nuevo paquete rápidamente con la información actualizada.

---
## Firewalls
Dispositivo que bloquea tráfico según ciertos criterios. Puede ser físico o no.
Pueden operar en distintas capas de la red, por lo que podriamos colocar firewalls en la capa de aplicación para monitorear el tráfico de las aplicaciones o podriamos colocar un firewall que bloquee rangos de ip.
El uso más común es colocarlos en la capa de transporte para bloquear conexiones y tráfico a ciertos puertos, algo así como policia fronteriza.

---

# Capa de Aplicación
En la capa de aplicación es donde las aplicaciones transmiten su información.
En general, hay distintos protocolos para cada cosa pero al final del día todas hablan más o menos lo mismo.
Por ejemplo para comunicar información de un servidor web podemos tener Apache, Nginx o IIS pero todos hablarán el mismo protocolo. Lo mismo con FTP, podemos tener FileZilla o WinSCP pero ambos utilizarán el mismo protocolo FTP y probablemente el mismo puerto 21 y/o 22.

En el modelo OSI, se agregan dos capas más a la capa de aplicación: la capa de sesión y la de presentación.
#### Capa de presentación
La capa de presentación traduce los datos entre el formato de red y el formato de la aplicación o viceversa. Se ocupa tanto de la transformación y codificación como del cifrado y descifrado.
Ejemplos:
- Conversión de formato de imágenes
- Cifrado SSL/TLS
- Compresión

#### Capa de sesión
La capa de sesión gestiona y controla las conexiones entre dos dispositivos (sesiones). También maneja la sincronización y el dialogo entre aplicaciones. Gestiona la recuperación en casos de interrupciones y coordina la retransmisión de los datos si es necesario.
Ejemplos:
- Define quién puede enviar datos (semiduplex o fullduplex)
- Checkpoints para asegurar la recuperación de datos en caso de fallos.

---

