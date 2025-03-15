---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables/"}
---

Las tablas IP es una herramienta de Linux para filtrar paquetes de red y controlar su tráfico. A grandes rasgos es un Firewall.

Viene preinstalado en la mayoría de distros, anteriormente era conocido como ipchains e ipfwadm.

Utiliza reglas para determinar qué paquetes pueden transitar por la red.

En este ejercicio:
- Crearemos una regla para bloquear la salida a internet.
- Crearemos una regla para bloquear la salida a solo un dominio
- Crearemos una regla para permitir acceso SSH, aunque no tenga el servicio funcionando.
> ejecutado en ubuntu

---

# Índice

1. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables#Bloqueo de salida a internet\|#Bloqueo de salida a internet]]
2. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables#Bloqueo específico\|#Bloqueo específico]]
3. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables#Regla para SSH\|#Regla para SSH]]
4. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables#Persistencia\|#Persistencia]]

---

<div class="page-break" style="page-break-before: always;"></div>

# Bloqueo de salida a internet

Primero haremos un ping para demostrar conectividad:
![](https://i.imgur.com/JevOLkm.png)

Ahora insertaremos una regla:
`sudo iptables -A OUTPUT -j DROP`
**donde:**
`-A` *especifica que le daremos una regla*
`-j` *especifica al objetivo de la regla lo que debe hacer si coincide.*

Y veremos la regla creada con el comando:
`sudo iptables -L -v -n`
**donde:**
`-L` *indica que debe listar*
`-v` *verboso*
`-n` *listar de manera numérica*
![](https://i.imgur.com/aW0Gznj.png)

Tiramos un ping (no hay conexión):
![](https://i.imgur.com/NG4pJLi.png)

Finalmente eliminamos dicha regla con
`sudo iptables -D OUTPUT -j DROP`
**donde:**
`-D` *indica la acción de eliminar una regla*
y lanzamos un último ping para corroborar conexión.
![](https://i.imgur.com/rRzSu4r.png)
Ahora volvemos a tener.

---
<div class="page-break" style="page-break-before: always;"></div>

# Bloqueo específico
Primero obtendremos la dirección IP del dominio a través de un ping a www.desafiolatam.com (172.67.175.45)
y creamos una regla:
`sudo iptables -A OUTPUT -d 172.67.175.45 -j DROP`
**donde:**
`-d` *Indica destino*
![](https://i.imgur.com/XTuvVdG.png)

Arrojamos dos ping:
1. `ping www.desafiolatam.com`
![](https://i.imgur.com/rITTvDo.png)

2. `ping www.google.com`
![](https://i.imgur.com/3eMAjHm.png)

Eliminamos y listamos la regla:
![](https://i.imgur.com/4sHF9N1.png)

---
<div class="page-break" style="page-break-before: always;"></div>

# Regla para SSH

El proceso es similar. El comando que utilizamos es:
`sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`
**donde:**
`-p` *indica el protocolo sobre el cual actuar*
`--dport` *indica el puerto de destino*

Osea estamos agregando una regla (-A) de entrada (INPUT) al protocolo tcp (-p tcp) en el puerto 22 (--dport 22) y la acción que debe realizar (-j) es la de aceptar (ACCEPT)
![](https://i.imgur.com/hslrO26.png)
![](https://i.imgur.com/8i0zxCr.png)


---

## Persistencia

Finalmente estas reglas no se guardan automáticamente (a menos que lo configuremos), pero la forma más sencilla es simplemente realizar:
`sudo iptables-save > /etc/iptables/rules.v4`

Lo que le indica a iptables que debe guardar las reglas hacia el archivo rules.v4
Si el archivo no existe, aplicamos `touch rules.v4` y `chmod 644` para permisos.

Si nos queremos ir un poco más extensos podemos generar una [[Fundamentos TI/Sistemas Operativos/Linux/Respaldo automático con Cron\|automatización a través de un script, cronjob y servicios]]