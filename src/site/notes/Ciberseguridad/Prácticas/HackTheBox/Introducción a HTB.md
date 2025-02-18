---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/HackTheBox/Introducción a HTB/"}
---


# Introducción

HTB o HackTheBox es una plataforma de aprendizaje, prácticas y entrenamiento para ciberseguridad.
Su plataforma <a href="https://academy.hackthebox.com/">Academy</a> es la enteramente enfocada en el aprendizaje.

![](https://i.imgur.com/Uyoh8RQ.png)
En primer lugar nos registramos con el gran botón verde.

![](https://i.imgur.com/KVN8wev.png)
<div class="page-break" style="page-break-before: always;"></div>

Creamos nuestra cuenta y accedimos.
![](https://i.imgur.com/QpFnAfR.png)

Llegamos al dashboard, desde aquí en el sector de la izquierda tenemos lo siguiente:
![](https://i.imgur.com/YcVVQnj.png)
- El dashboard es nuestra parte inicial.-
- Exams corresponde al lugar donde podemos ver los exámenes que posee HTB.-
- Modules es el segmento donde podemos ver pequeños módulos de aprendizaje.
- Paths es donde podemos ver rutas de aprendizaje que comprenden varios módulos
- Academy x HTB Labs es un sector donde podemos ver las relaciones entre módulos, exámenes, pruebas y otros de HTB.

Importante mencionar que HTB funciona con "cubos" que son el equivalente a "monedas" de cambio. Con ellas desbloqueamos módulos. Para obtener cubos podemos comprarlos, recibirlos con una suscripción o completando módulos.
![](https://i.imgur.com/Urhk8ld.png)
<div class="page-break" style="page-break-before: always;"></div>


--- 
# Linux Fundamentals

Para ejemplificar, haremos el módulo de Linux Fundamentals.
La forma más rápida es buscarlo arriba, pero nos enrolaremos en el learning path de Fundamentos de sistemas operativos:
![](https://i.imgur.com/FSRhnlO.png)
Presionamos en Enroll y nos llevará de vuelta al dashboard desde donde podemos desbloquear el primer módulo con nuestros cubos.
![](https://i.imgur.com/NcxgHCi.png)

Le damos a unlock y start
![](https://i.imgur.com/0k2h9gd.png)
<div class="page-break" style="page-break-before: always;"></div>

---

# Comandos extraídos del aprendizaje

- `whoami`
	- Muestra el usuario actual
- `hostname`
	- Muestra el nombre del host/equipo
- `id`
	- Muestra información sobre el usuario, el User ID, Group ID y los grupos actuales.
- `uname`
	- Muestra información sobre el sistema operativo, incluyendo nombre del SO, versión, arquitectura del procesador y otros
- `ifconfig`
	- Muestra información sobre las interfaces de red de la máquina, direcciones IP, máscaras de red, MAC, etc
	- **Si bien se sigue usando, está deprecado**, en su lugar usar `ip`
- `ps`
	- Muestra los procesos en ejecución, Process ID, nombre, usuario que ejecuta y más.
	- Se le pueden agregar parámetros para mostrar aún más información
- `pwd`
	- Muestra la ruta absoluta en la nos encontramos
- `ls`
	- Muestra un listado de los archivos del directorio actual
	- Los parámetros más usados son sin duda `-l` (más detalles) y `-a`(muestra ocultos)
- `lsusb`
	- Muestra información sobre los USB conectados
- `lsof`
	- Muestra un listado de los archivos que están siendo usados por los procesos ejecutados en el sistema.