---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 3/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 2\|Advent of Cyber día 2]]

Objetivos:
- Seguir revisando logs
- Utilización de ELK
- Aprender sobre Remote Code Execution y como este funciona a través de subir archivos de forma insegura

Herramientas:
- ELK
- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Red Team vs Blue Team\|Blue Team]]

---
# Comienzo
ELK, o ElasticSearch, LogStash y Kibana, es un stack de agregación de logs que combina análisis de datos y herramientas de procesamiento para analizar logs. Su utilidad radica en poder leer logs desde múltiples fuentes en un lugar centralizado.

*Kibana es un lenguaje estructurado sencillo para buscar valores en documentos. Similar al SPL de Splunk. Alternativamente podemos usar Lucene que utiliza terminos difusos como wildcards y lógica*

Vamos a analizar un ataque a un sistema de hotel y luego recrear el ataque.

Iniciaremos el trabajo como blue team.

---
# Blue team

Escenario: Los sistemas alertaron al equipo SOC a un shell siendo subido a la plataforma de reservas WareVille Rails el primero de octubre del 2024. Debemos analizar como es que el atacante logró esto.

Iniciamos la attackbox y la VM.
En nuestra attackbox, nos dirigimos a la URL que nos propociona el desafío y nos vamos a Discover como en el [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 2\|día 2]].
Desde ahí nos dirigimos hacia la colección "wareville-rails"
![](https://i.imgur.com/iF1AYJp.png)
Cambiamos la fecha para seleccionar los logs de Octubre 1 00:00 hasta Octubre 2 00:00.
Aplicamos filtros para acotar nuestra búsqueda:
IPs de cliente no relevante, quitar respuestas 404
![](https://i.imgur.com/LFuvsVZ.png)


De esta forma podemos trabajar con actividad que podría ser sospechosa.
Durante la revisión de cada log nos encontramos con que se hizo una petición y acceso de un archivo "shell.php".


Aquí podemos acotar la búsqueda buscando todos los logs que contengan **shell.php**. Con la barra de búsqueda superior, escribimos `message: "shell.php"`.
![](https://i.imgur.com/cpfbshp.png)

---

# Red Team
Aparentemente hay una vulnerabilidad donde alguien subió un archivo creando un web-shell para realizar RCE (Remote code execution).
Ahora haremos un ataque [[Ciberseguridad/Ataques/Web-Shell y RCE\|Web-Shell y RCE]] en la página de frostypines.

Lo primero será evaluar los logs de frostypines, con fecha Octubre 3.
Nos vamos directamente con el query `message: "shell.php"` 
![](https://i.imgur.com/s8qm3zF.png)

---

# Preguntas

Blue:
- Dónde se subió el web shell?
	- Revisar desde dónde se obtiene el GET
- Cuál es la dirección IP que accedió al shell?
	- Acotar logs que entreguen la información junto a shell
Red:
- Cuál es el contenido del archivo flag.txt?
	- Debemos conectarnos a la página http://frostypines.thm/ del desafío, irnos a reservas
	- Con las credenciales otorgadas (`admin@frostypines.thm` y `admin`) accedemos
	- Vamos a agregar una nueva habitación
	- Cargamos un script webshell y lo guardamos
	- Vamos hacia la url de la nueva "habitación" creada y tenemos para ejecutar comandos
	- De ahí sólo toca buscar flag.txt :)

Con esto hemos resuelto el día 3
![](https://i.imgur.com/u8u9qkq.png)


Procedemos [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 4\|al día 4]]
