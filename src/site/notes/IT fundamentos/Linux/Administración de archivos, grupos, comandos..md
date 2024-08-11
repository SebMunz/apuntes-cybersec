---
{"dg-publish":true,"permalink":"/IT fundamentos/Linux/Administración de archivos, grupos, comandos./"}
---

Linux posee distintas maneras de moverse entre archivos y para la administración de grupos, usuarios, permisos y procesos.

En este apartado, ejecutaré algunos comandos a modo de ejercicio.
Para este ejercicio utilizaremos la versión mas reciente de ubuntu, montada en virtualbox.
![Pasted image 20240810204548.png](/img/user/Pasted%20image%2020240810204548.png)

---
# Manejo de archivos y directorios

## 1.-
En este apartado:
- Crearemos un archivo
- Agregaremos contenido
- Crearemos un enlace duro apuntando a dicho archivo
- Notaremos los inodos
- Anotaciones adicionales

![Pasted image 20240810213344.png](/img/user/Pasted%20image%2020240810213344.png)

1. Haremos `cd Downloads/` para movernos a la carpeta Downloads
2. `ls` para listar que la carpeta esta vacia
3. `touch original.txt` con touch le indicamos que crearemos un archivo con el nombre original.txt
4. `ls` nuevamente para checar que esté nuestro archivo
5. `cat original.txt` para revisar que el archivo esté vacío
6. `nano original.txt` para editar original.txt usando el editor nano

Se nos abrirá nano, un editor de texto en el terminal.
![Pasted image 20240810213819.png](/img/user/Pasted%20image%2020240810213819.png)
Posteriormente le damos a `CTRL + X` en el teclado para cerrar, escribimos Y para aceptar los cambios y presionamos `ENTER` para que se guarde con el mismo nombre.
Posteriormente haremos nuevamente `cat original.txt` para ver que se haya guardado correctamente:
![Pasted image 20240810214031.png](/img/user/Pasted%20image%2020240810214031.png)

Ahora crearemos un enlace duro y listaremos los inodos y permisos.
![Pasted image 20240810214858.png](/img/user/Pasted%20image%2020240810214858.png)
1. `ln -i original.txt duro_link.hd` para creación
2. `ls` para revisar su existencia
3. `ls -li` para listar inodos, permisos e información relevante.
Aquí podemos notar que ambos archivos son exactamente iguales, tanto el inodo, permisos y fecha de creación pero su nombre es distinto.

#### Explicaciones y comentarios:
Un inodo es un identificador único para el archivo, el cual contiene los metadatos del archivo.

El enlace duro es un *alias* para un archivo. Es decir, es otra forma de acceder al mismo inodo.
En este caso, `duro_link.hd` y `original.txt`, lo que están haciendo ambos es acceder al inodo `918265`, con nombres diferentes.
Originalmente pensaba que eran lo mismo que los enlaces simbólicos (soft links - accesos directos) pero investigando un poco más encontré una analogía buenísima: ==Los enlaces duros son dos números de teléfono distintos para la misma linea, mientras que un enlace simbólico son dos lineas diferentes para la misma casa==. Esto quiere decir que un enlace duro de un archivo es el mismo archivo (inodo), accedido con otro nombre. Pero un enlace simbólico es otra forma de acceder a un archivo con un inodo diferente.
Las ventajas de un enlace duro parecen superiores ya que son más rápidos al apuntar al mismo inodo, pero no pueden cruzar sistemas y no pueden apuntar a directorios. En cambio los enlaces simbólicos son más flexibles en ese sentido pero se pueden romper más fácilmente.

Los enlaces duros pueden ser ideales cuando necesitamos múltiples nombres para un mismo archivo dentro del mismo sistema y queremos darle mayor seguridad a que el archivo no será accidentalmente borrado.

