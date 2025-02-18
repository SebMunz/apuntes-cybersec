---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos./"}
---

Linux posee distintas maneras de moverse entre archivos y para la administración de grupos, usuarios, permisos y procesos.

En este apartado, ejecutaré algunos comandos a modo de ejercicio.
Para esto utilizaremos la versión mas reciente de ubuntu, montada en virtualbox.
![linux_admarch_ubuntu_vm.png](/img/user/Assets/linux_admarch/linux_admarch_ubuntu_vm.png)

---
# Tabla de contenidos

- [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Manejo de archivos y directorios\|Manejo de archivos y directorios]]
	1. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#1.- Creación de archivos y enlaces\|Creación de archivos y enlaces]]
	2. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#2.- Modificación\|Modificación]]
	3. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#3.- Eliminación y enlaces\|Eliminación y enlaces]]
	4. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#4.- Enlaces simbólicos\|Enlaces simbólicos]]
	5. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#5.- Eliminación e impacto en enlace simbólico\|Eliminación e impacto en enlace simbólico]]
	6. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#6.- Find e importancia de logs\|Find e importancia de logs]]
	7. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#7.- Comando de búsqueda\|Búsqueda]]
- [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Usuarios y grupos\|Usuarios y grupos]]
	1. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#1.- Creación de usuario\|Creación de usuario]]
	2. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#2.- Creación de grupos\|Creación de grupos]]
	3. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#3.- Listar usuarios\|Listar Usuarios]]
	4. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#4.- Listar grupos\|Listar Grupos]]
- [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Procesos\|Procesos]]
	1. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#1.- Formas de revisar procesos\|Formas de revisar procesos activos]]
	2. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#2.- Suspensión de procesos\|Suspensión de procesos]]
	3. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#3.- Relaciones jerárquicas\|Relaciones jerárquicas]]
	4. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#4.- Backups y Cron\|Backups y Cron]]
	5. [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#5.- Automatización de un reporte de monitoreo e importancia.\|Automatización de un reporte]]
- [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Conclusión\|Conclusión]]
- [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Anexo Comandos utilizados\|Comandos usados]]

---
# Manejo de archivos y directorios

## 1.- Creación de archivos y enlaces
En este apartado:
- Crearemos un archivo
- Agregaremos contenido
- Crearemos un enlace duro apuntando a dicho archivo
- Notaremos los inodos
- Anotaciones adicionales

![linux_admarch_touch_original.png](/img/user/Assets/linux_admarch/linux_admarch_touch_original.png)

1. Haremos `cd Downloads/` para movernos a la carpeta Downloads
2. `ls` para listar que la carpeta esta vacia
3. `touch original.txt` con touch le indicamos que crearemos un archivo con el nombre original.txt
4. `ls` nuevamente para checar que esté nuestro archivo
5. `cat original.txt` para revisar que el archivo esté vacío
6. `nano original.txt` para editar original.txt usando el editor nano

Se nos abrirá nano, un editor de texto en el terminal.
![linux_admarch_contenido_txt.png](/img/user/Assets/linux_admarch/linux_admarch_contenido_txt.png)
Posteriormente le damos a `CTRL + X` en el teclado para cerrar, escribimos Y para aceptar los cambios y presionamos `ENTER` para que se guarde con el mismo nombre.
Posteriormente haremos nuevamente `cat original.txt` para ver que se haya guardado correctamente:
![linux_admarch_cat_original txt.png](/img/user/Assets/linux_admarch/linux_admarch_cat_original%20txt.png)

Ahora crearemos un enlace duro y listaremos los inodos y permisos.
![linux_admarch_ls_li.png](/img/user/Assets/linux_admarch/linux_admarch_ls_li.png)
1. `ln -i original.txt duro_link.hd` para creación
2. `ls` para revisar su existencia
3. `ls -li` para listar inodos, permisos e información relevante.
Aquí podemos notar que ambos archivos son exactamente iguales, tanto el inodo, permisos y fecha de creación pero su nombre es distinto.

