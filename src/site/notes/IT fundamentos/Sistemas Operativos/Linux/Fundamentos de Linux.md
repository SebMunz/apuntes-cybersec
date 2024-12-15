---
{"dg-publish":true,"permalink":"/IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux/"}
---

# Índice
- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Introducción\|#Introducción]]
- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Los principios fundamentales\|#Los principios fundamentales]]
	- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Los 5 fundamentos principales\|#Los 5 fundamentos principales]]
	- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Componentes\|#Componentes]]
	- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Arquitectura\|#Arquitectura]]
	- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Jerarquía de archivos\|#Jerarquía de archivos]]
- [[IT fundamentos/Sistemas Operativos/Linux/Fundamentos de Linux#Shell\|#Shell]]
---
# Introducción

Linux es uno de los sistemas operativos más importantes que mantienen vivo el ecosistema de computadores a nivel global. Empujado por un joven estudiante finlandés llamado Linus Torvald en el año 1991, rápidamente se transformó en un pilar fundamental de la infraestructura global.

Lo que conocemos como "Linux" esta ligeramente errado popularmente.
GNU/Linux sería lo correcto, dado que Linux es el Kernel y esto representa aproximadamente la mitad de un sistema operativo. El resto del sistema está compuesto por el proyecto GNU de Richard Stallman y componentes adicionales como compiladores, intérpretes y otros bajo la licencia GPL.

Es así como tenemos diversos sistemas operativos que utilizan el kernel de Linux como su base, como por ejemplo Android que utiliza el kernel de Linux pero no GNU.
Los sistemas utilizan la combinación GNU/Linux se le llaman popularmente **distros**, de los cuales hay cientos.
Entre las distros tenemos para:
Servidores
- Ubuntu Server
- CentOS
- Debian
- RedHat Enterprise
- SUSE Enterprise
Usuarios
- Ubuntu
- Mint
- Manjaro
- Fedora
- openSUSE
- Arch
Especialistas
- Kali
- Parrot
- Tails
- ROS
- BioLinux
Rarezas y bromas:
- RedStarOS, desarrollado por Corea del Norte
- HannahMontana Linux, Rebecca Black Linux, Justin Bieber Linux (...)
- Yggdrasil, el primer LiveCD de linux
- Gobo, que utiliza un sistema de directorios y organización más cercana a Windows

Destaca por su política de código abierto, su robustez, seguridad y flexibilidad. Sin embargo, también tiene sus desventajas como la falta de soporte en algunos casos, limitaciones debido a su escasa popularidad al nivel usuario e incluso su dificultad general.
Linux no es precisamente el sistema operativo más amigable a la hora de aprender a usarlo, tiene una curva de aprendizaje bastante alta en comparación con otros SO como [[Windows\|Windows]].

Sin embargo, el nivel de satisfacción por usarlo es mucho mayor gracias a la capacidad de poder modificarlo y ajustarlo a nuestro propio gusto.
A un nivel más de *power user*, su manejo es fundamental.

Actualmente linux corre en servidores, mainframes, escritorios, routers, televisores, relojes, refrigeradores, consolas, teléfonos, etc.

---
# Los principios fundamentales
## Los 5 fundamentos principales:
- **TODO ES UN ARCHIVO**
	- Todos los archivos de configuración para los servicios no son más que archivos de texto
- **PROGRAMAS SENCILLOS, PEQUEÑOS, DE UN SOLO USO**
	- Las herramientas y programas de linux cumplen un propósito específico que pueden combinarse con otros
- **COMBINAR PROGRAMAS PARA TAREAS COMPLEJAS**
	- Podemos utilizar los resultados de los diversos programas para realizar tareas más complejas como filtrar resultados específicos y redirigirlos a otras acciones
- **LAS GUI NO SON NECESARIAS**
	- Todo el sistema operativo está pensado para ser trabajado desde la terminal
- **LAS CONFIGURACIONES SON ARCHIVOS**
	- como por ejemplo `/etc/passwd` que contiene todos los usuarios registrados

## Componentes
- Bootloader
	- Un trozo de código que guía el proceso de encendido. Como por ejemplo GRUB
- OS Kernel
	- Maneja los recursos del sistema al nivel de hardware
- Daemons
	- Los servicios que corren en el background se llaman "Daemons" en linux
	- Manejan procesos pequeños como tareas programadas, imprimir y multimedia
- OS Shell
	- El shell, o CLI, es la interface entre el SO y el usuario, con ella podemos darle instrucciones al sistema operativo
	- Algunas populares son ZSH y Bash
- Graphics server
	- Provee de un subsistema (o servidor) para manejar los programas gráficos para que puedan funcionar de manera local o remotamente
- Window Manager
	- GUI. Es la interfaz gráfica de usuario donde podemos "ver" lo que estamos haciendo a través de una interfaz más amigable
	- Existen varias como KDE, GNOME, MATE, Unity y Cinnamon.
- Utilities
	- Aplicaciones que realizan acciones para el usuario o para otras utilidades.

## Arquitectura
- Hardware
	- Periféricos "físicos" como RAM, CPU y otros
- Kernel
	- Manejo de los recursos del computador, distribuyéndolo al SO
- Shell
	- CLI
- Utilidades de sistema
	- Entrega las funcionalidades al usuario final

## Jerarquía de archivos
Linux utiliza una estructura de árbol para sus archivos. Utiliza los siguientes directorios top-level:
- `/`
	- El punto raíz desde donde se montan todos los demás directorios ANTES del booteo inicial
- `/bin`
	- Binarios de comandos esenciales
- `/boot`
	- Bootloader, ejecutables del kernel y archivos requeridos para bootear Linux
- `/dev`
	- Archivos de dispositivos para acceder fácilmente a los hardware
- `/etc`
	- Archivos de configuración del sistema local. A veces posee también las configuraciones de aplicaciones
- `/home`
	- Directorio local de cada usuario para almacenamiento personal
- `/lib`
	- Bibliotecas compartidas por todos los usuarios con archivos que se requieren para el booteo de sistema
- `/media`
	- Dispositivos extraíbles se montan aquí
- `/mnt`
	- Punto de montaje para sistemas de archivos regulares
- `/opt`
	- Archivos opcionales, como para herramientas de terceros
- `/root`
	- Directorio de raíz para el usuario root
- `/sbin`
	- Contiene los ejecutables usados para la administración de sistema
- `/tmp`
	- Contiene archivos temporales del sistema
- `/usr`
	- Contiene ejecutables, bibliotecas, etc
- `/var`
	- Contiene archivos variables como logs, archivos cron, etc.

---

# Shell

Es importante familiarizarnos con el Shell/CLI en linux ya que gran parte de los servidores manejan linux.
No es difícil de entender ni aprender, gran parte de lo que hacemos en ella es bastante descriptivo si sabes lo que hace cada comando. Y si no lo sabes, siempre está el manual del comando.

Como se mencionó antes, el shell no es más que una interfaz para interactuar directamente con el sistema operativo. Todo lo que podemos hacer en el GUI, se puede hacer en el CLI pero con esteroides.

```shell-session
<usuario>@<hostname><directorio actual>$
```
Por defecto, generalmente se ve así.
O ejemplificado:
```shell-session
floure@mi_pc[~]$
```
`[~]` es nuestro directorio por defecto donde nos logueamos
`$` nos indica que estamos conectados como un usuario normal.

Linux tiene una forma de acceder a comandos y privilegios más avanzados llamado el superusuario root. `sudo` es el prefijo que utilizamos para realizar los comandos como super usuario, pero podemos "loguearnos" como super usuario sólo realizando `su`, ahí lo veríamos de esta forma:
```shell-session
root@mi_pc[~]#
```

Como especialistas en ciberseguridad, es importante entender lo que podemos ver en ese query inicial. En un ambiente propio y común, es así como lo veríamos. Pero en un ambiente de penetración, lo más probable es que sólo veamos `$`
Es ahí donde entra el archivo de configuración `.bashrc`, en él podemos configurar *qué vemos* en esa parte.
Por ejemplo podríamos agregar `\u` para visualizar el usuario actual, `\d` para la fecha y otros.
Son varias las opciones la verdad. Una manera rápida y eficiente de hacerlo es a través de herramientas como <a href="https://bash-prompt-generator.org/">este generador</a>.

Uno de los comandos más útiles que tenemos es el `man`, el cual nos entrega parte del *manual* del comando. Podemos, por ejemplo, consultar qué hace un comando de esta forma:
```shell-session
man curl
```
![](https://i.imgur.com/3Z4zTCK.png)
Además de `man`, podemos también utilizar `--help` o `-h`lo que nos dará las opciones:
![](https://i.imgur.com/UAmPVpj.png)

Otro muy útil es el comando `apropos` que nos ayudará a buscar comandos, revisando las instancias del nombre en los manuales
[[IT fundamentos/Sistemas Operativos/Linux/Comandos\|Este es el apartado con comandos linux]]

---

#wip