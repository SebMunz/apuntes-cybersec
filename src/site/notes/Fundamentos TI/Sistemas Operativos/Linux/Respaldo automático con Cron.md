---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Respaldo automático con Cron/"}
---

Esto es algo que se me ocurrió probar cuando estaba realizando el ejercicio de [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables\|IP tables]].
# Script automatización para guardar iptables y cronjob

Cron es bien divertido, sirve para muchas cosas de automatización en Linux y es **MUY FÁCIL DE CONFIGURAR**. Pueden ver otro ejemplo en este lugar [[Fundamentos TI/Sistemas Operativos/Linux/Administración de archivos, grupos, comandos.#4.- Backups y Cron\|donde hice varios ejercicios básicos de linux]]

Así que aquí va un pequeño script de bash que:
- Comprueba que exista el archivo `/etc/iptables/rules.v4`
- Si existe lo guarda
- Si no, lo crea y luego guarda

``` bash
#!/bin/bash

#variables con las rutas
DIR="/etc/iptables"
ARCHIVO="$DIR/rules.v4"

#Crear el directorio si no existe
if [! -d "$DIR"]; then
	echo "Directorio $DIR no existe. Creándolo..."
	sudo mkdir -p "$DIR"
	sudo chmod 755 "$DIR"
fi

#Comprobar si el archivo existe si no, lo crea
if [ ! -f "$ARCHIVO" ]; then
	echo "No existe $ARCHIVO - Creándolo..."
	sudo touch "$ARCHIVO"
	sudo chmod 644 "$ARCHIVO"
fi

#Guardar reglas
echo "Guardando reglas..."
sudo iptables-save | sudo tee "ARCHIVO" > /dev/null

# Tuvo éxito el comando anterior?
if [ $? -eq 0]; then
	echo "Guardado correctamente en $ARCHIVO."
	else echo "Error al guardar"
fi
```

Esto lo guardaremos por ahí en nuestro equipo, lo guardé en la carpeta de usuario por conveniencia.

Le cambiamos las reglas para que sea ejecutable:
`sudo chmod +x /home/usuario/guardar_reglas.sh`

Editamos el archivo cron del root
`sudo crontab -e`

y agregamos la linea:
`0 0 * * * /home/usuario/guardar_reglas.sh`
esto hará que se ejecute automáticamente todos los días a las 00:00

---
# Servicio que ejecuta un comando

Alternativamente podríamos crear un servicio que ejecute dicho comando al momento de apagar, suspender o reiniciar el equipo, agregando una capa de complejidad mayor.

`sudo nano /etc/systemmd/system/guardar_reglas.service`

Y agregamos lo siguiente:
```ini
[Unit]
Description=Guardar reglas iptable de forma automática
DefaultDependencies=no
Before=shutdown.target reboot.target halt.target

[Service]
Type=oneshot
ExecStart=/home/usuario/guardar_reglas.sh

[Install]
WantedBy=shutdown.target reboot.target halt.target multi-user.target
```

Muy sencillo veamos el desglose:
- `[Unit]`
	- `Description`
		- *descripción*
	- `DefaultDependencies=no`
		- *indica que no debe ejecutarse como parte de las dependencias predeterminadas de sistema. Si lo dejamos en yes, corre el riesgo de que si hay alguna falla en el script, el sistema se bloquee*
	- `Before=shutdown.target reboot.target halt.target`
		- *Especificamos que se debe ejecutar antes del apagado, reinicio o detención del sistema*
- `[Service]`
	- `Type=oneshot`
		- *el servicio se ejecuta una sola vez y no se reinicia automáticamente*
	- `ExecStart=...`
		- *especifica qué debe hacer el servicio, en este caso ejecutar el script*
- `[Install]`
	- `WantedBy=shutdown.target reboot.target halt.target multi-user.target`
		- *El servicio debe ser ejecutado cuando se alcancen los objetivos de apagado, reinicio, detención del sistema o cuando esté listo para ser usado en estado normal*

# Dudas 

Algunas dudas que me saltaron al principio y que debí aclararme fue:

> ¿No se ejecutará el script al iniciar el servicio?
La respuesta es **NO**. Gracias a que le dimos triggers (`before`), se ejecutará el script sólo cuando ocurra uno de ellos.

> En `WantedBy=` sólo estamos indicando que **el servicio** debe iniciarse, más no el script.

> ¿Es realmente seguro?
> Si y no. Cualquier cosa automatizada podría tener problemas si no nos aseguramos de que esté bien hecho.

>¿Por qué podría no ser seguro?
>Error humano. Uno tiende a desentenderse del script al estar automatizado. Supongamos que alguien logró romper el acceso y logró modificar el script. Felicidades, tienes un script que se ejecutará automáticamente sin darte cuenta. Pero obviamente esto podemos minimizarlo con un monitoreo constante y permisos adecuados.


Finalmente ahora se guardan automáticamente las iptables cuando se apaga, se reinicia o se suspende el equipo. Además se inicia automáticamente el servicio al iniciar el equipo.

Se puede reemplazar para cualquier ejecución u script que necesitemos
ヾ(≧▽≦*)o