---
{"dg-publish":true,"permalink":"/IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux/"}
---

En este ejercicio gestionaremos servicios y el almacenamiento de una distribución **ubuntu**.
Se instalará y configurará  servicios comunes de red (HTTP, DHCP, FTP, SSH), gestión de particiones y sistemas de archivos en linux y por último gestión de volúmenes lógicos.
Utilizaremos la siguiente configuración de ubuntu en una VM.
![linux_admarch_ubuntu_vm.png](/img/user/Assets/linux_admarch/linux_admarch_ubuntu_vm.png)

---

# Tabla de contenidos

- [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Instalación de Servicios de red]]
	1. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux#Apache\|Instalación Apache y configuración básica]]
	2. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Configuración DHCP para asignar direcciones IP automáticamente en la red local]]
	3. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|FTP con acceso anónimo]]
	4. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Implementación SSH]]
- [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Gestión de particiones y sistemas de archivos]]
	1. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Creación de partición ext4 y montaje]]
	2. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Configuración fstab]]
- [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Gestión volúmenes lógicos]]
	1. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Creación de grupos de volúmenes (VG) a partir de volúmenes físicos (PV)]]
	2. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Creación de volúmen lógico (LV) dentro de un VG]]
	3. [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux\|Expansión de LV sin interrupción del servicio]]