Un inodo es un identificador único para el archivo, el cual contiene los metadatos del archivo.

El enlace duro es un *alias* para un archivo. Es decir, es otra forma de acceder al mismo inodo.
En este caso, `duro_link.hd` y `original.txt`, lo que están haciendo ambos es acceder al inodo `918265`, con nombres diferentes.
Originalmente pensaba que eran lo mismo que los enlaces simbólicos (soft links - accesos directos) pero investigando un poco más encontré una analogía buenísima: ==Los enlaces duros son dos números de teléfono distintos para la misma linea, mientras que un enlace simbólico son dos lineas diferentes para la misma casa==. Esto quiere decir que un enlace duro de un archivo es el mismo archivo (inodo), accedido con otro nombre. Pero un enlace simbólico es otra forma de acceder a un archivo con un inodo diferente.
Las ventajas de un enlace duro parecen superiores ya que son más rápidos al apuntar al mismo inodo, pero no pueden cruzar sistemas y no pueden apuntar a directorios. En cambio los enlaces simbólicos son más flexibles en ese sentido pero se pueden romper más fácilmente.

Los enlaces duros pueden ser ideales cuando necesitamos múltiples nombres para un mismo archivo dentro del mismo sistema y queremos darle mayor seguridad a que el archivo no será accidentalmente borrado.

**¿Qué pasa si elimino el archivo original?**
Si elimino el archivo original, todos los enlaces duros se vuelven inválidos. Sin embargo, el archivo sigue existiendo en el disco porque su inodo sigue estando activo. Recién cuando eliminemos todos los enlaces duros, su inodo desaparecerá.
## 2.- Modificación
En este apartado:
- Modificaremos el archivo original.txt
- Mostraremos el contenido de duro_link.hd
![linux_admarch_cat_mod_hd.png](/img/user/Assets/linux_admarch/linux_admarch_cat_mod_hd.png)
Como podemos ver, las modificaciones hechas en el archivo `original.txt`, también se ven reflejadas en `duro_link.hd`. La explicación es la misma que hice [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Explicaciones y comentarios\|aquí]]. Ambos son el mismo archivo, pero accedidos de distinta forma.
## 3.- Eliminación y enlaces
En este apartado:
- Eliminaremos original.txt
- Mostraremos su contenido desde duro_link.hd
- Verificación de su estado
![linux_admarch_rm_txt.png](/img/user/Assets/linux_admarch/linux_admarch_rm_txt.png)
1. `rm original.txt`: eliminamos original.txt
2. `cat duro_link.hd`: comprobamos que el contenido sigue siendo el mismo
3. `ls -li`: verificamos *qué* hay en la carpeta.

Si bien, eliminamos el archivo original, su enlace duro sigue estando ahí. Como mencioné [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Explicaciones y comentarios\|aquí]], aplica el mismo concepto. Su inodo sigue existiendo y es a eso a lo que estamos apuntando.
## 4.- Enlaces simbólicos
En este apartado:
- Crearemos un nuevo archivo: example.txt
- Crearemos un enlace simbólico que apunte a example.txt

![linux_admarch_touch_con_echo.png](/img/user/Assets/linux_admarch/linux_admarch_touch_con_echo.png)
- `touch example.txt`: creamos example.txt
- `echo "texto" > example.txt`: echo para darle el texto, `>` para indicarle que la salida es hacia example.txt
- `cat example.txt`: para verificar su contenido
- `ln -s example.txt symlink.sl`: Creamos un enlace, con el argumento `-s` le indicamos que es un enlace simbólico
- `ls -li`: listamos la información de la carpeta.

Aquí podemos notar que los inodos de example y symlink son distintos. Además, podemos corroborar que los permisos son diferentes, incluye una `l` que indica que es un enlace simbólico, tiene fechas distintas y además symlink.sl -> example.txt nos indica que este archivo está apuntando a otro.
Con esta información podemos concluir definitivamente que un enlace simbólico es diametralmente diferente a un enlace duro.

