---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer/"}
---

El objetivo de este desafío es la práctica de diseño, configuración y solucionar problemas en una red simulada usando Cisco Packet Tracer.

---
# Índice
1. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Creación y configuración de una topología básica\|#Creación y configuración de una topología básica]]
2. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Configuración\|Configuración de base]]:
	1. Nombrar routers y switches de acuerdo a la topología
	2. Configurar direcciones IP de interfaces
3. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Configuración OSPF\|Configuración OSPF]]
4. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Insertar nuevos equipos\|Agregar nuevos switch y equipos]]
5. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Configuración de los endpoint\|Configuración equipos agregados]]
6. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Verificación de conectividad\|#Verificación de conectividad]]
7. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Tablas de enrutamiento y protocolos\|#Tablas de enrutamiento y protocolos]]
8. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Conclusiones\|#Conclusiones]]
9. [[Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Configuración básica de switches y routers con Cisco Packet Tracer#Comandos\|Anexo de comandos utilizados]]
---

<div class="page-break" style="page-break-before: always;"></div>


# Creación y configuración de una topología básica

Queremos replicar esta topología:
![](https://i.imgur.com/BIQ106M.png)

Para ello, iniciaremos nuestro CPT e insertaremos equipos.
Partimos insertando 1 router 2621XM, le agregaremos una tarjeta WIC-2T (WAN interface card - 2 puertos) y repetiremos 2 veces para 3 routers.

![](https://i.imgur.com/NUrJaF2.png)
- Negro: Router 2621XM en cuestión que debemos duplicar  después de terminada la instalación de WIC-2T
- Morado: WIC Cover y NM Cover, las tapas para los lugares donde no instalaremos nada por ahora, protegiendo del polvo y mejorando la circulación de aire.
- Verde: WIC-2T y el lugar donde la insertaremos.
- Rojo: Botón de poder. Debemos apagar el equipo antes de instalar cualquier cosa y luego encenderlo cuando terminemos.

![](https://i.imgur.com/2RgOTnm.png)
Clonamos Router0 arrastrándolo con CTRL.

Ahora los conectaremos a través de cables DCE:
![](https://i.imgur.com/eZWBEd0.png)
Seleccionamos el cable DCE
![](https://i.imgur.com/IY1pRbG.png)
Después le damos click al router y elegimos serial 0/0
![](https://i.imgur.com/B5Gib9I.png)
Elegimos el router objetivo y lo conectamos a la serial 0/1

![](https://i.imgur.com/Z7IbR1h.png)

## Configuración
Ahora vamos a configurar los equipos con sus respectivas direcciones IP.
Hacemos click en nuestro primer router (Router0) y nos vamos a CLI
![](https://i.imgur.com/TXV1muL.png)
Ingresamos los siguientes comandos:
```
enable
configure terminal
hostname R1
!
interface Se0/0
ip address 192.168.2.5 255.255.255.252
no shutdown
clock rate 40000000
interface Se0/1
ip address 192.168.2.10 255.255.255.252
no shutdown
clock rate 40000000
do wr
```

Básicamente: habilitamos, configuramos, cambiamos el nombre, el ! es un separador de línea o para comentarios,
- Habilitamos.
- Configuramos este terminal.
- Cambiamos el nombre de host por R1.
- ! se usa para separar lineas o comentarios.
- Indicamos la interfaz a modificar (serial 0/0).
- Le damos esa la IP, que parte en .5 porque la primera ip asignable empieza desde ahí.
- Reactivamos la interfaz.
- Le damos el clock rate.
- Repetimos para la segunda conexión.
- Finalmente damos do wr (haz: escribir) para guardar.

Repetimos para Router2 y Router3.
>Router 2
```
enable
configure terminal
hostname R2
!
interface Se0/1
ip address 192.168.2.6 255.255.255.252
no shutdown
do wr
```
> Router 3
```
enable
configure terminal
hostname R3
!
interface Se0/0
ip address 192.168.2.9 255.255.255.252
no shutdown
do wr
```

Ya con esto realizado notaremos que los triángulos rojos se transforman en verdes, simbolizando la correcta conexión entre los puntos.
![](https://i.imgur.com/8yS4jXY.png)

---
<div class="page-break" style="page-break-before: always;"></div>


# Configuración OSPF
OSPF (Open Shortest Path First) es un protocolo de enrutamiento dinámico utilizado en redes WAN. Permite que los routers intercambien información sobre la topología de la red y calculen las rutas más eficientes para enviar paquetes de datos.
Lo clave:
- Ajusta automáticamente las rutas según cambios en la red
- Calcula la ruta más corta entre dos puntos
- Divide la red en áreas para mejorar la escalabilidad
- Es seguro ya que utiliza autenticación
- Reduce la congestión de tráfico
Dicho esto, la configuración es rápida en el CLI.
> Router 1:
```
enable
configure terminal
router ospf 1000
network 192.168.2.4 0.0.0.3 area 0
network 192.168.2.8 0.0.0.3 area 0
do wr
```
- le indicamos que vamos a configurar ospf en este router, con ID 1000
- indicamos la red a asignar y el área designada
- escribimos
Repetimos esto para los otros routers:
> Router 2:

```
enable
configure terminal
router ospf 1000
network 172.16.2.0 0.0.0.255 area 0
network 192.168.2.4 0.0.0.3 area 0
do wr
```

> Router 3:

```
enable
configure terminal
router ospf 1000
network 172.16.1.0 0.0.0.255 area 0
network 192.168.2.0 0.0.0.3 area 0
do wr
```

---
<div class="page-break" style="page-break-before: always;"></div>


# Insertar nuevos equipos
Primera agregaremos un par de switch y sus respectivos endpoints.

Insertamos dos switch 2960 que se encuentran en el apartado de Network devices -> Switches
![](https://i.imgur.com/qMY43nY.png)

Los nombramos según topología (swA - swB) y los conectamos utilizando cables directos (Cooper Straight-Through)
![](https://i.imgur.com/ueniYwh.png)

Agregamos los endpoints, un par de computadores a cada switch.
Cada uno conectado con el mismo tipo de cable directo.
![](https://i.imgur.com/P3NpjiD.png)

Ahora, lo que nos falta es configurar:
El hostname de los switches, las interfaces ethernet y los endpoints.
Partiremos por las interfaces ethernet.

Para ello simplemente vamos a nuestro R2 y R3, al CLI, y colocamos lo siguiente:
>Router 2
```
enable
configure terminal
interface fa0/0
no shutdown
ip address 172.16.2.1 255.255.255.0
do wr
```
> Router 3
```
enable
configure terminal
interface fa0/0
no shutdown
ip address 172.16.1.1 255.255.255.0
do wr
```
Sabemos que estamos OK porque las luces se tornan verde, indicando conexión entre ambos puntos
![](https://i.imgur.com/kzWopNS.png)

Para cambiar el nombre a los switches vamos al CLI de cada uno y le damos:
```
enable
configure terminal
hostname swA (o swB)
do wr
```

<div class="page-break" style="page-break-before: always;"></div>


## Configuración de los endpoint
Para ello abrimos el endpoint -> desktop -> IP Configuration
![](https://i.imgur.com/cjWJIxh.png)

En esta ventana hacemos la configuración según topología:
![](https://i.imgur.com/DwA1BYx.png)

Básicamente le indicamos que vamos a usar una IP estática, le decimos cuál IP (que es la que nos entregó la topología de base), la máscara de red (también proporcionada) y finalmente el gateway que es nuestro R3, terminado en .1

Repetimos lo mismo para el PC A
![](https://i.imgur.com/5JJuvdH.png)
<div class="page-break" style="page-break-before: always;"></div>


## Verificación de conectividad
Básicamente vamos a enviar un ping desde PC-A hacia PC-B, por lo tanto pasaremos por todos los equipos y deberíamos recibir una respuesta.
Nos dirigimos al desktop del endpoint y abrimos command prompt.
![](https://i.imgur.com/PJjA3Xo.png)
en él, escribimos `ping 172.16.1.10` y le damos enter
![](https://i.imgur.com/2N4ZE2K.png)
Aquí lo envié dos veces, por que en el primer envío se perdió un paquete. En el segundo se movieron los 4 sin problema.

![](https://i.imgur.com/TNqDMd9.png)
Aquí realicé lo mismo pero desde PC-B a PC-A
Todo OK.

---
<div class="page-break" style="page-break-before: always;"></div>

## Tablas de enrutamiento y protocolos
Finalmente utilizaremos un par de comandos para mostrar las tablas de enrutamiento y protocolos usados en cada router.

> Router 1

![](https://i.imgur.com/uPSdFxg.png)
```
enable
show ip route
```
En él podemos ver: 
1. los códigos de los protocolos y estados.
2. Que 172.16.0.0/24 tiene 2 subredes:
	1. 172.16.1.0 siendo la de 192.168.2.9 (conectada a la serial 0/1)
	2. 172.16.2.0 siendo la de 192.168.2.6 (conectada a la serial 0/0)
	3. Ambas son realizadas por protocolo OSPF
3. Que 192.168.2.0 tiene 2 subredes:
	1. 192.168.2.4, por conexión directa en serial 0/0
	2. 192.168.2.8, por conexión directa en serial 0/1
	3. Ambas por conexión directa

![](https://i.imgur.com/HKUicM8.png)
```
show ip protocols
```
Nos muestra los protocolos configurados, en este caso OSPF y su ID
- ID del router 192.168.2.10
- Números de áreas designadas (1)
- Máximo número de rutas (4)
- Rutas para esta red (nos muestra las rutas que configuramos)
- Respectiva información y fuentes de estas rutas.

> Router 2

![](https://i.imgur.com/jqn5QFR.png)
```
enable
show ip route
```
Obtenemos un resultado similar donde se nos indica las subredes configuradas y si están por conexión directa (C) o por protocolo OSPF (O)
Además nos indica su respectiva serial, o en este caso nos muestra también que una de nuestras conexiónes directas es por FastEthernet0/0 (hacia el switch)

![](https://i.imgur.com/RS5s28A.png)
```
show ip protocols
```
Ocurre lo mismo, nos muestra las rutas que traza OSPF.

> Router 3

![](https://i.imgur.com/UHwP0pm.png)
![](https://i.imgur.com/DWDIgiV.png)

Con esto mostramos ambos.

---
<div class="page-break" style="page-break-before: always;"></div>

# Conclusiones
Cisco Packet Tracer (CPT) es una buena herramienta para familiarizarse con las topologías de redes y poder practicar las mismas sin requerir de los costosos equipos o infraestructura. Básicamente poder poner en práctica sin miedo de arruinar algo.

En este desafío hemos configurado 3 routers, 2 switches y 2 endpoints para un total de 7 equipos. Esto realmente no es mucho en comparación con verdaderos sistemas empresariales con cientos (o miles) de equipos, pero nos entrega una buena base para poder ir escalándolo. A este mismo ejercicio podríamos agregar perfectamente redes PAN o incluso agregar más endpoints a cada uno de los switches; cada swithc aguanta 24 fast ethernet y 2 gigabit ethernet lo que nos daría 52 equipos que podriamos configurar con solo esos dos switches.

Se vió también la configuración sencilla de OSPF que es un protocolo bastante útil en redes WAN. Para este ejercicio es quizás un poco exagerado y podríamos haber usado algo más pequeño como EIGRP del mismo Cisco o IS-IS que son más eficientes para el tamaño que usamos.

Finalmente vimos el uso de algunos comandos como el ya clásico ping pero simulado desde CPT y los comandos de ruta de ip y protocolo que nos sirve para poder ver información relevante de nuestros routers, poder identificar configuraciones adecuadas y poder dar una revisión eficiente de estos.

---

<div class="page-break" style="page-break-before: always;"></div>

# Comandos

- `enable` : Para ingresar al modo privilegiado y poder entregar configuraciones al equipo
- `configure terminal`: Básicamente para indicar que vamos a configurar la terminal
- `hostname`: Cambiar el nombre de host
- `!`: Comunmente usado como separador de línea pero también se utiliza para iniciar comentarios en archivos de configuración
- `interface [interface]`: Indicamos que vamos a configurar la siguiente interface
- `ip address`: Asignar la siguiente dirección IP y su máscara de red
- `no shutdown`: Lo inverso de shutdown (osea, encender)
- `do wr`: Do de hacer, Write de escribir. Osea, Haz: escribe. Básicamente guarda la configuración.
- `show ip route`: Muestra la tabla de enrutamiento del router. Esto nos trae las rutas estáticas, dinámicas, redes conectadas de forma directa, rutas aprendidas por los protocolos, máscaras de subred, dirección de la puerta de enlace e interfaz de salida.
- `show ip protocols`: Muestra los protocolos de enrutamiento configurados. También muestra el número de procesos e ID, redes y áreas configuradas, vecinos y estados de protocolo.