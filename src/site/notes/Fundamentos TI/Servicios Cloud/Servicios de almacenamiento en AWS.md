---
{"dg-publish":true,"permalink":"/Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS/"}
---

Implementaremos a modo de ejercicio un sitio web AWS estático en un bucket S3, además de crear instancias EC2, volúmenes EBS y montaje del mismo a la instancia.

---

# Índice

1. [[Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS#Configuración inicial\|#Configuración inicial]]
2. [[Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS#Sitio web estático en S3\|#Sitio web estático en S3]]
3. [[Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS#Creación almacenamiento\|#Creación almacenamiento]]

---

# Configuración inicial

Para empezar debemos crear una cuenta en AWS. 
El proceso inicial es bastante directo, ingresar a <a href="https://aws.amazon.com/es/">AWS</a> -> botón de Sign-up
Desde ahí seguir instrucciones, en el paso 3 debemos ingresar información de una tarjeta de crédito (o débito), como Free trial tenemos acceso durante un año gratuito a 750 horas de EC2, 5GB de almacenamiento, 750 horas de RDS, 1 millón de requests Lambda, etc. además de un montón de otros beneficios. Hecho esto nos vamos a la consola.

---
<div class="page-break" style="page-break-before: always;"></div>

# Sitio web estático en S3

S3, o Amazon Simple Storage Service, es un servicio de almacenamiento cloud. Es escalable, seguro y tiene alta disponibilidad gracias a los servidores Amazon. Su uso es principalmente para realizar respaldos, webapps, análisis, etc.

Desde la consola podemos en la barra de búsqueda escribir S3 o bien en el widget de servicios, ir directamente a Storage -> S3
![](https://i.imgur.com/zSv3nTl.png)
<div class="page-break" style="page-break-before: always;"></div>

En s3 crearemos un bucket
![](https://i.imgur.com/CgPdXHH.png)
Aquí en la creación del bucket se nos levantan diversas opciones de configuración.
El tipo de bucket para este caso será **General**, agregamos un nombre al bucket, configuramos los ACL (en este caso no es necesario), cambiamos el acceso público (en este caso queremos que pueda ser accedido), versionamiento si lo requerimos, tags para organizar nuestros buckets, encriptación (SSE-S3 es suficiente en este caso). Finalmente creamos el bucket.
![](https://i.imgur.com/mGLOK2h.png)
Aquí se nos muestra los buckets creados.
<div class="page-break" style="page-break-before: always;"></div>

Le damos click al nombre y procedemos a subir nuestros archivos:
![](https://i.imgur.com/F7lmix4.png)

Más bajo tenemos los storage class donde podemos configurar qué tipo de acceso tendrán los archivos. Standard es el que necesitamos en nuestro caso pero importante notar que también existen otros como Intelligent-Tiering que es cuando desconocemos la frecuencia de acceso a los datos, Glacier que es para datos rara vez accedidos y los 'congelamos' y Standard-IA que es para datos que se acceden pocas veces (una vez al mes).

También tenemos para mayor seguridad ServerSide encryption para protección de los datos en descanso, checksums adicionales para integridad de los datos, tags y metadatos.

Le damos a upload, y volvemos a nuestro bucket lists. Debemos dirigirnos a properties.
![](https://i.imgur.com/I1JSZmS.png)
<div class="page-break" style="page-break-before: always;"></div>

De ahí debemos ir a Static Website Hosting, donde podremos configurar nuestro sitio web estático a través de amplify.app (lo que nos da más opciones, es más rápido y es más sencillo) o a través de static website hosting tradicional. Por el ejercicio lo haremos a través del canal tradicional así que presionamos en edit:
![](https://i.imgur.com/i5iAfdU.png)
![](https://i.imgur.com/KKuE64j.png)
En el sector que se abre colocamos cuál es el index según lo que tengamos en nuestro S3.
Lo subimos y luego nos vamos a permissions

![](https://i.imgur.com/yzKfpav.png)
y a bucket policies -> edit
<div class="page-break" style="page-break-before: always;"></div>

En el sector de políticas debemos editar el JSON para permitir que sea de acceso público el contenido en S3. Para ello vamos a add new statement, filtramos servicio a S3, agregamos la acción "GetObject", en recurso elegimos el servicio (S3), el tipo de recurso (object) y reemplazamos el nombre del bucket (desde donde queremos obtener los recursos) y el nombre del objeto ( en este caso los quremos todos así que colocamos "\*" )
![](https://i.imgur.com/ebMGVvt.png)

Guardamos los cambios y finalmente podremos acceder desde la URL que se nos provee desde el apartado de static website hosting (<a href="http://sebastian-munoz-z.s3-website.us-east-2.amazonaws.com/"> en mi caso es esta </a>)
![](https://i.imgur.com/uCy7DKV.png)
Con amplify, como decía antes, es mucho más rápido, nos basta de un par de clicks y nos entrega <a href="https://staging.d1gcsenmwstuoq.amplifyapp.com/">esta URL</a> y podemos configurar las rutas a través de Route S3.

---
<div class="page-break" style="page-break-before: always;"></div>

# Creación de almacenamiento

EC2, o Elastic Compute Cloud, es un servicio en la nube de AWS para alquilar máquinas virtuales (llamadas "instancias").
EBS, o Elastic Block Store, es un servicio de almacenamiento en bloque para almacenamiento persistente para las instancias EC2. A grandes rasgos es un disco duro virtual conectado al EC2. Con que sea "en bloque" se refiere a que el almacenamiento no es consumido en flujo, si no, en bloques de datos para proporcionar mayor disponibilidad e integridad.
## Instancia EC2
Para crear una instancia EC2 nos dirigimos a nuestra consola, servicio y seleccionamos EC2 (de la misma forma que seleccionamos S3).
Desde esta pantalla simplemente seleccionamos "Launch Instance"
![](https://i.imgur.com/GUxZ5cd.png)
<div class="page-break" style="page-break-before: always;"></div>

En la siguiente pantalla debemos configurar:
- Nombre: nombre-para-instancia
- AMI (Amazon Machine Image): podemos elegir desde amazon linux, macOS, ubuntu, windows, redhat, suse y debian. Para este caso basta con Amazon Linux.
- Tipo de instancia: t2.micro es suficiente y es la que nos entrega 750 horas gratis por nuestro primer año, de ahí tenemos 750 distintos tipos para distintas cargas de trabajo. Algunas tienen hasta 448 CPUs. 
- Par de llaves: debemos seleccionar pares de llaves para hacer login a través de SSH.

En network settings configuramos cosas como la red, la IP pública, firewall y los permisos de acceso SSH, HTTPS y HTTP.

Configuramos el almacenamiento y los detalles avanzados de ser necesarios (como autorecuperación, que hacer cuando apagamos la máquina, elastic GPU, metadatos, etc).

Con esto listo simplemente damos click a launch instance.
Volvemos a nuestras instancias y veremos
![](https://i.imgur.com/yAGjGuL.png)
En la parte de status check que aún se está inicializando, debemos esperar a que diga running.
<div class="page-break" style="page-break-before: always;"></div>

## EBS
En el mismo sector de instancias, en el menú de hamburguesa de la izquierda, está la opción de Elastic Block Store.
Nos dirigimos a Volúmenes y crear volumen.
![](https://i.imgur.com/9S7iNH6.png)
En este apartado tenemos diferentes opciones:
- Volume type: el tipo de disco según necesidad
- Size: el tamaño del mismo
- IOPS: cantidad de operaciones por segundo de input/output
- Throughput: rendimiento del disco en MiB/s
- Availability Zone: localización del disco, recomendable la misma que el EC2
- Snapshot ID: Identificador para la creación de Snapshots
- Encryption: encriptación adicional para el disco
- Tags

<div class="page-break" style="page-break-before: always;"></div>

## Asignación del EBS al EC2
Para asignarlo, ingresamos al volumen, acciones y attach volume
![](https://i.imgur.com/Xk0oXzZ.png)

Seleccionamos la instancia, el nombre de volumen que se le asignará en linux y attach.
![](https://i.imgur.com/vH40xHb.png)

Para montarlo, debemos realizarlo a través de la instancia, para ello nos podemos conectar usando EC2 Instance Connect (que es interno de AWS), pero generalmente lo hacemos desde SSH:
`ssh -i key.pem usuario_definido@IP_PUBLICA_INSTANCIA`
<div class="page-break" style="page-break-before: always;"></div>

![](https://i.imgur.com/eRpokMx.png)
Ahora debemos ejecutar los siguientes comandos:
- Creamos el file system
	- `sudo mkfs -t ext4 /dev/sdb`
- Creamos la carpeta donde montaremos el volumen
	- `sudo mkdir /mnt/ebs-volumen`
- Montamos el volumen en su carpeta
	- `sudo mount /dev/sdb /mnt/ebs-volumen`
- Verificamos
	- `df -h`
 ![](https://i.imgur.com/UOH516S.png)
