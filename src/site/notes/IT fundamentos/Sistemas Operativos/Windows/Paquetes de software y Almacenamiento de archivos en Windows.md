---
{"dg-publish":true,"permalink":"/IT fundamentos/Sistemas Operativos/Windows/Paquetes de software y Almacenamiento de archivos en Windows/"}
---

Instalación (y eliminación) de software a través de GUI y CLI en Windows.
Se instalará Sublime, se usará des/compresión en formato `.tar` y se usará Powershell para la des/instalación.

# Instalación Sublime Text con GUI

Lo primero será descargar el archivo desde la su web.
![](https://i.imgur.com/VK5oFjy.png)

Lo que nos deja con este archivo en descargas
![](https://i.imgur.com/G2wOFSl.png)

Simplemente le damos doble click. Para empezar la instalación
![](https://i.imgur.com/aHdkGu8.png)
Utilizamos la ubicación predeterminada, continuar y finalmente la botón Install.

# Extracción de archivos con 7zip y Powershell
7zip es un gestor de archivos comprimidos. La forma más fácil a través de GUI es simplemente hacerle click derecho -> 7zip en el menu contextual -> extraer aquí
![](https://i.imgur.com/Ysvu53n.png)
Y tenemos los archivos descomprimidos.
![](https://i.imgur.com/3ZfoEab.png)

A través de Powershell la compresión se realiza de la siguiente forma:
![](https://i.imgur.com/8Zs4zSS.png)
Básicamente nos movemos con `cd` a la carpeta con los archivos que queremos comprimir.
`Compress-Archive -Path x nombre.zip` Damos la instrucción, le decimos `-Path` para indicar que le daremos los paths a los archivos que queremos comprimir y terminamos con `nombre.zip` indicándole el nombre del archivo zip

# Instalación VLC con Powershell
Muchísimo más engorroso y complejo, necesitamos obtener el archivo desde la url donde se encuentra el archivo de descarga:
![](https://i.imgur.com/m31ktfR.png)
*nota: corrí dos veces el mismo comando por error pero esto no afecta el resultado, simplemente omitir*

Básicamente:
1. `$VLC_URL = "[https://get.videolan.org/vlc/last/win64/](https://get.videolan.org/vlc/last/win64/)"`  
	- Se define una variable llamada `$VLC_URL` con la dirección URL de la página de descarga de la última versión de VLC para Windows 64 bits.
2. `$GET_HTML = Invoke-WebRequest $VLC_URL`
	- Se utiliza el cmdlet `Invoke-WebRequest` para realizar una solicitud web a la URL almacenada en `$VLC_URL` y se almacena el contenido HTML de la página en la variable `$GET_HTML`.
3. `$FILE = $GET_HTML.Links | Select-Object @{Label='href';Expression={@{$true=$_.href}[$_.href.EndsWith('win64.exe')]}} | Select-Object -ExpandProperty href`
	- Se utiliza el cmdlet `Select-Object` para filtrar los enlaces (`Links`) de la página HTML y seleccionar el que termina con `win64.exe` (el instalador de VLC para Windows 64 bits). El resultado se almacena en la variable `$FILE`.
4. `$URL = ($VLC_URL+$FILE)`
    - Se construye la URL completa del archivo de instalación de VLC combinando la URL base (`$VLC_URL`) con el nombre del archivo (`$FILE`).
5. `$DOWNLOAD_DIR = "C:\users\qwiklabs\Downloads"`
	- Se define una variable llamada `$DOWNLOAD_DIR` con la ruta del directorio de descargas.
6. `$OUTPUT_FILE = ($DOWNLOAD_DIR+$FILE)`
    - Se construye la ruta completa del archivo de salida combinando el directorio de descargas (`$DOWNLOAD_DIR`) con el nombre del archivo (`$FILE`).
7. `(new-object System.Net.WebClient).DownloadFile($URL, $OUTPUT_FILE)`
    - Se crea un nuevo objeto `WebClient` y se utiliza su método `DownloadFile` para descargar el archivo desde la URL (`$URL`) y guardarlo en la ruta de salida (`$OUTPUT_FILE`).
8. `cmd.exe /c $OUTPUT_FILE /S`
	- Se ejecuta el archivo de instalación de VLC (`$OUTPUT_FILE`) con el parámetro `/S` para realizar una instalación silenciosa (sin interfaz gráfica). El comando `cmd.exe /c` se utiliza para ejecutar el comando en una nueva instancia de la consola de comandos.
# Desintalación GIMP con Powershell
Afortunadamente la desinstalación es mucho más simple.
`cmd.exe /c "C:\Program Files\GIMP 2\uninst\unins000.exe" /VERYSILENT /NORESTART`
Le decimos que con cmd ejecute el archivo unins000.exe en modo silencioso (sin mostrar nada en consola) y que no reinicie.

Luego corremos un `Get-Package` para verificar su desinstalación.