## 5.- Eliminación e impacto en enlace simbólico
En este apartado:
- Eliminaremos example.txt
- Comprobaremos el contenido a través de su enlace simbólico
- Verificar estado

![linux_admarch_rm_comprob.png](/img/user/Assets/linux_admarch/linux_admarch_rm_comprob.png)
1. `rm example.txt`: eliminamos example
2. `cat symlink.sl`: revisamos el contenido, notamos que indica que el archivo no existe
3. `ls -li`: El archivo en realidad está ahí pero ahora su dirección apunta en rojo.

¿Qué ocurre?, los enlaces simbólicos al apuntar hacia otros archivos, no funcionan por sí solos. Es por esto que me arroja que el archivo no existe, porque en realidad me está diciendo que el archivo al que apunta, no existe.
Aquí [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#Explicaciones y comentarios\|nuevamente podemos comprarlo con mi respuesta previa]]. Los enlaces simbólicos apuntan *al archivo* y no al *inodo* como lo hacíamos con los enlaces duros.

## 6.- Find e importancia de logs
En este apartado:
- Con find buscaremos los archivos .log en un directorio particular
- Crearemos copias a un nuevo directorio
- La importancia de los logs

![linux_admarch_find_args.png](/img/user/Assets/linux_admarch/linux_admarch_find_args.png)
- `find /var/log -type f -name "*.log"`: iniciamos la búsqueda de los archivos log

![linux_admarch_sudo_rm.png](/img/user/Assets/linux_admarch/linux_admarch_sudo_rm.png)
- `sudo rm /tmp/copias`: el método que utilicé originalmente me creó un archivo binario que sólo podía eliminar de esta forma
- `sudo mkdir -p /tmp/copia_logs`: creamos el directorio dentro de la carpeta tmp
- `sudo find /var/log -type f -name "*.log" -exec cp {} /tmp/copia_logs/ \;`: básicamente busca los archivos y por cada archivo que encuentre ejecuta el comando `cp`
- `ls /tmp/copia_logs`: revisamos que estén las copias de los archivos.

Crear copias de los logs es crucial para mantener la integridad de los mismos. Con estas copias de seguridad podemos asegurarnos que los contenidos no han sido modificados y que están disponibles en todo momento. [[Fundamentos TI/Logs\|En este enlace de mis apuntes, hablo un poco sobre logs]]

## 7.- Comando de búsqueda
En este apartado:
- Comando para buscar archivos mayores a 5MB, listando sus nombres y tamaños
![linux_admarch_find_+5M.png](/img/user/Assets/linux_admarch/linux_admarch_find_+5M.png)
1. `find ~/ -type f -size +5M -exec ls -lh {} +`: Con este comando encontramos todos los archivos mayores a 5MB, pero dado que es una instalación fresca, no encontrará nada así que realizamos el siguiente:
2. `find ~/ -type f -size +1M -exec ls -lh {} +`: Es el mismo comando pero cambiamos que sea mayores a 1MB. Esto nos despliega como resultado los permisos, el autor, dueño, tamaño, fecha de modificación y localización, pero creo que podría mejorarse.

![linux_admarch_find_awk_adv.png](/img/user/Assets/linux_admarch/linux_admarch_find_awk_adv.png)
Este comando es similar, pero un poco más complejo. El resultado de `find` se lo pasamos (`|`) a `awk` (un lenguaje de programación interno de linea de comandos usado para procesar y analizar textos), luego imprimimos (`print`) los parámetros $9 y $5 concatenando un `:` entremedio.

La utilidad de este tipo de comandos es útil a la hora de tomar respaldos, de administrar el espacio, ayuda a hacer mantenimiento de los computadores y ayuda a identificar archivos obsoletos, con esto podemos fácilmente identificar archivos problemáticos, podriamos combinarlo con otros comandos para automáticamente eliminar todos los archivos mayores que un determinado tamaño o podriamos generar un informe con ello.

---
# Usuarios y grupos

## 1.- Creación de usuario
En este apartado:
- Crear un usuario con una ID determinada con shell bash
- Crear otro usuario, pero con shell no interactivo
- Un tercer usuario con shell zsh
![linux_admarch_usrs.png](/img/user/Assets/linux_admarch/linux_admarch_usrs.png)
1. `cat /etc/passwd`: Primero corremos este comando para verifiar los usuarios actuales. Los primeros usuarios que lista son todos internos de sistema, el último es el usuario que cree para usar ubuntu.

![linux_admarch_useradd.png](/img/user/Assets/linux_admarch/linux_admarch_useradd.png)
1. `sudo useradd -u 1000 -s /bin/bash ana`:  sudo, creamos nuevo usuario, le pasamos el id y le decimos que shell usar. En este caso nos encontramos con un error porque el id 1000 ya estaba en uso por el usuario por defecto (seb)
2. `sudo useradd -u 1001 -s /bin/bash ana`: Cambiamos el id 1000 por el 1001 y esta vez si funciona
3. `sudo useradd -u 1100 -s /usr/sbin/nologin marta`: Mismo proceso pero le damos id 1100 y especificamos usar no-login.
4. `sudo useradd -u 1200 -s /bin/zsh`: Mismo proceso, id 1200 pero nos topamos con que no es posible ya que no existe zsh. Procedemos a su instalación.


![linux_admarch_apt_install.png](/img/user/Assets/linux_admarch/linux_admarch_apt_install.png)
1. `sudo apt install zsh git fonts-font-awesome`: sudo, apt install para installar zsh, además le damos parametros adicionales para instalar fuentes que podrían ser útiles para configurar zsh en un futuro.
2. `sudo useradd -u 1200 -s /bin/zsh`: Lo ejecutamos pero me dice que el usuario ya existe así que lanzamos...
3. `cat /etc/passwd`: Para leer nuevamente los contenidos de passwd, listar usuarios y obtenemos:
![linux_admarch_usrlist.png](/img/user/Assets/linux_admarch/linux_admarch_usrlist.png)
Con esto ya confirmamos que están los 3 usuarios creados y con un shell asignado.
Como anotación sobre los shells, me parece importante mencionar:
- `bash` es el CLI por defecto
- `nologin` básicamente crea un usuario sin login, útil para usuarios que no lo necesitan
- `zsh` es similar a `bash` pero con más características y funciones, es un bash con esteroides.

## 2.- Creación de grupos
En este apartado:
- Crearemos 3 grupos diferentes.
- Asignaremos a los 3 usuarios a dichos grupos.
![linux_admarch_groupadd.png](/img/user/Assets/linux_admarch/linux_admarch_groupadd.png)
Corremos el mismo comando modificado 3 veces para así crear los grupos:
`sudo groupadd -g idgrupo nombregrupo`

![linux_admarch_usermod.png](/img/user/Assets/linux_admarch/linux_admarch_usermod.png)
Ejecutamos:
1. `sudo usermod -aG grupo usuario`: Ejecutamos este comando tres veces cambiando los parámetros de grupo y usuario
2. `uso (...)`: comando mal escrito
3. `groups ana marta carlos`: Listamos los grupos de cada usuario.

Con este proceso hemos agregado a cada usuario a un grupo distinto.

## 3.- Listar usuarios
En este apartado:
- Listamos la información de cada usuario
![linux_admarch_usrid.png](/img/user/Assets/linux_admarch/linux_admarch_usrid.png)
Ejecutamos el comando `id` con cada usuario.
Recibimos:
- `uid`: user id
- `gid`: group id
- `groups`
> Lo primero que noté es que además de los grupos que le entregué yo a cada uno, cada usuario tiene un grupo personal con la misma id que el usuario.
> Esto se debe a que la mayoría de las distros modernas de linux existe el concepto de `UPG` o User Private Group. Cuando creamos un usuario nuevo, se le asigna automáticamente a un grupo privado del mismo usuario, de modo que los archivos que este crea, sean sólo de su autoría y no de un grupo común, para así evitar problemas de integridad.

Ahora, listaremos además los usuarios con grep.
![linux_admarch_grep_usr.png](/img/user/Assets/linux_admarch/linux_admarch_grep_usr.png)
La salida que nos entrega grep es `usuario:contraseña:uid:gid:comentario:rutaHome:shell`.
La contraseña está encriptada por lo tanto sólo nos entrega 'x' a modo simbólico, como no tenemos comentarios de usuario sólo aparece como `::` sin nada entremedio.

## 4.- Listar grupos
En este apartado:
- Listaremos la información de los grupos.
![linux_admarch_grep_group.png](/img/user/Assets/linux_admarch/linux_admarch_grep_group.png)
Obtenemos `grupo:x:gid:usuarios`. Es similar a lo que obtenemos de usuarios, nuevamente la `x` representa la contraseña encriptada.

---
# Procesos
## 1.- Formas de revisar procesos
En este apartado:
- Revisaremos los procesos activos en el sistema con diferentes comandos
- Analizaremos las ventajas, desventajas y diferencias de cada uno.

##### PS
![linux_admarch_ps.png](/img/user/Assets/linux_admarch/linux_admarch_ps.png)
`ps`: Muestra un snapshot o instantánea de los procesos. Veo que es más limitado sin argumentos pero si le pasamos aux es mucho más completo
![linux_admarch_ps_aux.png](/img/user/Assets/linux_admarch/linux_admarch_ps_aux.png)
`ps aux`

##### PSTREE
![linux_admarch_pstree.png](/img/user/Assets/linux_admarch/linux_admarch_pstree.png)
`pstree`: Muestra los procesos como un árbol, podemos ver qué proceso responde a qué o su relación padre-hijo.

##### TOP
![linux_admarch_top.png](/img/user/Assets/linux_admarch/linux_admarch_top.png)
`top`: Funciona en tiempo real, y se va actualizando constantemente como un monitor. Similar al administrador de tareas de windows.

##### HTOP
![linux_admarch_htop.png](/img/user/Assets/linux_admarch/linux_admarch_htop.png)
`htop`: No viene por defecto pero lo instalamos rápidamente con `sudo apt install htop`. Es más completo que top.

Cada uno de los comandos utilizados tiene su propia ventaja y desventaja.
- `ps` sirve para mostrarnos un "pantallazo" de los procesos, es más limitado en ese sentido pero podemos recibir más información con más argumentos.
- `pstree` también nos muestra un pantallazo, es bueno mostrándonos la jerarquía pero no nos muestra, por ejemplo, el uso de recursos.
- `top` top si nos muestra el uso de recursos en tiempo real pero su interfaz es poco amigable e intuitiva
- `htop` es ahí donde entra htop que sí es más visualmente intuitiva. tenemos distinciones de colores (que ya es una gran diferencia).

## 2.- Suspensión de procesos
En este apartado:
- Abriremos un nuevo proceso
- Lo suspenderemos y verificaremos su estado
- Será reanudado y luego terminado de forma adecuada.

Ejecutamos `vi` para abrir Vim y presionamos `CTRL + Z`
![linux_admarch_suspend.png](/img/user/Assets/linux_admarch/linux_admarch_suspend.png)
![linux_admarch_ps_grep.png](/img/user/Assets/linux_admarch/linux_admarch_ps_grep.png)
![linux_admarch_ps_grep_vi.png](/img/user/Assets/linux_admarch/linux_admarch_ps_grep_vi.png)
Ejecutamos:
- `ps` : solo con este comando no logramos identificar si el proceso está suspendido, nos falta más información.
- `ps aux | grep 'vi'`: Ahora sí podemos ver en el id 4952 que Vi está con estado 'T' que significa suspendido.
- `ps aux | grep -w vi`: Un grep más acotado para que no me muestre coincidencias parciales.

![linux_admarch_foreground.png](/img/user/Assets/linux_admarch/linux_admarch_foreground.png)
Utilizamos el comando `fg nombre`. En este caso, `fg` era suficiente, esto trae el proceso suspendido más reciente, pero es bueno tener en cuenta que si tenemos más de uno, debemos pasarle el nombre.
![linux_admarch_backtovim.png](/img/user/Assets/linux_admarch/linux_admarch_backtovim.png)

Realizamos nuevamente `ps` y notamos que Vi ya no está activo.
![linux_admarch_ps_comp.png](/img/user/Assets/linux_admarch/linux_admarch_ps_comp.png)

De pasada, aprovecharemos de cerrar forzosamente nano
![linux_admarch_kill.png](/img/user/Assets/linux_admarch/linux_admarch_kill.png)
`kill -9 5113`

## 3.- Relaciones jerárquicas
En este apartado:
- Relaciones jerárquicas con `ps`

Para mostrar las relaciones de jerarquía que tienen los procesos, usando `ps`, le pasamos los argumentos `fax`, cada uno de ellos hace algo diferente:
- `f` nos muestra el formato completo, incluyendo una columna árbol con las jerarquías.
- `a` nos muestra los procesos de todos los usuarios
- `x` muestra los procesos que no están asociados a una terminal, como procesos en segundo plano.

Ejecutamos `ps fax`
![linux_admarch_ps_aux_tree.png](/img/user/Assets/linux_admarch/linux_admarch_ps_aux_tree.png)
Aquí podemos ver en el proceso 2627 que:
- `/usr/libexec/gnome-termina-server` es el proceso de donde sale la terminal, esta es padre de
- `bash` que es la terminal, y este a su vez es padre de
- `ps fax` que es el comando que estamos viendo.
- Cada indentación muestra la jerarquía.

Ejecutamos `ps -ejH`
![linux_admarch_pid.png](/img/user/Assets/linux_admarch/linux_admarch_pid.png)
Este es un comando similar con la diferencia que:
- Nos muestra los procesos como árbol compacto
- `e` muestra todos los procesos sin importar el usuario
- `j` muestra información sobre el grupo de procesos, incluyendo su id
- `H` le otorga la cualidad de mostrarlo con el árbol de jerarquías.

También, similarmente tenemos `ps --tree` que no está disponible siempre pero muestra sólo los procesos activos del usuario, omitiendo los procesos en segundo plano.
![linux_admarch_ps_forest.png](/img/user/Assets/linux_admarch/linux_admarch_ps_forest.png)

## 4.- Backups y Cron
En este apartado:
- Crearemos una tarea de automatización con cron
- Automatizar backup de documentos

Para esto tenemos 2 alternativas:
1. Crear un script, el cual sea ejecutado por crontab
2. Crear la tarea dentro de crontab.

Con tareas complejas la primera opción es la ideal, por lo tanto la segunda opción es la más adecuada, pero por fines educativos haremos ambas.

![linux_admarch_compr.png](/img/user/Assets/linux_admarch/linux_admarch_compr.png)
1. `ls` para notar que no hay nada en `/Documents`
2. `touch script-backup-cron.sh` para crear un script de bash
3. `ls` nuevamente para ver su creación
4. `nano script-backup-cron.sh` para editar el archivo.
 
![linux_admarch_script_bash.png](/img/user/Assets/linux_admarch/linux_admarch_script_bash.png)
1. `cat script-backup-cron.sh` mostramos el contenido, ahí podemos ver el script que hice.
2. `crontab -e` lanzamos el *-editor* de crontab.

![linux_admarch_cron_backupscript.png](/img/user/Assets/linux_admarch/linux_admarch_cron_backupscript.png)
- Crontab no es más que un archivo con instrucciones en texto
- Dentro del mismo archivo están las instrucciones de uso.

La configuración va así:
1. hora, día, comando.
2. hora está dividido en minutos, horas
3. día está dividido en día del mes, mes, día de la semana
4. se pueden usar asteriscos `*` para indicar que sean "todos"
5. el comando a ejecutar puede ser un linkeo externo (como la primera línea que ejecuta el script indicado)
6. el comando puede ser dentro de la misma linea (como la segunda línea)

Es importante automatizar ciertos procesos para disminuir el error humano y mejora la eficiencia. Mientras menos tenga que intervenir el usuario en tareas repetitivas, menos espacio dejas para errores por negligencia. Es también importante realizar backups constantes de archivos importantes, como [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#6.- Find e importancia de logs\|mencionamos en este apartado]].
Cron es una poderosa herramienta para automatizar los procesos más tediosos pero importantes. Nos permite automatizar tareas según frecuencia en horas, días o incluso meses. Las tareas se ejecutarán aún cuando el equipo se haya reiniciado, dada la consistencia. Además es bastante sencillo de utilizar.

## 5.- Automatización de un reporte de monitoreo e importancia.
En este apartado:
- Crear una tarea de cron que automatice un proceso
- Dicho proceso tendrá una salida que se guardará en un archivo
- Importancia del monitoreo de recursos

Nuevamente podemos realizarlo a través de un script o directo a Cron.
En esta oportunidad, con un script es una tarea más compleja pero de todas formas haremos ambos.
![linux_admarch_comprob_scri.png](/img/user/Assets/linux_admarch/linux_admarch_comprob_scri.png)
Creamos el archivo, listamos y lo editamos con nano.

![linux_admarch_bash_.png](/img/user/Assets/linux_admarch/linux_admarch_bash_.png)
Creamos el script.
Ahora vamos a linkearlo en crontab
![linux_admarch_crontab_script_log.png](/img/user/Assets/linux_admarch/linux_admarch_crontab_script_log.png)
En la 3ra linea tenemos el linkeo del script, similar al de la linea 1.
En la 4ta linea tenemos el comando directo.

Ahora, la forma dentro de crontab puede sonar tentativa por simplicidad pero es importante mencionar que es menos modificable. Si quisiéramos hacer lo mismo que en el script, tendríamos una linea más compleja con información, la cual puede resultar difícil de leer si tenemos muchas automatizaciones.

Monitorear regularmente los recursos del sistema es importante para detectar anomalías y mantener un ojo en cuando podemos necesitar una mantención. También nos ayuda a analizar el rendimiento, reconocer cuándo el disco se llenará y así tomar acciones preventivas.
También es importantísimo al momento de cumplir normativas de una empresa o para análisis forenses.

Similar a crontab también tenemos `nagios` que nos puede ayudar a levantar alertas para ello. `Grafana` también es uno muy útil ya que nos puede mostrar visualizaciones para hacer más legible la información.

---
# Conclusión

El manejo de herramientas y comandos en Linux es esencial para lograr un desempeño óptimo en la administración. Aunque Linux es conocido por su curva de aprendizaje y su interfaz menos amigable en comparación con otros sistemas operativos más populares, sus ventajas se hacen evidentes a medida que nos familiarizamos con sus capacidades.

El uso de herramientas como **cron** facilita la automatización de tareas, permitiendo una gestión eficiente y programada de procesos repetitivos, como backups y reportes. Esto no solo ahorra tiempo, sino que también minimiza el riesgo de errores humanos y asegura la consistencia en las tareas de mantenimiento del sistema.

Además, comandos como **grep** resultan fundamentales para el filtrado y la búsqueda de información específica en el sistema, mejorando la eficiencia.
A través de estos ejercicios, hemos desarrollado habilidades prácticas en la administración de Linux y hemos obtenido una comprensión más profunda del sistema. La capacidad de gestionar procesos, configurar tareas y realizar monitoreo de recursos proporciona una base sólida, destacando las fortalezas y flexibilidad de Linux en comparación con otros entornos.

---
# Anexo: Comandos utilizados

- `cd`: Change directory, cambiar de directorio
- `ls`: `ls` lista los archivos y directorios dentro de un directorio. El argumento `-li` dice:
	- `l`: Mostrar información de permisos, propietario, grupo, tamaño, fecha de modificación y nombre
	- `i`: Mostrar el inodo
	- `h`: lo hace "humanamente legible", es decir, transforma los tamaños de sólo a bytes a un formato más legible
- `ln`: Link, linkea un archivo a otro, creando un enlace duro.
	- `-s`: indica que es un enlace simbólico
- `touch`: Crea un archivo nuevo
- `cat`: Concat. Nos muestra los contenidos o concatena archivos
- `nano`: Abre nano, el editor de texto en el CLI.
- `useradd`: Agregar usuario.
	- `-u`: para asignarle una ID
	- `-s`: para indicarle un shell a utilizar
- `apt`: Comando para realizar acciones sobre aplicaciones
	- `install`: con esto le indicamos a `apt` que queremos instalar un nuevo paquete
- `groupadd`: Creamos un nuevo grupo.
	- `-g`: para especificar la id, ya sea al momento de crearlo o asignarlo
- `usermod`: Modificar usuario
	- `-a`: append. indica que se debe agregar x a y
	- `-G`: Indica el grupo. Por lo tanto, al usarlo como `-aG` le decimos que debe agregar al grupo
- `groups`: Comando para listar los grupos a los que pertenece el usuario actual (sin parámetros) o a los de los usuarios que le pasamos.
- `id`: Muestra información detallada sobre usuario.
- `grep`: comando para buscar y filtrar texto dentro de archivos o resultados de otros comandos. Significa `global regular expression print` - 'Impresora global de expresiones regulares'
	- Al ser un comando de expresiones regulares, los parámetros son diversos.
	- <a href='https://regex101.com/'>Una buena página para practicar y aprender expresiones regulares</a>
- `echo "texto" > example.txt`: Echo es un comando para mostrar texto en el terminal. Literalmente hace "eco" de lo que le decimos.
	- `>`: se llama redirección de salida, con esto le indicamos que lo que entrega echo, sea redirigido al archivo example.txt
- `rm`: Remove. Literalmente remover, eliminar.
- `find /donde/ "que"`: Buscar.
	- `-name`: especifica que estamos buscando archivos a través de su nombre.
	- `-type`: especifica que estamos buscando archivos según un tipo, le entregamos `f` para decirle que busque solo `files`
- `awk`: lenguaje interno utilizado para procesar texto.
- `sudo`: super user do. Ejecutar el siguiente comando con privilegios elevados.
- `ps`: Process status. Muestra un snapshot de los procesos
	- `aux` muestra todos los procesos con detalles.
	- podemos combinarlo con `grep` a través de un pipe `|` para filtrar y destacar
- `pstree`: Muestra snapshot de los procesos en formato de árbol, con las jerarquías padre-hijo
- `top`: Muestra procesos en tiempo real detallando uso de recursos
- `htop`: Lo mismo que `top` pero con un formateo más amigable y otras funcionalidades adicionales.
- `fg`: Foreground. Trae el proceso más recientemente suspendido de vuelta.
- `kill pid`: "mata" un proceso o lo termina. Sin argumentos le envía una señal 15 (de terminación), lo cual le da tiempo para cerrar y limpiar. En este caso de uso le dimos -9 y 5113 donde -9 le da la orden de terminarlo sí o sí y 5113 es el pid (process id).
	- Importante notar que nano no se cerraría con `kill 5113` al estar suspendido.
- `crontab`: Usar crontab, el argumento `-e` abre la edición de sus parámetros.