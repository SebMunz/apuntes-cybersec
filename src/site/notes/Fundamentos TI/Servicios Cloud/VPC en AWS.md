---
{"dg-publish":true,"permalink":"/Fundamentos TI/Servicios Cloud/VPC en AWS/"}
---

Para esta actividad vamos a crear una VPC (Amazon Virtual Private Cloud), generar una red personalizada, grupos de seguridad para la [[Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS#Instancia EC2\|instancia EC2]] y finalmente personalizar la instancia EC2 para ejecutar el servidor web y lanzarlo en VPC.
![](https://i.imgur.com/UfaftBM.png)
Recrearemos esta topología.

---

# Índice

1. [[Fundamentos TI/Servicios Cloud/VPC en AWS#VPC\|#VPC]]
2. [[Fundamentos TI/Servicios Cloud/VPC en AWS#Subredes\|#Subredes]]
3. [[Fundamentos TI/Servicios Cloud/VPC en AWS#Configuración Gateways y Tablas de Rutas\|#Configuración Gateways y Tablas de Rutas]]
4. [[Fundamentos TI/Servicios Cloud/VPC en AWS#Grupo de seguridad\|#Grupo de seguridad]]
5. [[Fundamentos TI/Servicios Cloud/VPC en AWS#EC2 y asociación\|#EC2 y asociación]]
6. [[Fundamentos TI/Servicios Cloud/VPC en AWS#Montaje sitio web estático en esta nueva instancia\|#Montaje sitio web estático en esta nueva instancia]]
7. [[Fundamentos TI/Servicios Cloud/VPC en AWS#Conclusión\|#Conclusión]]

---
<div class="page-break" style="page-break-before: always;"></div>


# VPC

Para la creación del VPC debemos dirigirnos a servicios -> Networking & Content Delivery -> VPC
![](https://i.imgur.com/PYAuNyd.png)

Luego presionamos en Create VPC
![](https://i.imgur.com/HzXLbBX.png)

Ahora se nos abre un dashboard con diversas opciones de configuración y un preview de la topología.
Técnicamente, desde aquí podemos crear la VPC con subnets, sin embargo lo haré separado, por lo tanto seleccionamos la opción "VPC ONLY"
<div class="page-break" style="page-break-before: always;"></div>

Configuramos:
- Nombre
- CIDR (básicamente el rango de direcciones IP asignados a la red)
- Si es que vamos a utilizar IPv6 (no en este caso)

Guardar y listo:
![](https://i.imgur.com/Chl4AdY.png)

Ahora, a la izquierda nos dirigimos a Subnets
<div class="page-break" style="page-break-before: always;"></div>

# Subredes
Lo más probable es que en este punto tengamos algunas subnets creadas por la [[Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS#Instancia EC2\|instancia EC2 creada con anterioridad]]. Sin embargo, sólo debemos crear nuevas.
Para ello, crearemos 4 subredes. 2 públicas y 2 privadas.

Botón Create subnet.
Seleccionamos la VPC correspondiente (mi-vpc).
Luego debemos configurar ciertas cosas:
- Nombre
- Zona de disponibilidad
- CIDR IPv4 (el mismo de la VPC)
- CIDR IPv4 subnet (la IP para la subred)

Creamos las 4, distribuidas como:
- públicaOprivada-numeroDeZona-letraDeZona
- IP partiendo de 10.0.0.0/24 hasta el 10.0.3.0/24
![](https://i.imgur.com/2TL1Kr9.png)
<div class="page-break" style="page-break-before: always;"></div>

# Configuración Gateways y Tablas de Rutas
Nos vamos nuevamente a la izquierda y seleccionamos "Internet Gateways" y "Create Internet Gateways" en el botón naranjo-amazon
![](https://i.imgur.com/vBWgAAE.png)

![](https://i.imgur.com/qPsZo5a.png)
Se nos mostrará la opción para agregarla a nuestra VPC. Si no lo hacemos así, siempre podemos ir al dashboard de VPC, seleccionar el gateway, acciones y "Attach To VPC"
![](https://i.imgur.com/5SfMD4j.png)

Ahora debemos crear las tablas de ruta.
<div class="page-break" style="page-break-before: always;"></div>

En el menú de la izquierda vamos a "Route Tables", justo encima de "Internet Gateways". Mismo proceso presionando el botón naranjo "Create Route Table".
Le indicamos a cual VPC lo adherimos y continuamos.
![](https://i.imgur.com/NAwIrpX.png)
Desde esta pantalla podemos configurar las rutas, la local ya viene configurada, sólo nos falta el gateway:
Le damos a edit routes -> add route
![](https://i.imgur.com/mQ7GmPa.png)
finalmente debemos asociarlo a nuestras subredes. Desde el dashboard de la tabla de rutas creada
![](https://i.imgur.com/bomDSJa.png)
Subnet associations y edit subnet associations.
Ingresamos ahí, seleccionamos las redes públicas y save.
![](https://i.imgur.com/UYkujee.png)
<div class="page-break" style="page-break-before: always;"></div>

Finalmente debemos crear un proceso similar para NAT gateway.
Nos dirigimos ahí desde el menú de la izquierda, create NAT y configuramos:
- Nombre
- Asociación a subred (pública, zona A)
- Tipo de conectividad (en este caso necesita acceso a internet, ergo, pública)
- Elastic IP, simplemente presionar el botón de allocate porque no tenemos ninguno configurado previamente
Le damos a create.
![](https://i.imgur.com/XbgMfjA.png)

Esperamos a que el estado cambie a disponible, y nos dirigimos a route tables nuevamente.
Aquí debemos crear una nueva tabla de enrutamiento específica para subredes privadas.
Editamos las rutas:
![](https://i.imgur.com/qPtyogL.png)
y agregamos las subredes privadas:
![](https://i.imgur.com/U3Tpnxu.png)
<div class="page-break" style="page-break-before: always;"></div>

# Grupo de seguridad
El proceso es bastante sencillo:
Nos dirigimos al menú de la izquierda y Security->Security Groups->Create security group
![](https://i.imgur.com/IKsxiIw.png)
y configuramos reglas de entrada, como por ejemplo:
SSH desde mi IP, HTTP desde cualquier IPv4 e ICMP desde cualquier IPv4.

![](https://i.imgur.com/6hAB6cv.png)
<div class="page-break" style="page-break-before: always;"></div>

# EC2 y asociación
Finalmente vamos a asociar una instancia EC2 al nuevo grupo de seguridad. Lo más fácil es crear una nueva instancia y al momento de hacerlo le decimos que use ese grupo de seguridad y VPC. El camino difícil es una migración para lo cual debemos crear una AMI de la instancia previamente creada, lanzar la nueva instancia en la VPC.

Lo que haremos será:
- Crear una nueva instancia
- Asignarla al VPC creado
- Asignarle el grupo de seguridad
- Montar el sitio estático que creamos en [[Fundamentos TI/Servicios Cloud/Servicios de almacenamiento en AWS#Sitio web estático en S3\|S3]]

Creamos la nueva instancia, similar a la anteriormente mencionada pero cambiando algunos parámetros:
![](https://i.imgur.com/BzYakI9.png)
- Seleccionamos la VPC creada
- Asignamos una subred pública
- Seleccionamos un grupo de seguridad previamente creado

Con eso ya tenemos configurado el grupo de seguridad y la VPC en la instancia EC2. Para poder conectarnos a ella debemos asignarle una IP pública, la cual podemos hacer con elastic IP.
<div class="page-break" style="page-break-before: always;"></div>

# Montaje sitio web estático en esta nueva instancia
Similar a como lo hicimos [[Fundamentos TI/Sistemas Operativos/Linux/Gestión de servicios y almacenamiento en Linux#Apache2\|en este documento]], vamos a instalar Apache2 mediante SSH, crear un rol IAM para acceder al bucket S3, descargar los archivos en la instancia, sync en la máquina.

Haremos los siguientes comandos luego de conectarnos por SSH:
```
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

Ahora en el dashboard de amazon iremos a crear una IAM. IAM es Identity and Access Management, básicamente sirve para crear reglas, credenciales, identificación, authenticación, etc.
Nos vamos al menú de la izquierda, en roles->create role.
![](https://i.imgur.com/GNklo4m.png)
<div class="page-break" style="page-break-before: always;"></div>

En la parte de los permisos 
![](https://i.imgur.com/phr0emA.png)
Ya con eso, nos vamos hacía la instancia EC2, la seleccionamos y nos dirigimos a Actions -> security -> modify IAM roles. Seleccionamos y Update
![](https://i.imgur.com/8WgfYEQ.png)
<div class="page-break" style="page-break-before: always;"></div>

Nos dirigimos, a la terminal, nos conectamos por SSH a la instancia y lanzamos el comando
`aws s3 ls s3://URL-BUCKET`
con esto comprobamos el acceso al bucket.
![](https://i.imgur.com/qDJ5C8F.png)

Con esto ya hecho, podemos acceder a través de la dirección que nos proporciona la instancia EC2
![](https://i.imgur.com/c55HP42.png)
Que por cierto en este caso es http por la configuración de apache2.

---
<div class="page-break" style="page-break-before: always;"></div>

# Conclusión

Configuramos una VPC, la desplegamos en una instancia EC2 y utilizamos dicha instancia para montar un servidor web con un sitio estático.
Todo esto nos permitió entender de mejor forma la importancia de las estructuras bien configuradas en entornos de nube.
Este diseño de subredes públicas y privadas, gateways y nat gateways optimiza la seguridad y garantiza que las instancias privadas puedan tener acceso controlado a internet para poder mantener actualizaciones.

Me enfrenté al problema del montaje de la VPC en una instancia EC2 previamente creada, descubriendo que la forma más ideal es crear la VPC *antes* de la instancia, si no, hay que hacer una migración de la instancia a través de una imagen de respaldo. Esto es un problema inherente de AWS que es mejor evitar.

Finalmente el montaje de un sitio estático en la instancia, creando así un servidor web, consolida la comprensión sobre la integración de servicios AWS y el funcionamiento del ecosistema.

Todo esto nos deja aún más clara la importancia de realizar una planificación meticulosa de la infraestructura que vamos a montar.