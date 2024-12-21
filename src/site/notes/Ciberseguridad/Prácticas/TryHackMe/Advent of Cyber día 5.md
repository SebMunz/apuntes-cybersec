---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 5/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 4\|Advent of Cyber día 4]]

Objetivos de aprendizaje:
- Entender conceptos de XML
- Explorar **XML EXTERNAL ENTITY** (XXE) y sus componentes
- Aprender a explotar estas vulnerabilidades
- Entender  formas de remediarlo

Herramientas y conocimientos:
- XML
- BurpSuite

---

# Comienzo

[[IT fundamentos/XML\|XML]] es un método común de transportar y almacenar datos de forma estructurada. Utiliza tags para etiquetar y organizar la información.
Cuando los equipos se comunican, utilizan XML para intercambiar la información de forma ordenada, para esta comunicación utilizamos DTD (Data Type Definition) que son reglas para estructurar el archivo XML. Además de ello, utiliza entidades para referirse a contenidos usados con frecuencia.

Ahora, con esto entendido a grandes rasgos, podemos entender que es la vulnerabilidad XXE.
Toma ventaja de cómo los parseos XML maneja las entidades externas. Si la sanitización no es realizada de forma correcta, el atacante podría apuntar a un código malicioso.
Por ejemplo, si se viera así:
```XML
<!DOCTYPE people[
	<!ENTITY thmFile SYSTEM "file:///etc/passwd">
]>
<people>
	<name>Glitch</name>
	<address>&thmFile;</address>
	<email>glitch@wareville.com</email>
	<phone>111000</phone>
</people>
```
Aquí la entidad `thmFile` refiere al archivo `/etc/passwd` en el sistema.

# BurpSuite
En este ejercicio vamos a rutear el tráfico a través de BurpSuite para poder analizarlo.
Burp Suite es una plataforma para realizar pruebas de seguridad en aplicaciones web. Incluye varias herramientas para escanear, fuzz, interceptar y analizar el tráfico web.

Lo que haremos será utilizarlo para capturar el tráfico de "Wareville's Wishville", una página donde podemos agregar productos a un carrito de compras y estos son enviados a un servidor interno.

---

# Wareville's Wishville

![](https://i.imgur.com/woPu9Pc.png)
Vamos a hacer las primeras investigaciones. Iremos por el procedimiento estándar de agregar un producto, irnos al carrito, hacer  checkout y ver qué sucede.
![](https://i.imgur.com/wwuX6pR.png)
![](https://i.imgur.com/6ZNjvTB.png)
Esto básicamente nos dice que no tenemos los permisos necesarios. Pero además nos dice que se guardan en un archivo de texto hosteado en /wishes/ y que además esos archivos van creciendo, por lo tanto hay un 20, 19, 18... y así.

Vamos a interceptar el request para ver qué información trae.
Para ello usaremos Burp Suite.
![](https://i.imgur.com/1YnfMZ3.png)
![](https://i.imgur.com/XszlIOt.png)
La pantalla de inicio que nos recibe es así, donde podemos ver varias pestañas con distintas utilidades.
![](https://i.imgur.com/Kv31mnW.png)
Nos iremos a proxy -> Open Browser. De este modo, Burp suite ruteará todo a través de sí mismo.
![](https://i.imgur.com/I37xYl0.png)

Cuando agregamos un producto a la wishlist, en la págin, podemos ver que a través de una llamada AJAX se llama a wishlist.php:
![](https://i.imgur.com/rETUKnz.png)
Si revisamos detenidamente la forma en que se parsea el XML nos encontramos con esto:
```php
libxml_disable_entity_loader(false);
$wishlist = simplexml_load_string($xml_data, "SimpleXMLElement", LIBXML_NOENT);
```
Con esto podemos identificar que la carga de entidades externas está habilitada, por lo tanto la la parte de `LIBXML_NOENT` no tiene utilidad, ergo, podemos inyectar XXE.
```XML
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/etc/hosts"> ]>
<wishlist>
	<user_id>1</user_id>
		<item>
			<product_id>&payload;</product_id>
		</item>
</wishlist>
```
Lo que esto hará es básicamente definir la entidad como payload, acceder a system y recibir "/etc/hosts" que será parseado en la parte de `<product_id>&payload;</product_id>`

Nos vamos al repetidor de Burpsuite con el que podemos repetir n veces un request.
Básicamente vamos a duplicar el post de wishlist.php, pasarle el payload y recibir el contenido.

!!!!!!

Modificaremos la parte del payload para acceder a `"/var/www/html/wishes/wish_n.txt` y ver que encontramos en ellos.

!!!!!

Con esto, hemos realizado exitósamente un ataque XXE.

----

# Preguntas

- ¿Cuál es la bandera que obtenemos al navegar por los wish_n.txt?
	- Se encuentra en uno de los wish_n.txt
- ¿Cuál es la bandera que obtenemos en la posible prueba de sabotaje?
	- Sólo debemos revisar el changelog que nos proporcionan

Con eso hemos logrado completar el desafío del día 5
![](https://i.imgur.com/7lvBDWB.png)

Procedamos al [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 6\|día 6]]