---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Jaula Chroot/"}
---

Una jaula chroot, o simplemente chroot, es un mecanismo que permite crear un entorno aislado para un proceso en sistemas operativos tipo Unix.

Al ejecutar un proceso en un entorno chroot, se le presenta un directorio raíz diferente al del sistema operativo principal, lo que limita su acceso a archivos y comandos fuera de ese directorio aislado, como si estuviera en una "jaula"

# Indice
1. [[#Configuración Seguridad en la conexión SSH]]
2. [[#Creamos usuario|Nuevo Usuario]]
3. [[#Creamos la estructura de la Jaula|Estructura Jaula]]
4. [[#Copiamos binarios y librerías|Binarios y librerias]]
5. [[#Configuración SSH|Configuración para su uso]]

---

# Configuración Seguridad en la conexión SSH
-Si no tenemos instalado openssh-server, [[Fundamentos TI/Sistemas Operativos/Linux/Gestión de servicios y almacenamiento en Linux#SSH\|aquí hay un apartado]]-

Configuramos SSH de manera segura primeramente:
vamos a
`sudo nano /etc/ssh/sshd_config`

y agregamos/modificamos lo siguiente:
```
Port 2222
PermitRootLogin no
PasswordAuthentication no
```

Reiniciamos SSH
`sudo service ssh restart`

---

# Creamos usuario

`sudo adduser --shell /bin/false --home /home/desafio desafio`
![](https://i.imgur.com/h1P9Hrg.png)
Con este comando le dimos un shell falso-no funcional y le designamos una carpeta home.

---

# Creamos la estructura de la Jaula

`sudo mkdir -p /var/chroot/desafio/{bin,lib,lib64,home/desafio}`
![](https://i.imgur.com/jE9Gj7E.png)
y además cambiamos permisos con
`sudo chown root:root /var/chroot/desafio`
`sudo chmod 0755 /var/chroot/desafio`

Con esto creamos los directorios de forma recursiva y esta será su entorno, además de cambiar permisos para que root sea el propietario superior del entorno, agregando una capa de seguridad para evitar el escalamiento de privilegios. El usuario desafio podrá ser propietario y los otros sólo tendrán lectura y ejecución.

Verificamos con ``
`ls -ld /var/chroot/desafio`
![](https://i.imgur.com/EtacciL.png)

---

# Copiamos binarios y librerías

Para que el usuario pueda utilizar lo básico en su jaula, debemos también proporcionarle los binarios y sus respectivas librerías:
![](https://i.imgur.com/mkNeB3b.png)
- para copiar los binarios de ls y de bash
	`sudo cp /bin/bash /bin/ls /var/chroot/desafio/bin/`

Luego debemos copiar sus respectivas librerías.
```bash
# Para buscar las librerias necesarias, filtrarlas y copiar las necesarias
libs=$(ldd /bin/bash /bin/ls | awk '{print $3}' | grep ^/ | sort -u)
for lib in $libs; do
  dir="/home/desafio$(dirname "$lib")"
  sudo mkdir -p "$dir"
  sudo cp "$lib" "$dir"
done
```


---

# Configuración SSH

Vamos nuevamente a nuestro `sshd_config` y agregamos la siguiente linea para configurar perfiles específicos para un usuario:
![](https://i.imgur.com/HRz0br2.png)

con eso le decimos cuál es su directorio Chroot y que debe utilizarlo al conectarse por SSH.

