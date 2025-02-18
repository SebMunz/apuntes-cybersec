---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 4/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 3\|Advent of Cyber día 3]]

Objetivos:
- Utilización del [[wip folder/MITRE ATT&CK\|MITRE ATT&CK]]
- Utilización de Atomic Red Team
- Creación de reglas de alerta y detección, según los resultados de las pruebas

Herramientas y conocimientos usados:
- <a href="https://www.atomicredteam.io/">Atomic Red Team</a>
- [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Red Team vs Blue Team\|Red Team vs Blue Team]]
- [[wip folder/Cyber Kill Chain\|Cyber Kill Chain]]
- [[wip folder/MITRE ATT&CK\|MITRE ATT&CK]]
- Powershell
- Sysmon

---
# Comienzo

Algo importante que debemos tener en consideración antes de comenzar:
Nada es perfecto, incluyendo la detección. Por lo tanto debemos siempre apuntar a hacer más pequeñas estas brechas de seguridad.
Las brechas son muchas veces por las siguientes razones:
- Cada vez que encontramos brechas, el equipo rojo u atacantes seguirán buscando más.
- La línea entre normal y anómalo es muy delgada, lo que hace difícil crear reglas precisas que además permitan anomalías esperadas

# Cyber Kill Chain

La cyber kill chain es un modelo desarrollado por Lockheed Martin que muestra las distintas etapas típicas de un ataque cibernético, está basado en conceptos militares pero se ha adaptado a la ciberseguridad.
![](https://i.imgur.com/P7UAInx.png)

Tabla con las etapas, descripción, ejemplos y acciones que puede tomar la defensa para mitigar.

| Stage                 | Description                  | Common Examples                                                                               | Defender Actions                                                                          |
| --------------------- | ---------------------------- | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Reconnaissance        | Gathering target information | - Network scanning<br>- Social media research<br>- Email harvesting<br>- OSINT gathering      | - Limit public information<br>- Hide network details<br>- Monitor for scanning activities |
| Weaponization         | Creating attack tools        | - Malware development<br>- Exploit modification<br>- Payload packaging                        | - Keep systems patched<br>- Monitor threat intelligence<br>- Study common attack tools    |
| Delivery              | Getting weapons to target    | - Phishing emails<br>- Malicious websites<br>- USB drops<br>- Drive-by downloads              | - Email filtering<br>- Web filtering<br>- USB disable policies<br>- User training         |
| Exploitation          | Breaking into the system     | - Software vulnerabilities<br>- Zero-day exploits<br>- Social engineering                     | - Regular patching<br>- Security updates<br>- Endpoint protection<br>- Access controls    |
| Installation          | Establishing persistence     | - Malware installation<br>- Backdoor creation<br>- Registry modifications                     | - Application whitelisting<br>- Behavior monitoring<br>- File integrity monitoring        |
| Command & Control     | Setting up remote control    | - Hidden communication channels<br>- Covert protocols<br>- Remote access tools                | - Network monitoring<br>- Traffic analysis<br>- Firewall rules<br>- IDS/IPS systems       |
| Actions on Objectives | Achieving attack goals       | - Data theft<br>- Ransomware deployment<br>- System destruction<br>- Further lateral movement | - Data encryption<br>- Backup systems<br>- Access logging<br>- Incident response plans    |

---

# MITRE ATT&CK

MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge), es un framework utilizado para entender las distintas técnicas y tácticas que los actores de amenaza realizan.
Es una recolección de tácticas, técnicas y procedimientos que han sido implementadas en la realidad, de este modo podemos entenderlas mejor.
Si bien es sólo una explicación teórica, es importante de comprender.

---

# Atomic Red

Atomic Red Team es una biblioteca de casos de prueba que están mapeados al ATT&CK. Son casos sencillos que pueden ser ejecutados para detectar brechas de seguridad y cerrarlas. Además soporta automatización para ejecutar pruebas periódicas de forma automática.

| Parametro           | Explicación                                                                                                          | Ejemplo                                                                               |
| ------------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `-Atomic Technique` | Define la técnica a emular. Podemos usar el nombre completo o el valor "TXXXX". Se puede omitir                      | `Invoke-AtomicTest -AtomicTechnique T1566.001`                                        |
| `-ShowDetails`      | Muestra los detalles de cada prueba incluída                                                                         | `Invoke-AtomicTest T1566.001 -ShowDetails`                                            |
| `-ShowDetailsBrief` | Muestra el título de cada prueba incluída                                                                            | `Invoke-AtomicTest T1566.001 -ShowDetailsBrief`                                       |
| `-CheckPrereqs`     | Revisa si todo los componentes necesarios están presentes para la prueba                                             | `Invoke-AtomicTest T1566.001 -CheckPrereqs`                                           |
| `-TestNames`        | Setea las pruebas que quieres ejecutar, usando el nombre completo                                                    | `Invoke-AtomicTest T1566.001 -TestNames "Download Macro-Enabled Phishing Attachment"` |
| `-TestGuids`        | Setea las pruebas que quieres ejecutar usando el identificador                                                       | `Invoke-AtomicTest T1566.001 -TestGuids 114ccff9-ae6d-4547-9ead-4cd69f687306`         |
| `-TestNumbers`      | Setea las pruebas que quieres ejecutar usando el número de prueba. Limitado a la técnica atómica                     | `Invoke-AtomicTest T1566.001 -TestNumbers 2,3   `                                     |
| `-Cleanup`          | Ejecuta los comandos de limpieza que fueron configurados previamente para revertir el estado de la máquina a normal. | `Invoke-AtomicTest T1566.001 -TestNumbers 2 -Cleanup`                                 |
Vamos a ejecutar T1566.001 con Atomic.

---

