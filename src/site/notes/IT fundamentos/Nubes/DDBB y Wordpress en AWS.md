---
{"dg-publish":true,"permalink":"/IT fundamentos/Nubes/DDBB y Wordpress en AWS/"}
---

Para este ejercicio crearemos una una base de datos en AWS, a través de su servicio RDS (relational database service), configuraremos el acceso desde EC2 e instalaremos y configuraremos Wordpress en ella.

---
# Índice
1. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#RDS\|#RDS]]
2. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#EC2 + RDS\|#EC2 + RDS]]
	1. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#Creación EC2 para wordpress\|#Creación EC2 para wordpress]]
	2. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#Acceder RDS desde EC2\|#Acceder RDS desde EC2]]
3. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#Wordpress\|#Wordpress]]
4. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#Comprobación\|#Comprobación]]
5. [[IT fundamentos/Nubes/DDBB y Wordpress en AWS#Conclusión\|#Conclusión]]

---
<div class="page-break" style="page-break-before: always;"></div>

# RDS

RDS, o Relational Database Service, es el servicio de AWS para bases de datos relacionales.
Para crear una instancia, vamos a la consola de RDS en AWS y seleccionamos **Crear base de datos**
![](https://i.imgur.com/rxCol4D.png)


Elegimos el modo **Creación estándar** y seleccionamos el motor de base de datos y su versión. En mi caso lo haré con MySQL en su última versión.
![](https://i.imgur.com/VpmATSn.png)
<div class="page-break" style="page-break-before: always;"></div>

Debemos ahora configurar el nombre de la base de datos, el usuario maestro (root) y una contraseña:
![](https://i.imgur.com/itainWD.png)
<div class="page-break" style="page-break-before: always;"></div>

Ahora, en la sección de configuración de red, seleccionamos la VPC que [[IT fundamentos/Nubes/VPC en AWS#VPC\|creamos en este ejercicio]] y negamos el acceso público.
![](https://i.imgur.com/rk6Uagx.png)
De aquí pudimos conectarnos directo al EC2, pero lo haremos separado por fines educativos.
<div class="page-break" style="page-break-before: always;"></div>

Configuramos el grupo de seguridad para que permita el puerto 3306 (o el puerto que utilice el motor de base de datos) desde EC2
![](https://i.imgur.com/hd04glN.png)

![](https://i.imgur.com/Ndyz8Lo.png)

Otras configuraciones a notar:
Templates podemos rápidamente seleccionar el free tier para pruebas pero si elegimos el de producción podemos cambiar:
- cantidad de instancias para disponibilidad
- credentials management, el secrets manager de AWS mantiene nuestras credenciales pero podemos seleccionar self managed para nosotros preocuparnos de eso.
- el tipo de instancia (procesador, memoria, etc)
- en almacenamiento podemos elegir almacenamiento escalable
- autenticación
- En configuraciones adicionales podemos dar el nombre de la base de datos inicial
 <div class="page-break" style="page-break-before: always;"></div>

# EC2 + RDS

## Creación EC2 para wordpress

Ahora vamos a configurar una nueva instancia para utilizar wordpress.
Configuramos el nombre de la instancia, el AMI (amazon linux), el tipo de instancia, la asignamos a la VPC con la subred pública, el grupo de seguridad que permita acceso SSH, HTTP y lanzamos la instancia.
![](https://i.imgur.com/gtiqwUg.png)
<div class="page-break" style="page-break-before: always;"></div>

## Acceder RDS desde EC2
Nos conectamos a la instancia a través de SSH.
Instalamos MySQL en la instancia:
- `sudo yum update -y`
- `sudo wget https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm`
- `sudo dnf install mysql80-community-release-el9-1.noarch.rpm -y`
- `sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023`
- `sudo dnf install mysql-community-server -y`
Donde:
1. Actualizamos
2. Descargamos el archivo rpm
3. Lo instalamos
4. Importamos su llave pública
5. Instalamos el servidor
![](https://i.imgur.com/7P22Vf5.png)
<div class="page-break" style="page-break-before: always;"></div>

Debemos ahora ligar el RDS a nuestro EC2, asegurarnos que estén en la misma zona de disponibilidad para no incurrir en gastos fantasmas innecesarios.
![](https://i.imgur.com/bq5PgEj.png)

Probamos la conexión RDS:
- `mysql -h <endpoint RDS> -u admin(o usuario root configurado) -p`

Además nos pedirá la contraseña.  La dirección endpoint_rds la encontramos en la consola RDS
![](https://i.imgur.com/e0QRkEw.png)
<div class="page-break" style="page-break-before: always;"></div>

Dentro del cliente MySQL crearemos un usuario y una base de datos para WordPress:
``` MySQL
CREATE USER 'admin_wordpress'@'%' IDENTIFIED BY 'contraseña'; GRANT ALL PRIVILEGES ON nombre_DDBB.* TO 'admin_wordpress'@'%'; FLUSH PRIVILEGES;
```
Con este comando creamos el usuario y puede acceder desde cualquier ip ('%'), le asignamos la contraseña; le damos todos los privilegios de la base de datos (y sus tablas con el wildcard) al usuario y permitimos cualquier dirección IP; Hacemos un "flush" que a grandes rasgos es realizar todos estos cambios de privilegios ahora mismo.

Ojo que este comando sólo es necesario si necesitamos crear un usuario adicional con los permisos. En mi caso lo cree al momento de hacer la RDS.
<div class="page-break" style="page-break-before: always;"></div>

# Wordpress

Ahora, debemos instalar las dependencias de WordPress en la instancia:
- `sudo yum install -y httpd php php-mysqlnd wget`
- `sudo systemctl start httpd`
- `sudo systemctl enable httpd`

Con estos comandos instalamos los servicios necesarios para el servidor web y las configuraciones pertinentes para integrar mysql con el mismo.
![](https://i.imgur.com/fU9HgRx.png)
<div class="page-break" style="page-break-before: always;"></div>

Ahora debemos descargar y configurar Wordpress:
- `wget https://wordpress.org/latest.tar.gz`
- `tar -xvzf latest.tar.gz`
- `sudo mv wordpress/* /var/www/html/`
- `sudo chown -R apache:apache /var/www/html`
- `sudo chmod -R 755 /var/www/html`
Con estos comandos:
- Descargamos la última instancia de wordpress en formato tar
- lo descomprimimos
- Lo movemos desde `wordpress/*` hacia `/var/www/html/` que es donde se monta para el servidor
- Cambiamos el dueño de manera recursiva (`-R`), el nuevo dueño y su grupo y el directorio al cual se va a cambiar
- Modificamos los permisos (7 5 5 donde 7 es todos, 5 es lectura y ejecución) al mismo directorio.
![](https://i.imgur.com/EKDlN0u.png)
<div class="page-break" style="page-break-before: always;"></div>

Lo siguiente es configurar la base de datos en wordpress:
Para ello debemos primero editar el archivo `wp-config.php`
- `sudo nano /var/www/html/wp-config.php`
- Actualizamos las siguientes líneas 
```
define('DB_NAME', 'nombre_DDBB');
define('DB_USER', 'admin_wordpress');
define('DB_PASSWORD', 'contraseña');
define('DB_HOST', '<endpoint_RDS>');
```
- Finalmente reiniciamos apache con el comando `sudo systemctl restart httpd`
<div class="page-break" style="page-break-before: always;"></div>

# Comprobación

Para la comprobación accedemos a la instancia EC2 desde el navegador utilizando su dirección.
![](https://i.imgur.com/IAyDi88.png)
Nos encontramos con este error. Investigándolo, nos encontramos con que no tenemos acceso a http, así que nos dirigimos al grupo de seguridad y agregamos una regla para aceptar conexiones HTTP.
![](https://i.imgur.com/dHE3ITS.png)
Arreglado eso logré conectarme, sin embargo los contenidos de wp-config.php están expuestos lo que es una brecha de seguridad enorme. Esto es debido a un error.
Investigando a profundidad noté que wordpress no estaba correctamente instalado en el servidor, y no estaba parseando correctamente el php debido a que faltaban unos módulos de php, que no se instalaron directamente con la instalación inicial.

Con esto último solucionado, veremos la nueva página de wordpress:
![](https://i.imgur.com/fYboRPT.png)
<div class="page-break" style="page-break-before: always;"></div>



Completamos la configuración inicial de wordpress
![](https://i.imgur.com/Ag0fpRG.png)
![](https://i.imgur.com/XTzYBDB.png)
<div class="page-break" style="page-break-before: always;"></div>

Creamos una publicación y revisamos que los datos se almacenan en la base de datos RDS:
![](https://i.imgur.com/8BqJCe2.png)
![](https://i.imgur.com/pmakGhs.png)
<div class="page-break" style="page-break-before: always;"></div>

# Conclusión

Ha sido un desafío largo y complejo. Tuve que aprender varias cosas nuevas (php, wordpress, rds) pero ha sido satisfactorio.
La mayor dificultad fue sin duda el poder conectarme a wordpress por la falla en el parseo de php.

Lo que puedo rescatar de esta experiencia:
- Elegir la distro adecuada con antelación:
	- Gran parte de los problemas fueron por la elección de Amazon Linux 2023 que tiene problemas con algunos paquetes de php, mysql y wordpress.
	- Hacerlo con ubuntu hubiera sido más sencillo, definitivamente
- El peligro de exponer archivos como wp-config.php a la red, que contiene las credenciales de configuración de la base de datos.
- Explorar el uso de otros servidores como Nginx por sobre Apache2.
	- Apache2 tiene su uso, pero en proyectos donde no se necesita mayores configuraciones, como es el caso de wordpress, Nginx hubiera sido una mejor opción
- La importancia de leer los logs para identificar problemas de configuración.
