---
{"dg-publish":true,"permalink":"/Fundamentos TI/Redes y Comunicaciones/Infraestructura y configuración/Servidor Email/"}
---

La configuración de un servidor Email es una tarea compleja.
Los requisitos son extensos y el entendimiento de su funcionamiento debe ser preciso para evitar problemas.

![](https://i.imgur.com/Vh4VNar.png)


Los puntos que debemos tener a consideración:
- Mail Transfer Agent
	- Responsable de manejar el tráfico SMTP
	- Envía el correo de tu usuario a otro MTA y viceversa
- Mail Delivery Agent
	- LDA. 
	- Recibe el correo del MTA y lo mueve la bandeja de usuario correspondiente.
	- Distintos MDA tienen distintos formatos lo que cambia el cómo se almacenan los correos
- IMAP y/o POP3 server
	- Protocolos usados por los clientes, es la forma en que se reciben los correos
	- IMAP es complejo, permite multiples usuarios accediendo a la bandeja.
		- Se copian los mensajes del servidor al cliente, se mantienen en el servidor
	- POP3 es más sencillo
		- Se mueven los mensajes del servidor al cliente, no se mantienen en el servidor, sólo de forma local
- Filtro antispam
- AV
- Webmail
	- Acceso desde la web
- Nombre de dominio
- DNS records
- Certificados SSL

Correr un servidor propio tiene sus ventajas: la escalabilidad propia y el costo es inferior.
Sin embargo a veces puede resultar más sencillo saltarse todo esto y utilizar un servidor externo como Zoho, Office365, Google.

Una tercera opción es la de utilizar un servicio de reenvio de correos, como mailgun, donde creamos un correo con un dominio propio. Los correos recibidos en esa dirección, se redireccionan automáticamente a nuestro correo real, es a grandes rasgos una máscara (pero más complejo).

# Protocolos

## IMAP
Internet Message Access Protocol es el protocolo usado por la mayoría de las cuentas. Es donde utilizamos servidores remotos.
Utiliza dos puertos:
- 143
	- Por defecto, permite escuchar los request entrantes y sincronizar emails. No encriptado
- 993
	- IMAPS, IMAP sobre SSL (encriptado)

## POP3
Post Office Protocol 3. Se descargan los mensajes de un servidor al cliente. Tiene la ventaja de ser rápido, no cargar el servidor con requests constantes y poder mantener acceso a los correos aún sin acceso a internet. Sin embargo elimina por defecto los correos del servidor al descargarlos al cliente, dificultando la sincronización.
Utiliza uno de los dos puertos:
- 110
	- Por defecto, no encriptado
- 995
	- encriptado

## SMTP
Es el encargado completamente de enviar y recibir los correos. No requiere autenticación. Si bien esto puede ser ventajoso, es lo que permite el spam.
También maneja las notificaciones de recepción de email. 
Utiliza dos puertos:
- 25
	- Por defecto, no encriptado
	- Algunas veces está filtrado (justamente por el spam)
- 465 / 587
	- SMTPS (SMTP sobre SSL), por defecto, encriptado

## SMTP relay
Importante mencionar que si vamos a mandar emails en masa o por grandes cantidades, el uso de un relay es importantísimo para que los correos no sean marcados como spam, liberar carga del servidor y mantener separadas nuestras transacciones, acciones, etc.
Su configuración puede ser compleja pero existen alternativas de terceros.

## HTTP
Si bien no es un protocolo de correos como tal, sí es el protocolo por el cual lo más probable es que se acceda al email.
Es la parte de webmail mencionada más arriba.

---
