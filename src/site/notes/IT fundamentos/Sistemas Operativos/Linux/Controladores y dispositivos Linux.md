---
{"dg-publish":true,"permalink":"/IT fundamentos/Sistemas Operativos/Linux/Controladores y dispositivos Linux/"}
---

Los sistemas operativos basados en Linux reconocen los dispositivos conectados a la computadora como si fueran archivos. En Linux, los dispositivos se encuentran en el directorio /dev.

ej:
- **/dev/sda**: Primera unidad SCSI
- **/dev/sr0**: Primera unidad de disco óptica
- **/dev/usb**: Dispositivo USB
- **/dev/usbhid**: Mouse USB
- **/dev/usb/lp0**: Impresora USB
- **/dev/null**: Dispositivo de descarte

Estas son algunas de las categorías de dispositivos Linux:

- **Dispositivos de almacenamiento en bloques:** Pueden contener datos, como los discos duros, las unidades USB y los sistemas de archivos.
- **Dispositivos de caracteres:** Pueden ingresar o generar datos de un carácter a la vez, como teclados, impresoras y monitores.
- **Dispositivos de canalización:** Son similares a los dispositivos de caracteres, pero los dispositivos de canalización envían sus resultados a un proceso que se ejecuta en la máquina de Linux, en vez de a un monitor o una impresora.
- **Dispositivos de socket:** Son similares a los dispositivos de canalización, pero los dispositivos de socket ayudan a que varios procesos se comuniquen entre sí.
- 
# Cómo instalar un dispositivo en Linux

Los métodos para instalar dispositivos en Linux pueden variar de una versión a otra. Los siguientes funcionan en Linux con Red Hat 9 + GNOME.

### **Detección automática de dispositivos con udev**
Udev es un administrador de dispositivos que crea y quita archivos de dispositivos automáticamente en Linux cuando se conectan y desconectan los dispositivos asociados. Udev tiene un daemon en ejecución en Linux que escucha los mensajes del kernel sobre los dispositivos que se conectan a la máquina y se desconectan de ella.

### **Instalación a través de una interfaz de usuario (GNOME)**
1. En la interfaz de usuario GNOME, abre el menú **Configuración**. 
2. En el menú lateral izquierdo, selecciona **Impresoras**.
3. Haz clic en el botón **Desbloquear** en la esquina superior derecha para cambiar la configuración del sistema. Ten presente que tu cuenta de usuario debe tener privilegios de _superusuario_, _sudo_ o _printadmin_ para desbloquear la configuración del sistema para las impresoras.
4. Se abrirá un cuadro de diálogo con una lista de las impresoras disponibles. Si la red tiene una gran cantidad de impresoras, puedes buscarla por dirección IP o nombre de host.
5. Selecciona la impresora que quieres instalar en el sistema local y haz clic en **Añadir**.
6. La ficha de la impresora aparecerá en la ventana **Configuración** para las **impresoras.**
7. En la esquina superior derecha de la ficha de la impresora, haz clic en el ícono **Configuración de la impresora** y selecciona **Detalles de la impresora** en el menú emergente.
8. Los detalles de la impresora se abrirán en una ventana nueva. Deberías tener tres opciones para instalar el controlador de la impresora:
    1. **Buscar controladores:** El Centro de control de GNOME buscará automáticamente el controlador en los repositorios de controladores mediante PackageKit.
    2. **Seleccionar de la base de datos:** Selecciona un controlador de forma manual a partir de las bases de datos instaladas en el sistema Linux.
    3. **Instalar archivo PPD:** Selecciona manualmente a partir de una lista de archivos de Postscript Printer Description (PPD), que se pueden usar como controladores de impresoras.


### **Instalación mediante la línea de comandos**

Red Hat Linux usa Common Unix Printing System (CUPS) para administrar impresoras desde la línea de comandos. Los servidores de CUPS transmiten datos a los clientes para instalar impresoras automáticamente en máquinas Linux. Sin embargo, en los entornos de red que tienen varias impresoras, puede ser más conveniente instalar impresoras específicas manualmente a través de la línea de comandos.

- En la línea de comandos, ingresa **$ lpadmin -pnombredelaimpresora -m nombredelarchivodelcontrolador.ppd**
    - **lpadmin** es el comando del administrador de impresoras.
    - El parámetro **-p nombredelaimpresora** agrega o modifica la impresora nombrada.
    - El parámetro **-m nombredelarchivodelcontrolador.ppd** instala el nombre de archivo del controlador de Postscript Printer Description (PPD) que proporcionas. El archivo debe almacenarse en el directorio **/usr/share/cups/model/**.
    - Ingresa **$ man lpadmin** para abrir el manual del comando lpadmin y encontrar opciones de línea de comandos adicionales.

# Cómo comprobar si un dispositivo está instalado

**Mediante una interfaz de usuario como GNOME**
1. En la interfaz de usuario GNOME, abre el menú **Configuración**.
2. Explora cada dispositivo configurado en el menú lateral izquierdo.
3. Los dispositivos conectados del tipo seleccionado aparecerán en el panel de la ventana a la derecha.

**Mediante la línea de comandos**
La forma más común de comprobar si un dispositivo está instalado es usar el comando `ls` 
- **$ ls /dev**: Muestra una lista de todos los dispositivos de la carpeta /dev.
- **$ lscpci**: Muestra una lista de los dispositivos instalados en el bus PCI.
- **$ lsusb**: Muestra una lista de los dispositivos instalados en el bus USB.
- **$ lsscsi**: Muestra una lista de los dispositivos SCSI, como los discos duros.
- **$ lpstat -p**: Muestra una lista de todas las impresoras y si están habilitadas.
- **$ dmesg**: Muestra una lista de los dispositivos reconocidos por el kernel.

> Extraido del curso de Google para Soporte TI (2024)