# T1566.001
Si buscamos `T1566.001` en <a href="https://attack.mitre.org/">el sitio de MITRE</a>, nos encontramos con lo siguiente:
![](https://i.imgur.com/pZ1Vclr.png)

Básicamente podemos entender que es un tipo de [[Ciberseguridad/Ataques/Phishing#Distintos Tipos de Ataques\|Spearphishing]] con un adjunto.
Esto también podemos verlo ejecutando el comando `Invoke-AtomicTest T1566.001 -ShowDetails`

![](https://i.imgur.com/efvsNEB.png)


La información que nos entrega este comando es:
- Técnica: El nombre del MITRE ATT&CK que será testeado
- Atomic Test Name: Nombre descriptivo de la prueba a ejecutar
- Atomic Test Number: Número asignado a la prueba
- Atomic Test GUID: Número ID único de la prueba
- Descripción: Detallada
- Attack Commands: Comandos que se ejecutaran durante la prueba, incluyendo quién los ejecuta y los privilegios requeridos, nos permite buscar los artefactos en el Windows Event Viewer
- Cleanup Commands: Comandos que se ejecutaran para revertir la máquina a su estado inicial
- Dependencias: Los recursos requeridos que deben estar presentes para ejecutar las pruebas

Primero debemos revisar si están los recursos necesarios: `Invoke-AtomicTest T1566.001 -TestNumbers 1 -CheckPrereq`

![](https://i.imgur.com/579Dld3.png)

Ahora ejecutamos el comando:
`Invoke-AtomicTest T1566.001 -TestNumber 1`

![](https://i.imgur.com/8GXUS95.png)
Se ha ejecutado con éxito.
Ahora deberíamos revisar a través del System Monitor (de Windows) lo que ha ocurrido.
Primero correremos el cleanup de Atomic `Invoke-AtomicTest T1566.001 -TestNumbers 1 -cleanup`
![](https://i.imgur.com/7N6zLae.png)
Y nos iremos al Sysmon:
![](https://i.imgur.com/XHuaGZf.png)
![](https://i.imgur.com/yOh5Nwr.png)

1. Event Viewer
2. Apllications and Services
3. Microsoft
4. Windows
5. Sysmon
6. Operational

Podemos ver ahí en el tercer evento la siguiente información:
![](https://i.imgur.com/nYz5IrE.png)
- ID de proceso
- la línea de comando lanzada donde tenemos:
	- `"powershell.exe" & {$url = 'http://localhost/PhishingAttachment.xlsm' Invoke-WebRequest -Uri $url -OutFile $env:TEMP\PhishingAttachment.xlsm}`
	- Esto nos entrega lo que se ejecuta, la URL desde donde saldría el adjunto, la invocación de webrequest, la url y a dónde llega cuando se descarga

Con esta información podemos crear reglas de alerta.

# Alertas
Hay distintos formatos de alerta incluyendo Yara, Sigma, Snort, etc.
Gracias a la información obtenida, podemos crear reglas en sigma.
Tenemos por ejemplo detalles importantes como `WebRequest`, la url y el nombre del archivo descargado.
```sigma
title: Detect PowerShell Invoke-WebRequest and File Creation of PhishingAttachment.xlsm
	id: 1
	description: Detects the usage of Invoke-WebRequest to download PhishingAttachment.xlsm and the creation of the file
PhishingAttachment.xlsm.
	status: experimental
	author: TryHackMe
	logsource:
		category: process_creation
		product: windows
		service: sysmon
	detection:
		selection_invoke_webrequest:
			EventID: 1
			CommandLine|contains:
				- 'Invoke-WebRequest'
				-'http://localhost/PhishingAttachment.xlsm' 
				
			selection_file_creation:
			EventID: 11 # Sysmon Event ID for File Creation
			TargetFilename|endswith: '\PhishingAttachment.xlsm'
			
			condition: selection_invoke_webrequest or selection_file_creation
			falsepositives:
			- Legitimate administration activity may use Invoke-WebRequest, and legitimate Excel files may be created with similar names.
			level: high
			tags:
			- attack.t1071.001 # Web Service - Application Layer Protocol
			- attack.t1059.001 # PowerShell
			- attack.t1105 # Ingress Tool Transfer 
			- attack.t1566.001 # Spearphishing Attachment
```

En la parte de `detection` es donde ocurre la detección. Esta regla podemos importarla a nuestro [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR\|sistema de detección]].

Correremos un segundo ataque *donde se realice un ransomware a través del shell*

---

# Preguntas

- ¿Cuál es la bandera que se encuentra en el archivo .txt, que está en el mismo directorio del artefacto `PhishingAttachment.xslm`?
	- Debemos navegar al lugar de origen que obtenemos al revisar los detalles en el Sysmon
- ¿Qué ID de ATT&CK sería nuestro punto de interés?
	- Buscar en el sitio de MITRE
- ¿Cuál es la sub ID que se enfoca en Windows Command Shell?
	- En el ID anterior que buscamos en MITRE, podemos revisar en la parte de la izquierda donde está. Tenemos el formato TXXXX.subID
- ¿Cuál es el nombre de la técnica Atómica a probar?
	- Podemos obtenerla con la bandera `-ShowDetails` de Atomic
- ¿Cuál es el nombre del archivo usado en la prueba?
	- En el mismo `-ShowDetails` está la respuesta del archivo
- ¿Cuál es la bandera que encontramos si realizamos la prueba?
	- Realizar la prueba y buscar el archivo :)

Con esto hemos completado el día 4
![](https://i.imgur.com/4gP1vXS.png)

Por cierto... la bandera la podemos ingresar en Cyberchef y nos entrega un mensajito acerca de nuestro personaje glitch.

Procedemos al [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 5\|Advent of Cyber día 5]]

