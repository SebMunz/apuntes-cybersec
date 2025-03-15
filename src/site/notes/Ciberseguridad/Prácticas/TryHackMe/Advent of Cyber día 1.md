---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 1/"}
---

Qué aplicamos:
- OPSEC y OSINT
- Herramientas como exiftool y comandos básicos

Objetivos:
- Investigar links maliciosos
- Aprender sobre OPSEC
- Aprender sobre rastreo para atribuir identidades en las investigaciones

---

# Comienzo

Para resolver este desafío debemos iniciar la máquina y el attackbox.
De la máquina, accedemos a la dirección IP que se nos proporciona:
![](https://i.imgur.com/YLWjDNG.png)
La página se nos presenta como un clásico conversor de youtube.
Según la narrativa del desafío, este tipo de páginas se nos presentan con una sola función: descargar y/o convertir videos a otro formato. Este tipo de páginas, sin embargo, suelen ser usados de forma maliciosa.

Probemos a descargar <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">una canción</a> y ver qué sucede.
![](https://i.imgur.com/zuo7IZx.png)
El zip contiene los siguientes archivos:
![](https://i.imgur.com/wOHNBfS.png)
Podemos notar varias cosas extrañas:
El primer archivo:
- Tiene una falta ortográfica (soMg), su tamaño es de bajísimo para una canción y la fecha de modificación no coincide, indicando que no se ha hecho una conversión, si no, descargado algo previamente creado.
El segundo archivo:
- Tiene el mismo tema con la fecha de modificación, todo lo demás aparenta estar en orden.

Para determinar su contenido, podemos utilizar el comando `file` que nos entrega información del archivo.
Abrimos la terminal, nos dirigimos a la carpeta donde descomprimimos y ejecutamos el comando.
![](https://i.imgur.com/NCqw2ZJ.png)
El archivo song.mp3 no aparenta tener nada raro, es un archivo de audio.
Sin embargo, el archivo somg.mp3 nos muestra que en realidad es un archivo de atajo de windows, apunta a un archivo en particular y lo más importante: tiene argumentos de línea de comandos, por lo que nos dice que es un script.

Utilicemos exiftools para investigar más a fondo:
`exiftool somg.mp3`
![](https://i.imgur.com/I3Ayes0.png)
Con esto podemos ver que es un archivo `.lnk` (atajo), que apunta a abrir `powershell.exe` y le entrega diversos argumentos:
- `-ep Bypass -nop` deshabilita las restricciones de powershell, de esta manera permite el lanzamiento de scripts sin interrupciones por parte de la seguridad de windows
- `DownloadFile` nos trae un archivo desde internet, en este caso descarga `IS.ps1` desde <a href="https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1](https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1">esta ruta</a>.
- Posteriormente es ejecutado.

Si descargamos el archivo en cuestión y revisamos el contenido del script nos encontramos con esto:
![](https://i.imgur.com/nFxo4Qb.png)
Básicamente su función es robarse la información de las cryptowallets y mandarlo a un servidor.
Por alguna razón, el culpable lo firmó: `M.M`

# Ahora qué?

Pudimos notar que el archivo se descargaba desde github. Así que quizás podriamos empezar por ahí.
Buscamos `Created by the one and only M.M.` en github.
![](https://i.imgur.com/dkzrM3X.png)

(Por supuesto que la gente lo ha copiado...) Pero, al menos sabemos que hay una persona llamada MM entre ellas.
Hay varias conversaciones interesantes en este lugar pero con esto nos basta:
![](https://i.imgur.com/Nx7nvcU.png)

Tenemos nuestra primer hit.

# OPSEC

Operational Security (OPSEC) son principios y tácticas utilizadas para proteger la seguridad de un operador o de una operación. Como el uso de nombres claves o el uso de proxys.
En la ciberseguridad, cuando un actor malicioso falla en esto puede llegar a exponer su identidad, como ha ocurrido en algunos casos famosos como el de AlphaBay, un sitio de intercambios ilegales en la darknet, donde Alexandre Cazes reutilizó su correo (_pimp_alex_91@hotmail.com_) en diversos sitios, incluyendo su propio linkedin con su negocio legítimo.

Algunas de las fallas de OPSEC:
- Reutilizar correos, nombres de usuario o nombres de cuentas en múltiples plataformas
- Usar metadatos identificables y rastreables en documentos o fotos donde se podría revelar información de GPS, fechas, etc.
- Postear en foros públicos de fácil acceso (como en este caso) donde se podría comprometer la identidad
- No utilizar VPN, proxys u otras formas de esconderse

Lo que aquí realizamos es un ejemplo sencillo de [[Ciberseguridad/Habilidades y conocimientos básicos/Fundamentos de seguridad/OSINT\|OSINT]]. Si bien estos casos son posibles de ocurrir, es poco frecuente encontrar errores tan garrafales.

Ya con esto, podemos responder las preguntas que nos presenta TryHackMe:

- ¿Quién es el autor real de la canción song.mp3?
	- Para ello debemos utilizar exiftools
- El script envía la información a un servidor C2 (Command and Control Server), ¿cuál es la url?.
	- Esto aparece en el comando
- ¿Quién es M.M.?
	- Debemos revisar su perfil de Github, en él encontraremos la respuesta
- ¿Cuántos commits se realizaron el repo del issue?
	- Revisar el repositorio original de [Bloatware-WarevilleTHM](https://github.com/Bloatware-WarevilleTHM)

---

Con esto completamos el desafío del día 1
![](https://i.imgur.com/5gCyypP.png)

Ahora, vamos al [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 2\|Advent of Cyber día 2]].