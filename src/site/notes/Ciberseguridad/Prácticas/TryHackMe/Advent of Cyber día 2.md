---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 2/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 1\|Advent of Cyber día 1]]

Qué aplicamos:
- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR XDR#SIEM\|Herramientas SIEM]] con elastic SIEM
- Análisis SOC (Security Operations Center)
- Análisis de [[Fundamentos TI/Logs\|Logs]]

Objetivos:
- Entender el uso de las herramientas SIEM
- Investigar y lograr diferenciar **TRUE POSITIVE** y **FALSE POSITIVE**

---

# Comienzo

Los analistas SOC se encargan de monitorear y analizar eventos de seguridad en redes y sistemas, además de responder a las mismas.
Lo que tenemos que hacer en este desafío es analizar logs de un SIEM e investigar si lo que estamos viendo son true positive (amenazas reales) o false positives (alertas que saltaron pero que no eran realmente amenazas).

Lanzamos la máquina y nos conectamos a la url con las credenciales que nos proporcionan.
![](https://i.imgur.com/DEsADDw.png)
Nos vamos a Discover y nos encontramos con lo siguiente:
![](https://i.imgur.com/xGdNlwa.png)

Aún no hemos realizado ninguna búsqueda ni filtro. Para empezar, según la narrativa saltó una alarma el 1ro de Diciembre del 2024 entre 0900 y 0930. 
En el calendario, en la barra de búsqueda debemos seleccionar el time-frame. Le damos con absoluto e insertamos las fechas y horas desde y hasta cuando.
![](https://i.imgur.com/6weUg9Q.png)

![](https://i.imgur.com/grwoHqo.png)

En teoría, podríamos leer los logs así como están pero son poco amigables. Afortunadamente podemos agregar filtros, categorías y columnas para mejor organizar la información.
Según la narrativa de la práctica estamos buscando eventos relacionados a Powershell, por lo tanto nos sirve agregar las siguientes columnas:
- El nombre de host donde se corrió el comando. `host.hostname`
- El usuario que lo ejecutó. `user.name`
- Agregamos `event.category` para asegurar que estamos viendo la categoría correcta
- Para saber el comando agregamos `process.command_line`
- Para saber si el evento funcionó o no, agregamos `event.outcome`
![](https://i.imgur.com/pZ7aEPK.png)

Ahora podemos verlo más organizado.
Lo primero que podemos ver es que se corrió un comando codificado, que fue efectivo, que se corrió en distintas máquinas y que hubieron eventos de autenticación cada vez que se fue a correr el comando.
Algo que podríamos hacer es filtrar por IP para ver si hay algo de información útil:
Vamos a la izquierda a los filtros, agregamos `source.ip`, vamos al evento de autenticación, nos posicionamos sobre el símbolo **+**, con eso logramos que se filtre por esta categoría. No obtenemos nada útil, sólo podemos ver que son IP privadas locales.
![](https://i.imgur.com/n8vKz5L.png)
![](https://i.imgur.com/v5vGhcw.png)
Dado que no nos sirvió de mucho que digamos, vamos a quitar el filtro.

# Qué hacer ahora?
Las autenticaciones podrían venir desde mucho antes, por lo tanto vamos a aumentar el timeframe a un par de días antes y expandir las horas.
![](https://i.imgur.com/MJqInz5.png)
Esto ahora nos arroja 6814 actividades con un salto inmenso al final, claramente sucede algo.
![](https://i.imgur.com/mpkB1L2.png)
Vamos a aplicar los siguientes filtros:
- `user.name` en service_admin
- `source.ip` con la ip local 10.0.11.11

Con eso reducimos un poco la cantidad de hits, pero aún necesitamos más información.
![](https://i.imgur.com/nNAMZLK.png)

Agregamos un filtro para mostrar los resultados que NO incluyan esa ip.
Con ello notamos que hubieron miles de intentos fallidos antes de lograr conectarse.
Posteriormente podemos seguir indagando a través de los filtros. Podemos eliminar el filtro de ip y probar sólamente verificando las alertas de autenticación. A la larga, todo apuntaría a un ataque de fuerza bruta.

# Y el script?
Si recordamos el script que se ejecutó, el comando estaba codificado y no se revisó.
```
`C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -EncodedCommand SQBuAHMAdABhAGwAbAAtAFcAaQBuAGQAbwB3AHMAVQBwAGQAYQB0AGUAIAAtAEEAYwBjAGUAcAB0AEEAbABsACAALQBBAHUAdABvAFIAZQBiAG8AbwB0AA==`
```
Generalmente estas codificaciones son realizadas en Base64, por lo que vamos a <a href="https://gchq.github.io/CyberChef/">CyberChef</a> para decodificarla.
La recomendación general es no subir estas cosas online, por posibles filtraciones de datos sensibles, sin embargo al ser un laboratorio tenemos un pase libre.

En CyberChef agregamos las siguientes "recetas". Le indicamos que viene de Base64 y que realice la decodificación del texto. Además le indicamos que es UTF-16LE(1200) que es la codificación que usa Powershell
![](https://i.imgur.com/BACJ3D4.png)

Con eso obtenemos el resultado:
![](https://i.imgur.com/hlQ5bXY.png)
Osea... el comando no es más que una actualización forzosa de Windows...

---
Lo que sucedió según la narrativa es que:
- Las credenciales que se utilizaban para actualizar las máquinas de windows estaban obsoletas.
- Alguien realizó fuerza bruta para acceder y arreglar las credenciales.
- La evidencia está en que cada vez que se ejecutó el comando, previamente se autenticó correctamente.

Con esto finalmente podemos responder las preguntas:
- ¿Cuál es el nombre de la cuenta causando los logins fallidos?
	- Esto podemos obtenerlo con los filtros mencionados previamente
- ¿Cuantos intentos fallidos de logon?
	- Esto podemos obtenerlo también con los filtros, filtrando por fallidos.
- ¿Cuál es la dirección IP de Glitch?
	- Esto podemos obtenerlo cuando filtramos las IP y notamos la IP distinta.
- ¿Cuándo logró Glitch loguearse a ADM-01?
	- Nuevamente los filtros nos ayudan a esto, debemos buscar el primer intento evento success y agregando la máquina ADM-01 junto a la IP de Glitch.
- ¿Cuál es el comando decodificado?
	- Lo obtenemos a través de cyberchef, aplicando decodificación de base64 (UTF-16LE(1200))

Hemos resuelto el desafío del día 2.
![](https://i.imgur.com/rhNJCOw.png)


Continuamos con el [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 3\|Advent of Cyber día 3]]