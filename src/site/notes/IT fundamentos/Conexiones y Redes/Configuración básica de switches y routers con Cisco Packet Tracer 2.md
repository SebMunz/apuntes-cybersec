---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2/"}
---

El objetivo de este desafío es la práctica de diseño, configuración y solucionar problemas en una red simulada usando Cisco Packet Tracer.
A diferencia del [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer\|primer ejercicio relacionado]], este utiliza una topología un poco más avanzada.

---

# Índice

1. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Topología\|#Topología]]
2. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Configuraciones\|#Configuraciones]]
	1. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Configuración base\|#Configuración base]]
	2. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Configuración VLAN y VTP\|#Configuración VLAN y VTP]]
3. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Protocolo STP\|#Protocolo STP]]
4. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Configuración Endpoints\|#Configuración Endpoints]]
5. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Pruebas de conectividad\|#Pruebas de conectividad]]
6. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Conclusiones\|#Conclusiones]]
7. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#Comandos\|#Comandos]]

---

<div class="page-break" style="page-break-before: always;"></div>

# Topología

La topología a recrear:

![](https://i.imgur.com/QzvV9E9.png)

Para ello, vamos a iniciar el Cisco Packet Tracer (CPT) e insertar los equipos necesarios:
2 Routers (2621XM), 3 Switches (2960) y 4 Endpoints (PC).

![](https://i.imgur.com/Kay8MSi.png)

Lo siguiente será hacer las conexiones entre ellos.

![](https://i.imgur.com/AFrxCuB.png)
Para esto:
- Cable de cobre recto (Copper Straight-Through) desde FastEthernet de PC 0 y PC 2 a SW 2
- Cable de cobre recto (Copper Straight-Through) desde FastEthernet de PC 1 y PC 3 a SW 3
- Entre Switches están conectados con Cable de cobre cruzado (Copper Cross-Over)
- De SW 1 a Router A va con cable de cobre recto desde Gigabit Ethernet a Fast Ethernet del Router (en un caso real hay que tener en consideración los cuellos de botella que se puedan formar en redes de tráfico intenso, sin embargo en este caso no es problema y además están configurados full duplex con autonegociación de velocidad)
- De RA a RB están conectados con cable Serial. Para ello se agregó una interfaz serial a ambos.

<div class="page-break" style="page-break-before: always;"></div>

# Configuraciones
## Configuración base

Debemos ingresar al modo CLI de cada router y switch y configurar los nombres correspondientes, ya que los de la topología sólo son visuales, además de ello, debemos configurar las correspondientes ip.

```
enable
configure terminal
hostname RouterA  # cambiar según nombre
```

Para las IP podemos realizar lo siguiente:
```
interface FastEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

interface Serial0/0
ip address 10.1.1.1 255.255.255.252
no shutdown

```
Esto lo debemos repetir en ambos router.

<div class="page-break" style="page-break-before: always;"></div>

## Configuración VLAN y VTP

Primero crearemos el VTP en el SW1:
```
enable
configure terminal

vtp domain myVTP
vtp password myPass
vtp mode server
```
Luego en SW2 y SW3
```
enable
configure terminal

vtp domain myVTP
vtp password myPass
vtp mode client
```
Ya con esto realizado podemos enviar la información de los VLAN desde el servidor (SW1)
```
vlan 10
name VLAN010

vlan 20
name VLAN020

show vlan brief
```
![](https://i.imgur.com/EDV9sri.png)

Ahora sólo toca asignar:
```
enable
configure terminal

vlan 10
name VLAN10

vlan 20
name VLAN20

interface FastEthernet0/1
switchport mode access
switchport access vlan 10

interface FastEthernet0/2
switchport mode access
switchport access vlan 20

interface FastEthernet0/3
switchport mode trunk

interface FastEthernet0/4
switchport mode trunk

interface FastEthernet0/5
switchport mode trunk

interface FastEthernet0/6
switchport mode trunk

vtp mode client
vtp domain myVTP
vtp password myPass

```
Repetir y ajustar para SW3

<div class="page-break" style="page-break-before: always;"></div>

También debemos configurar Router A y Router B para permitir el enrutamiento VLAN:
Router A:
```
enable
configure terminal

interface FastEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.3.1 255.255.255.0

interface FastEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.4.1 255.255.255.0

interface FastEthernet0/0
no shutdown

interface Serial0/0
ip address 10.0.0.1 255.255.255.252
no shutdown
```

Repetir en Router B:
```
enable
configure terminal

interface Serial0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
```

<div class="page-break" style="page-break-before: always;"></div>

# Protocolo STP

STP (o Spanning Tree Protocol) previene bucles en una red conmutada, autobloqueando algunos puertos y activándolos automáticamente si es que los otros fallan.
Para testearlo en Cisco Packet Tracer, ejecutamos el siguiente comando en el SW1:
`show spanning-tree` lo que nos entrega lo siguiente
![](https://i.imgur.com/brCzxJI.png)
en ella podemos ver que SW1 no es el root bridge, lo que me está arrojando problemas de puertos en los otros switches.
Para solucionarlo, ejecutamos el comando:
```
enable
configure terminal
spanning-tree vlan 1 priority 0
spanning-tree vlan 10 priority 0
end
```
<div class="page-break" style="page-break-before: always;"></div>


Lanzamos nuevamente `show spanning-tree`
![](https://i.imgur.com/5iG3kgd.png)
Y podemos ver que ahora dice "This bridge is the root". El problema ocurre generalmente cuando los equipos tienen la misma prioridad pero la dirección MAC es menor.
<div class="page-break" style="page-break-before: always;"></div>

---
# Configuración Endpoints
Asignamos direcciones IP, subnet mask y gateway a cada PC, esto desde la pestaña Desktop -> IP configuration en cada endpoint.

![](https://i.imgur.com/GS1RGaz.png)
Para PC1 en la misma VLAN, la IP es `192.168.3.3` mientras que para PC2 es `192.168.4.2` (`192.168.4.1`para el gateway) y la IP de PC3 es `192.168.4.3`
<div class="page-break" style="page-break-before: always;"></div>

# Pruebas de conectividad
Para las pruebas de conectividad debemos dirigirnos al command prompt de cada PC.

**Intra VLAN**
PC0 -> PC1
`ping 192.168.3.3`
![](https://i.imgur.com/hu3aBbs.png)

PC2 -> PC3
`ping 192.168.4.3`
![](https://i.imgur.com/5WenOyQ.png)

<div class="page-break" style="page-break-before: always;"></div>

**Inter VLAN**
PC0 -> PC2
`ping 192.168.4.2`
![](https://i.imgur.com/pVjyWT6.png)

PC1-> PC3
`ping 192.168.4.3`
![](https://i.imgur.com/ccJfegs.png)

<div class="page-break" style="page-break-before: always;"></div>

Verificación de VLAN en Switches
`show vlan brief` en cada switch.

Switch1
![](https://i.imgur.com/RdqZXMt.png)

Switch2
![](https://i.imgur.com/6ZXzsfS.png)

Switch3
![](https://i.imgur.com/DDIsQSY.png)

<div class="page-break" style="page-break-before: always;"></div>

Finalmente con 
```
enable
show interfaces status
```
podemos ver el status de los puertos
![](https://i.imgur.com/HLCUWFn.png)

---
<div class="page-break" style="page-break-before: always;"></div>

# Conclusiones

Para este ejercicio, implementamos y verificamos el funcionamiento del protocolo Spanning Tree Protocol (STP) en una red con 3 switches, 2 VLAN y 4 endpoints. El objetivo fue evitar bucles de capa 2 y así evitar saturaciones de red, duplicación de paquetes e inestabilidad de la red.

STP nos ayuda con la eliminación de bucles al bloquear los puertos redundantes y nos ayuda con la redundancia al automáticamente activar los puertos que sean necesarios.

La mayor dificultad me la encontré cuando no lograba entender por qué tenía puertos aún funcionando. Esto lo logré resolver cuando aprendí el tema de las prioridades en STP y descubriendo que si todo tiene la misma prioridad, prima la dirección MAC.
También tuve que ajustar algunos comandos porque no todos funcionan para todos los equipos, como fue el comando switchport para encapsulación dot1q, ya que el switch 2960 sólo soporta un tipo de encapsulamiento.

En conclusión, la configuración STP garantiza red estable y eficiente, además de preparada para eventualidades. Tener énfasis en la configuración y la estructura adecuada de la red es importante para mitigar fallos en la red que pueden ser ocasionados por ataques.

---
<div class="page-break" style="page-break-before: always;"></div>

# Comandos
**Configuración VLAN y Puertos**
```
vlan <ID>
name <nombre>
exit

interface FastEthernet0/<puerto>
switchport mode access
switchport access vlan <ID>
exit
```

**Configuración de enlace troncal**
```
interface FastEthernet0/<puerto>
switchport mode trunk
exit
```

**Configuración VTP**
```
vtp domain <nombre_dominio>
vtp password <contraseña>
vtp mode <server/cliente>
```

**Cambiar prioridad de STP**
```
spanning-tree vlan <ID> priority <valor_prioridad>
```

**Diagnósticos y verificaciones**
```
show vlan brief
show vtp status
show spanning-tree
```