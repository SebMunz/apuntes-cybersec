---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 10/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 9\|Advent of Cyber día 9]]

Objetivos:
- Entender el [[Ciberseguridad/Ataques/Phishing\|Phishing]]
- Como los macros se pueden usar y abusar
- Cómo ejecutar un ataque de phishing usando macros

Herramientas:
- Metasploit

---

# Phishing

A grandes rasgos es una técnica de "fishing" o "pescar", donde le enviamos la carnada a un usuario o grupo de usuarios con el propósito de robar información personal o instalar malwares, usualmente convenciendo de que lo que estamos haciendo es real.
[[Ciberseguridad/Ataques/Phishing\|Más información en este apartado]].

---
# Macros
Una macro en computación se refiere a un set de instrucciones programadas diseñadas para automatizar tareas repetitivas. La suite office de microsoft, soporta macros en documentos para agilizar tareas. Sin embargo, son fáciles de utilizar maliciosamente sin cuidado.

---

# Plan de ataque

Al abrir el documento enviado, la macro ejecutara un payload y se conectará a la máquina maliciosa, dándole control. En el [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 9\|día 9]] ejecutamos un reverse shell, esto nos podría servir en este caso.

1. Crear un archivo con una macro maliciosa
2. Comenzar la escucha, esperando conexiones
3. Enviar el email con el documento y esperar...
4. El objetivo abre el documenta y se ejecuta el macro
5. Ganamos control de la máquina
La razón por la que es más sencillo que la máquina se conecte a nosotros es por la de los funcionamientos de firewall y redes privadas :)

