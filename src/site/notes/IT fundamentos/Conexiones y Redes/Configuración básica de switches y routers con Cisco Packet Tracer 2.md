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
	2. [[IT fundamentos/Conexiones y Redes/Configuración básica de switches y routers con Cisco Packet Tracer 2#\|#]]

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

