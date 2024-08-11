---
{"dg-publish":true,"permalink":"/IT fundamentos/Sistemas Operativos/"}
---

El sistema operativo es aquel que maneja los recursos de nuestro computador. Es también aquel encargado de la interacción usuario/máquina.
Existen dos partes principales:
- Kernel
- Espacio de usuario

## Kernel
El **kernel** es el núcleo de un sistema operativo. Es el componente central que actúa como un puente entre el hardware del computador y el software que corre sobre él. El kernel gestiona las tareas más básicas y fundamentales del sistema, tales como:

- **Gestión de procesos**: Controla qué procesos (programas en ejecución) tienen acceso a la CPU y en qué momento.
- **Gestión de memoria**: Asigna y supervisa la memoria para diferentes programas, asegurándose de que no se interfieran entre sí.
- **Gestión de dispositivos**: Coordina la comunicación entre el sistema operativo y el hardware del computador, como discos duros, tarjetas gráficas y otros periféricos.
- **Gestión de archivos**: Facilita el acceso y almacenamiento de datos en sistemas de archivos.

El kernel opera en un espacio protegido de la memoria llamado **kernel space**. Esta protección evita que los programas de usuario (que operan en el **user space**) interfieran directamente con el hardware o con las tareas críticas del sistema, manteniendo así la estabilidad y seguridad del sistema operativo.
El kernel proporciona servicios y recursos a los programas en el user space a través de llamadas al sistema (system calls). Estas llamadas permiten a los programas solicitar acciones específicas, como leer o escribir archivos, crear nuevos procesos o comunicarse con dispositivos hardware, sin necesidad de interactuar directamente con el kernel.
## User Space
El **user space** es el área de la memoria donde corren los programas y aplicaciones que el usuario utiliza directamente. Estos programas incluyen:

- **Aplicaciones de usuario**: Como navegadores web, editores de texto, reproductores de música, etc.
- **Interfaz de usuario**: Elementos visuales e interactivos que permiten al usuario interactuar con el sistema operativo, como ventanas, menús y botones.

El user space está separado del kernel space para proteger la integridad del sistema. Si un programa en el user space falla o se comporta mal, no puede afectar directamente al kernel, lo cual ayuda a prevenir que el sistema operativo completo colapse.

---

# Archivos
Cada sistema operativo organiza, opera y monitorea de forma diferente los archivos.
Cada sistema es distinto, tiene distintas ventajas y desventajas. Cada sistema operativo recomienda alguno(s) en particular.
Por ej.
- Windows utiliza NTFS que incluye encriptación, accesos rápidos, seguridad, etc.
- Linux depende de la distro, una de las principales usadas es EX T4, compatible con sistemas EXT más antiguos.
En general, lo mejor es utilizar lo que el SO recomienda.

## Almacenamiento
Los datos se escriben en forma de bloques al disco, dichos bloques se reparten entre "los cajones" del mismo y se organizan en distintas partes según necesidad. Esto aumenta la velocidad de manejo, es más rápido acceder a varios bloques al mismo tiempo que a un solo gran bloque.
Los archivos, además, utilizan los metadatos (los datos de los datos). Dichos metadatos nos dicen básicamente todo lo que necesitamos saber sobre el archivo (permisos, dueños, tamaño, tipo, fechas).
La extensión del archivo nos dice su tipo, el tipo de archivo le dice al equipo cómo manejarlo, abrirlo, ejecutarlo.

# User Space
El user space es donde el usuario interactúa directamente con el computador. En este lugar es donde el usuario ejecutará la gran mayoría de acciones que desea realizar con el equipo, como navegar webs, utilizar aplicaciones o administrar una red.
El user space suele ser comunmente utilizado en una GUI, o graphic user interface, pero no siempre es así.
Una gran cantidad de veces necesitaremos conectarnos a un equipo que no tiene GUI y esto lo haremos a través del shell para así poder ejecutar comandos o realizar acciones que son solamente realizables a través del Shell..
El shell no es más que un interpretador de texto para comandos que le enviará al SO. El shell más común es quizás BASH.

# Registros
Otro aspecto importante de cada sistema operativo es la forma en que maneja registros.
Los registros son archivos que guardan información respecto a eventos del computador, esto ayuda a solucionar errores y monitorear el funcionamiento.
La mayoría de los SO maneja registros de la misma forma (archivos) pero no todos muestran la misma información por defecto. Cada sistema debe ser modificado según las necesidades del usuario.

# Booteo
Proceso de inicio del computador.
Lo más común es iniciar el computador a través del botón de inicio y dejar que haga su trabajo, sin embargo, no es la única forma.
También podemos configurar para que inicie desde el USB, cambiar el orden de discos que inician, hotswap, por red, etc.

Internamente el computador posee un mini sistema operativo, o un software de bajo nivel, llamado UEFI/BIOS el cual ejecuta pruebas de diagnóstico, configura el orden de arranque y configura el equipo previo al inicio a cualquier SO.

Entre otras formas de inciar el computador, además del botón de inicio, tenemos:
- Unidades externas (USB, discos ópticos, hotswap)
- Particiones de disco
- Inicio por red (Wake on LAN, remote access, LAN)

Cada una de ellas responde a diferentes necesidades.


---

# Windows

@TODO
Aquí van cosas sobre windows pero aún no lo hago

---

# [[Linux\|Linux]]

@TODO
Aquí van cosas sobre linux que aun no hago