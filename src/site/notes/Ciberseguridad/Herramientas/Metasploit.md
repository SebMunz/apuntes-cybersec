---
{"dg-publish":true,"permalink":"/Ciberseguridad/Herramientas/Metasploit/"}
---

Framework para testear seguridad de sistemas y aplicaciones, finalmente explotándolas. Útil para simular ataques realistas.

Metasploit tiene 3 pasos fundamentales para su funcionamiento
- Detectar vulnerabilidad
	- Defecto en el sistema, en alguna aplicación, en el usuario, etc.
- Exploit
	- Un programa o script diseñado específicamente para aprovechar la vulnerabilidad
- Payload
	- Lo que contiene el programa/script, el código interno




Explotación `Eternalblue` de Win7 a modo de ejemplo:
Iniciamos:
`msfconsole`
`search ms17` o `search eternalblue` para determinar el módulo que utilizaremos, en general podemos buscar también con el CVE
`use nombredelmodulo` o `use numeroíndice`

Ahora podemos utilizar por ejemplo:
`info` para dar información respecto al módulo como autores, objetivos, parámetros, etc
`show options` es un poco más acotado y sólo muestra las opciones

Lo que nos diga `required` hay que configurar dichas opciones, por ejemplo `RHOST` nos indica que debemos configurar el host.
`set RHOST direccionHost`

`exploit` o `run` para iniciar el exploit. Generalmente funciona a la primera, si no, es posible que se requiera correr 2 o tres veces, cambiar el puerto de escucha, configurar el payload, etc.