**¿Qué pasa si elimino el archivo original?**
Si elimino el archivo original, todos los enlaces duros se vuelven inválidos. Sin embargo, el archivo sigue existiendo en el disco porque su inodo sigue estando activo. Recién cuando eliminemos todos los enlaces duros, su inodo desaparecerá.
## 2.-
En este apartado:
- Modificaremos el archivo original.txt
- Mostraremos el contenido de duro_link.hd
![Pasted image 20240810223647.png](/img/user/Pasted%20image%2020240810223647.png)
Como podemos ver, las modificaciones hechas en el archivo `original.txt`, también se ven reflejadas en `duro_link.hd`. La explicación es la misma que hice [[IT fundamentos/Linux/Administración de archivos, grupos, comandos.#Explicaciones y comentarios\|aquí]]. Ambos son el mismo archivo, pero accedidos de distinta forma.
## 3.-
En este apartado:
- Eliminaremos original.txt
- Mostraremos su contenido desde duro_link.hd
- Verificación de su estado
![Pasted image 20240810224844.png](/img/user/Pasted%20image%2020240810224844.png)
1. `rm original.txt`: eliminamos original.txt
2. `cat duro_link.hd`: comprobamos que el contenido sigue siendo el mismo
3. `ls -li`: verificamos *qué* hay en la carpeta.

Si bien, eliminamos el archivo original, su enlace duro sigue estando ahí. Como mencioné [[IT fundamentos/Linux/Administración de archivos, grupos, comandos.#Explicaciones y comentarios\|aquí]], aplica el mismo concepto. Su inodo sigue existiendo y es a eso a lo que estamos apuntando.
## 4.-
En este apartado:
- Crearemos un nuevo archivo: example.txt
- Crearemos un enlace simbólico que apunte a example.txt

![Pasted image 20240810225905.png](/img/user/Pasted%20image%2020240810225905.png)
- `touch example.txt`: creamos example.txt
- `echo "texto" > example.txt`: echo para darle el texto, `>` para indicarle que la salida es hacia example.txt
- `cat example.txt`: para verificar su contenido
- `ln -s example.txt symlink.sl`: Creamos un enlace, con el argumento `-s` le indicamos que es un enlace simbólico
- `ls -li`: listamos la información de la carpeta.

Aquí podemos notar que los inodos de example y symlink son distintos. Además, podemos corroborar que los permisos son diferentes, incluye una `l` que indica que es un enlace simbólico, tiene fechas distintas y además symlink.sl -> example.txt nos indica que este archivo está apuntando a otro.
Con esta información podemos concluir definitivamente que un enlace simbólico es diametralmente diferente a un enlace duro.

## 5.-
En este apartado:
- Eliminaremos example.txt
- Comprobaremos el contenido a través de su enlace simbólico
- Verificar estado

![Pasted image 20240810231133.png](/img/user/Pasted%20image%2020240810231133.png)
1. `rm example.txt`: eliminamos example
2. `cat symlink.sl`: revisamos el contenido, notamos que indica que el archivo no existe
3. `ls -li`: El archivo en realidad está ahí pero ahora su dirección apunta en rojo.

¿Qué ocurre?, los enlaces simbólicos al apuntar hacia otros archivos, no funcionan por sí solos. Es por esto que me arroja que el archivo no existe, porque en realidad me está diciendo que el archivo al que apunta, no existe.
Aquí [[IT fundamentos/Linux/Administración de archivos, grupos, comandos.#Explicaciones y comentarios\|nuevamente podemos comprarlo con mi respuesta previa]]. Los enlaces simbólicos apuntan *al archivo* y no al *inodo* como lo hacíamos con los enlaces duros.

## 6.-
En este apartado:
- Con find buscaremos los archivos .log en un directorio particular
- Crearemos copias a un nuevo directorio
- La importancia de los logs

![Pasted image 20240811001316.png](/img/user/Pasted%20image%2020240811001316.png)
- `find /var/log -type f -name "*.log"`: iniciamos la búsqueda de los archivos log

![Pasted image 20240811001610.png](/img/user/Pasted%20image%2020240811001610.png)
- `sudo rm /tmp/copias`: el método que utilicé originalmente me creó un archivo binario que sólo podía eliminar de esta forma
- `sudo mkdir -p /tmp/copia_logs`: creamos el directorio dentro de la carpeta tmp
- `sudo find /var/log -type f -name "*.log" -exec cp {} /tmp/copia_logs/ \;`: básicamente busca los archivos y por cada archivo que encuentre ejecuta el comando `cp`
- `ls /tmp/copia_logs`: revisamos que estén las copias de los archivos.

Crear copias de los logs es crucial para mantener la integridad de los mismos. Con estas copias de seguridad podemos asegurarnos que los contenidos no han sido modificados y que están disponibles en todo momento. [[Ciberseguridad/Habilidades y conocimientos básicos/Logs\|En este enlace de mis apuntes, hablo un poco sobre logs]]

## 7.-
En este apartado:
- Comando para buscar archivos mayores a 5MB, listando sus nombres y tamaños
![Pasted image 20240811003550.png](/img/user/Pasted%20image%2020240811003550.png)
1. `find ~/ -type f -size +5M -exec ls -lh {} +`: Con este comando encontramos todos los archivos mayores a 5MB, pero dado que es una instalación fresca, no encontrará nada así que realizamos el siguiente:
2. `find ~/ -type f -size +1M -exec ls -lh {} +`: Es el mismo comando pero cambiamos que sea mayores a 1MB. Esto nos despliega como resultado los permisos, el autor, dueño, tamaño, fecha de modificación y localización, pero creo que podría mejorarse.

![Pasted image 20240811004113.png](/img/user/Pasted%20image%2020240811004113.png)
Este comando es similar, pero un poco más complejo. El resultado de `find` se lo pasamos (`|`) a `awk` (un lenguaje de programación interno de linea de comandos usado para procesar y analizar textos), luego imprimimos (`print`) los parámetros $9 y $5 concatenando un `:` entremedio.

La utilidad de este tipo de comandos es útil a la hora de tomar respaldos, de administrar el espacio, ayuda a hacer mantenimiento de los computadores y ayuda a identificar archivos obsoletos, con esto podemos fácilmente identificar archivos problemáticos, podriamos combinarlo con otros comandos para automáticamente eliminar todos los archivos mayores que un determinado tamaño o podriamos generar un informe con ello.

##### Comandos utilizados
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
- `echo "texto" > example.txt`: Echo es un comando para mostrar texto en el terminal. Literalmente hace "eco" de lo que le decimos.
	- `>`: se llama redirección de salida, con esto le indicamos que lo que entrega echo, sea redirigido al archivo example.txt
- `rm`: Remove. Literalmente remover, eliminar.
- `find /donde/ "que"`: Buscar.
	- `-name`: especifica que estamos buscando archivos a través de su nombre.
	- `-type`: especifica que estamos buscando archivos según un tipo, le entregamos `f` para decirle que busque solo `files`
- `awk`: lenguaje interno utilizado para procesar texto.