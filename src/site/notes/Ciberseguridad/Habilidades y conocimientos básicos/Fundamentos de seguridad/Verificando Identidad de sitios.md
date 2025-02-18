---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Fundamentos de seguridad/Verificando Identidad de sitios/"}
---

Un pequeño y sencillo ejercicio donde verificaremos la identidad de 10 sitios webs a través de sus certificados.

# Google

Empecemos con uno sencillo para explicar el proceso: <a href="www.google.com">Google</a>
La forma más rápida, en navegadores basados en chromium es la de ir al sitio, hacer click aquí:
![](https://i.imgur.com/jr3J3W0.png)

Presionamos `Connection is secure`
![](https://i.imgur.com/5wPN70a.png)
Luego vamos a `Certificate is valid`
![](https://i.imgur.com/gjA74K6.png)
Y nos dará la siguiente ventanita:
![](https://i.imgur.com/2a70GCM.png)
Donde podemos ver:
- A quién se le entregó
	- Su nombre común (CN)
	- Organización
	- Unidad organizacional
- Quién lo entregó
	- CN (en este caso WR2)
	- O (en este caso es el mismo servicio de google trust)
	- OU
- El periodo de validez
	- Desde cuando
	- Hasta cuando
- La huella de identidad SHA-256
	- La huella del certificado
	- Su llave pública

Alternativamente podemos ir a las herramientas de desarrollador y
1. Presionar la pestaña de Security
2. Presionar View certificate
nos mostrará la misma ventana.
![](https://i.imgur.com/nkTYFW8.png)

---
<div class="page-break" style="page-break-before: always;"></div>

# Desafío Latam

![](https://i.imgur.com/sNQL6Za.png)
- La identidad corresponde efectivamente a <a href="www.desafiolatam.com">desafio Latam</a>
- Fue emitido por una entidad confiable (Google Trust Services)
- Sabemos el dominio y dueño
- Además incluye las huellas, la emisión y cuando expira.

---
<div class="page-break" style="page-break-before: always;"></div>

# Mi sitio web

<a href="https://apuntes-seb.vercel.app/">Mi sitio de apuntes personales</a>
![](https://i.imgur.com/nz9MhuI.png)
Aquí tenemos una nueva entidad:
`Let's Encrypt`
https://letsencrypt.org/es/

Entrega certificados cifrados gratuitos gracias a donaciones de grandes organizaciones como chrome, aws, mozilla, cisco, ibm, ford foundation, shopify, github, zendesk, etc.

---
<div class="page-break" style="page-break-before: always;"></div>

# Epublibre

<a href="https://epublibre.org">Sitio para respaldos de libros</a>
![](https://i.imgur.com/2TVsSmq.png)
Nuevamente Let's Encrypt :) pero esta vez es R11
No es más que una numeración en serie para los certificados emitidos por ellos. <a href="https://letsencrypt.org/2024/03/19/new-intermediate-certificates/">más información aquí</a>

---
<div class="page-break" style="page-break-before: always;"></div>

# RPGFan

<a href="www.rpgfan.com"> Página para fans de los juegos RPG </a>
![](https://i.imgur.com/3HXTfv7.png)

---
<div class="page-break" style="page-break-before: always;"></div>

# Saint11.art
<a href="https://saint11.art">Página de un dibujante de pixel art con muchos tutoriales</a>
![](https://i.imgur.com/msMN7SI.png)

---
<div class="page-break" style="page-break-before: always;"></div>

# TVTropes

<a href="https://tvtropes.org">Página para leer sobre "tropos" (elementos narrativos que se repiten en todas las obras) de series</a>
![](https://i.imgur.com/sH0EDPh.png)

En esta tenemos un certificado Amazon que utiliza RSA 2048 M02

---
<div class="page-break" style="page-break-before: always;"></div>

# Github.io
Plataforma donde se desplegan las aplicaciones web subidas en github

![](https://i.imgur.com/4pfJPOO.png)
Aquí tenemos otra entidad: <a href="https://www.digicert.com/es">Digicert Inc</a>
Es otra plataforma de certificados seguros con precios que van desde los 22 euros el más básico a los 95 euros el avanzado.

Su CN también nos indica el tipo de certificado, que es TLS con encriptación RSA SHA256 2020 CA1.

---
<div class="page-break" style="page-break-before: always;"></div>

# SII.cl

La página del servicio de impuestos internos.
![](https://i.imgur.com/iFL9j6L.png)
Aquí tenemos otra entidad de confianza: <a href="https://www.globalsign.com/es">GlobalSign</a>

---
<div class="page-break" style="page-break-before: always;"></div>

# Certificado expirado
<a href="https://expired-rsa-dv.ssl.com/">Un sitio con un certificado expirado de prueba</a>
![](https://i.imgur.com/KfufIJy.png)

Así podemos ver un certificado expirado: Venció el 2016

Otro ejemplo importante, del que no he podido encontrar, es cuando un certificado se emitió a un dominio, pero estamos en otro, lo que sería una suplantación de SSL o "Spoofing".

---
<div class="page-break" style="page-break-before: always;"></div>

# Síntesis

Los certificados son importantes para verificar la identidad y validez del sitio que visitamos.
Si bien un certificado expirado no es necesariamente una señal de que algo malo pasa, si es algo a tener consideración. Quizás simplemente venció reciente y están en proceso de revalidarlo.
Lo que sí, hay que tener ojo con el dominio/subdominio al que fue emitido para así evitar ataques de suplantación de identidad.

Uno que recuerdo de hace algunos años fue una página de phishing del banco que tenía el certificado "casi" exactamente igual.