- [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux#Conclusiones finales\|Conclusiones finales]]
- [[IT fundamentos/Linux/Gestión de servicios y almacenamiento en Linux#Comandos Utilizados\|Comandos]]

---

> Antes de comenzar, nos aseguraremos de ejecutar `sudo apt update` para estar actualizados.

# Instalación de Servicios de Red

## Apache2

Apache2 es un servidor de código abierto, quizás uno de los más populares actualmente. Gracias a él, habilitaremos **HTTP**.
Apache funciona como el portero, de modo que administra las solicitudes de conexión al servidor HTTP.
Otros de sus puntos fuertes es la facilidad de configuración, estabilidad, compatibilidad y su *modularidad*. Además, al ser uno de los más antiguos y populares de código abierto, tiene un nivel de documentación enorme y comunidades muy amplias con ayuda.
```
En este conexto, nos ayuda a crear un punto de control para conexiones entrantes, así poder dirigirlos adecuadamente a donde queremos. Sin embargo, su uso puede ser complejo a gran escala.
```

---

Comenzaremos con su instalación:
`sudo apt get install apache2 -y`
![linux_gestionsvcalm_install_apache.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_install_apache.png)
Esto iniciará la instalación que tomará no más de un par de minutos.
Terminado esto ejecutamos:
`sudo systemctl status apache2`
![linux_gestionsvcalm_apache_status.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_apache_status.png)
En esta ventana podemos ver varias cosas. Entre ellas que está **activo** y **habilitado**, desde **cuando** está funcionando, su proceso, el uso de memoria y cpu, además del historial de alertas.
En dicho historial, el segundo mensaje con código `AH00558` nos indica que no tiene un nombre por defecto y por lo tanto usará la dirección IP como nombre de servidor.

De pasada, configuraremos el nombre del servidor. Para ello abriremos el archivo de configuración de apache, añadiremos la directiva, verificaremos la sintaxis correcta y reiniciaremos apache para ejecutar los cambios.
Ejecutamos:
`sudo nano /etc/apache/apache2.conf`
Esto nos abrirá el archivo de configuración de apache2, nos vamos al final del archivo e incluimos la siguiente línea:
![linux_gestionsvcalm_apache_servername.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_apache_servername.png)
Guardamos y cerramos ( `CTRL + O, CTRL + X`)
Ahora, ejecutamos el comando `sudo apachectl configtest`, nos debería arrojar el siguiente mensaje:
![linux_gestionsvcalm_apache_configtest.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_apache_configtest.png)
Esto nos indica que está correcto.
Lo siguiente es configurar un sitio web estático.

Ejecutaremos el siguiente comando:
`echo "<html><body><h1>Hola, soy un texto desde apache</h1></body></html>" | sudo tee /var/www/html/index.html`
con esto sobreescribimos el `index.html` por defecto.

Ejecutamos `sudo systemctl restart apache2` para reiniciar el servidor, abriremos el navegador y nos vamos a `localhost` para encontrarnos con lo siguiente:
![linux_gestionsvcalm_apache_navegador.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_apache_navegador.png)

Esto confirma que hemos configurado apache de una forma básica y sencilla. Ahora podriamos expandir sus funciones a través de los módulos. Por ejemplo:
- Ejecución de scripts python, perl, php, etc.
- Configuraciones de seguridad como SSL, HTTPS, autenticación contra base de datos
- Proxy
- logs
Pero por ahora lo dejaremos tranquilo.

---
## DHCP

DHCP, **Dynamic Host Configuration Protocol** es el protocolo de red encargado de asignar las direcciones IP automáticamente a los dispositivos conectados a una red.
Su funcionamiento, a nivel superficial, es bastante sencillo:
1. Cuando un dispositivo se conecta a la red, envía una solicitud al servidor DHCP
2. El servidor responde con una oferta: esta incluye una dirección IP, máscara de subred, puerta de enlace predeterminada y otros parámetros adicionales.
3. El dispositivo acepta la oferta, envía una solicitud de confirmación
4. El servidor confirma la dirección ip


```
En un servidor, el uso de DHCP es útil para la gestión de conexiones, automatización de la configuración y escalabilidad. Podemos configurar distintos segmentos de red y reutilizar las ips.
Ahora, una incorrecta configuración podría traer problemas como que si el servidor DHCP falla, nadie podrá conectarse a la red, por lo tanto el DHCP es un bastión crítico de seguridad.

```

---

Partiremos instalando el paquete de DHCP.
`sudo apt install isc-dhcp-server -y`
![linux_gestionsvcalm_install_dhcp.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_install_dhcp.png)
Ya con esto instalado, ejecutamos:
`sudo nano /etc/dhcp/dhcpd.conf`, con esto abriremos el archivo de configuración por defecto de DHCP. Escribiremos lo siguiente:
![linux_gestionsvcalm_dhcp_subnet.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_dhcp_subnet.png)
> Con esto le decimos que en la subred x, aplique lo siguiente {`configuraciones`}.

Ahora configuraremos la interfaz de red.
Ejecutamos:
`sudo nano /etc/default/isc-dhcp-server`, con esto abriremos el archivo de configuración de dhcp  para las interfaces de red.
![linux_gestionsvcalm_dhcp_server.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_dhcp_server.png)
Aquí aplicamos las configuraciones en la interfaz `enp0s3` (recordar que es el nombre de la interfaz)
Guardamos, ejecutamos `sudo systemctl restart isc-dhcp-server` para reiniciar DHCP.
Luego ejecutamos `sudo systemctl status isc-dhcp-server` para comprobar su estatus. a lo cual recibí un mensaje de error.
![linux_gestionsvcalm_dhcp_error.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_dhcp_error.png)

Veamos la solución.
Ejecuté `journalctl -ex`, busqué el lanzamiento de dhcp y me encontré con esto:
![linux_gestionsvcalm_dhcp_error2.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_dhcp_error2.png)
Básicamente una mala configuración de subnet en la linea 17, tengo una ip distinta a la de la interfaz.
`sudo nano /etc/dhcp/dhcpd.conf`, cambiamos la ip por la de la interfaz
![linux_gestionsvcalm_subnet_fix.png](/img/user/Assets/linux_gestionsvcalm/linux_gestionsvcalm_subnet_fix.png)
guardamos, reiniciamos dhcp y status nuevamente.
![Pasted image 20240819174507.png](/img/user/Assets/linux_gestionsvcalm/Pasted%20image%2020240819174507.png)
Con eso hemos comprobado su funcionamiento.

---
## FTP

File transfer protocol. Es un protocolo usado para transferir archivos entre un equipo y un servidor a través de una red. Básicamente un copy paste a través de la red.
```
FTP es una forma sencilla de compartir archivos, incluyendo archivos de gran tamaño de forma de eficiente. Es muy útil para manejo de archivos de forma interna. Además se puede automatizar.
En este ejercicio lo haremos con acceso anónimo, lo cual puede ser útil para pruebas, pero es totalmente peligroso en un ambiente abierto y grande por su falta de seguridad.
```

---

Instalaremos **vsftpd**, el servidor fpt por excelencia de Linux. Los hay más, pero este es uno de los más recomendados.
`sudo apt install vsftpd -y`
![](https://i.imgur.com/GfrQ1R1.png)

y nos dirigimos a su configuración post instalación.
`sudo nano /etc/vsftpd.conf` y modificamos la siguiente línea para habilitar acceso anónimo:
![](https://i.imgur.com/6SmGQbF.png)
Guardamos, reiniciamos servicio con `sudo systemctl restart vsftp.service` y
`sudo mkdir /home/ftp/` para crear el directorio root del acceso anónimo.
Técnicamente con eso estamos listos, pero haremos un par de cosas más para agregar una capa de seguridad básica:

![](https://i.imgur.com/uQjDCDF.png)
Con esto deshabilitamos que los usuarios locales del servidores se conecten con su usuario, de modo que sus cuentas no puedan ser atacadas fácilmente a través de FTP.

![](https://i.imgur.com/Dw7mv2O.png)
Deshabilitamos la escritura. Los usuarios sólo pueden ver y descargar los archivos del servidor FTP.

Guardamos, reiniciamos servicio y le damos un `sudo systemctl status vsftpd`
![](https://i.imgur.com/qVLc0X9.png)
Funcionando.

Comprobaremos creando un archivo de texto en la carpeta root de anon y lo leeremos desde windows, conectado por FTP:
![](https://i.imgur.com/ZbHEksH.png)
(nota: tuve que cambiar el owner para escribir al archivo)

![](https://i.imgur.com/JFsaWmZ.png)
Accedí desde el cliente WinSCP, donde podemos ver que estamos en root, está el archivo `hola_ftp` creado desde Linux y tiene su contenido.

---

## SSH

Secure Shell. Protocolo de red que permite conexión segura a sistemas remotos.
```
Las conexiones son cifradas y posee una fuerte autenticación. Otro de sus puntos fuertes es la creación de túneles seguros para otros protocolos, es eficiente y multiplex (múltiples conexiones en el mismo puerto).
Todo esto nos entrega un protocolo útil en un ambiente de servidor.
```

---

Procedemos con su instalación: `sudo apt install openssh-server -y`
![](https://i.imgur.com/8K1MibA.png)

Ahora deshabilitaremos la autenticación por contraseña, de modo que sólo sea accesible por claves SSH.
`sudo nano /etc/ssh/sshd_config`
y vamos a configurar las siguientes líneas:

![](https://i.imgur.com/cn6zmXJ.png)
Para deshabilitar la autenticación por contraseña

![](https://i.imgur.com/eSdcT3t.png)
Deshabilitamos PAM (Pluggable Authentication Modules). Es un sistema que permite utilizar métodos de autenticación modulares, es decir, distintos métodos habilitados como biométrico, contraseñas, etc. Al deshabilitarlo, forzamos a que sólo se permitan las claves SSH.

![](https://i.imgur.com/VeuAm7q.png)
Debajo de UsePAM agregamos `ChallengeResponseAuthentication no`. Esto deshabilita la autenticación interactiva basada en desafíos y respuestas. Al deshabilitarlo simplificamos el acceso SSH y forzamos claves SSH.

Realizado esto guardamos, reiniciamos (`sudo systemctl restart ssh`) y verificaremos con SSH desde Windows.
Lo primero que haremos es generar las claves SSH desde windows.
`ssh-keygen -t rsa -b 4096`, con eso generamos una clave pública y una privada:
![](https://i.imgur.com/VSzeySM.png)
Nos pedirá dos cosas: dónde guardar las llaves y una frase para el 'salting' la clave.

Copiamos la clave pública al servidor SSH, hay diversas formas pero esta vez simplemente la copié y pegué, otras formas incluyen pasarla a través de FTP, manualmente o conectarse por contraseña normalmente, copiarla al servidor y luego demandar claves seguras.
![](https://i.imgur.com/8pvQGmN.png)
Ahí ya estamos conectados al servidor SSH de Ubuntu, montado en Virtualbox, a través de Powershell en Windows.

---

# Gestión de Particiones y Sistemas de Archivos

## Particiones

Las particiones son básicamente subdivisiones de un disco, estas pueden ser por varias razones como la organización o para aislamiento. ext4 es uno de los formatos más comunes pero también existen otros como `xfs`(útil en big data) o `f2fs`(diseñado para funcionamiento óptimo de discos SSD).

Haremos una partición ext4 y montarla:
Identificamos los discos actualmente activos: `sudo fdisk -l`
#pegar-screen

Luego, crearemos la partición con fdisk: 
`sudo fdisk /dev/sda`  y navegamos el menú:
#pegar-screen

Las opciones que elegimos son las siguientes:
- `n` para crear una nueva partición
- `p` para crear una partición primaria
- elegimos el número de partición
- checamos los valores para el espacio
- `w` para escribir los cambios.
#pegar-screen 

Ahora, haremos el formateo en `ext4`
`sudo mkfs.ext4 /dev/sdX1`
#pegar-screen #checar-nombre

Lo siguiente es montar la partición:
Crearemos un directorio de montaje: `sudo mkdir /mnt/nuevo_almacenamiento` y montamos la partición: `sudo mount /dev/sdX1 /mnt/nuevo_almacenamiento`
#pegar-screen 

Por último realizamos la comprobación a través del comando `df -h`
#pegar-screen 


#to-do
linux_gestionsvcalm_

---
# Comandos Utilizados
- `sudo apt get install apache2 -y`: Básicamente: super user do, instala la siguiente aplicación, dale yes a todo.
- `sudo systemctl status apache2`: Preguntamos a system control el status de apache2
- `sudo nano /etc/apache/apache2.conf`: Abrimos el archivo apache2.conf con nano
- `sudo apachectl configtest`: Control de apache, le pedimos que haga una prueba de configuración para verificar si está bien configurado.
- `echo "<html><body><h1>Hola, soy un texto desde apache</h1></body></html>" | sudo tee /var/www/html/index.html`: Este comando es básicamente un echo con el contenido del archivo html, un pipe, y el comando `tee` que agarra el input, lo despliega y/o lo guarda en un archivo o concatena en otro; en este caso reemplaza `index.html`
- `sudo apt install isc-dhcp-server -y`: Instalamos DHCP server
- `sudo nano /etc/dhcp/dhcpd.conf`: Archivo de configuración por defecto de DHCP
- `sudo nano /etc/default/isc-dhcp-server`: Archivo de configuración de interfaces de red para DHCP
- `sudo systemctl restart isc-dhcp-server`: Reinicio de servidor DHCP
- `sudo systemctl status isc-dhcp-server`: Revisar estado de DHCP
- `journalctl -ex`: Para revisar todos los logs del sistemas de forma centralizada
	- `-ex`: `e` hace que `journalctl` se mueva al 'end'. `x` hace que imprima más información adicional, útil para depurar errores.
- `sudo apt install vsftpd -y`: Instalamos **vsftpd**, el daemon FTP de Linux.
- `sudo nano /etc/vsftpd.conf`: Archivo de configuración del very secure FTP daemon
- `sudo systemctl restart vsftp.service`: Reinicio de servicio vsftp
- `chown`: Change Owner. Cambiar propietario
- `sudo apt install openssh-server -y`: Instalación servidor SSH
- `sudo nano /etc/ssh/sshd_config`: Archivo de configuración del servidor SSH
- `ssh-keygen -t rsa -b 4096`: Comando para generar las llaves.
	- `-t rsa`: Tipo de clave, RSA es el algoritmo
	- `-b 4096`: Tamaño de la clave en bits
- `sudo fdisk -l`: lista los discos y particiones.
- `sudo fdisk /dev/sda`: ejecutamos fdisk sobre sda
- `sudo mkfs.ext4 /dev/sdX1`: formateo, formato y etiqueta
- `sudo mkdir /mnt/nuevo_almacenamiento`: crear nuevo directorio
- `sudo mount /dev/sdX1 /mnt/nuevo_almacenamiento`: básicamente "montamos esto aquí".
- `df -h`: nos lista todas las particiones montadas en el sistema.