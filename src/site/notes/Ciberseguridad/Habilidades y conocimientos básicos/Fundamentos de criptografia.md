---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Fundamentos de criptografia/"}
---



# Fundamentos de Criptografía
### Proceso de transformar información en una forma que los lectores no autorizados no puedan entender.

Se utilizan el mensaje a cifrar (__ciphertext__) y una llave criptográfica (__cipherkey__), el cual es un mecanismo que desencripta dicho ciphertext a plaintext (texto legible, plano, normal).

__Toda forma de encriptación necesita el cifrado y la llave para asegurar el intercambio de información.__

Por ejemplo, una de las formas de encriptación más antigua es el _cifrado Cesar_ (Caesar's cipher), nombrado así por ser el método utilizado por Julio Cesar para comunicarse con sus generales.
Se cifraban mensajes a través de una llave que no era más que mover las letras en un número fijo de espacios.

Por ejemplo, __Hola__, usando un cifrado cesar de 3, sería __Krod__, porque se mueven las letras 3 espacios.
Dicho cifrado actualmente es muy débil porque la cantidad de pruebas necesarias para desencriptar un mensaje se limita a la cantidad de letras del abecedario, por lo tanto sólo se necesitan unos ~26 intentos para descifrar el mensaje.

Esta táctica se llama [[Ciberseguridad/Ataques/Fuerza bruta#Brute Force - Ataque de Fuerza Bruta\|Ataque de fuerza bruta]], un proceso donde se prueban -a la fuerza- diferentes combinaciones.

## Cifrado simétrico y asimétrico

Existen dos tipos principales de cifrado:
- Simétrico:
  - Una única clave secreta para el intercambio de información.
  - Remitente y receptor deben conocer/tener dicha clave

- Asimétrico:
   - Dos claves, una pública para cifrar y una privada para descifrar.

---
# Criptoanálisis

Analizar el proceso de criptografía para mejorar el proceso de encriptación y/o generar nuevas formas de defensa.
La encriptación moderna se basa en su mayoría en la factorización de números primos grandes que son difíciles de calcular manualmente. La misma evolución tecnológica que permite estos algoritmos, también habilita la desencriptación más rápida mediante factorización y ataques de fuerza bruta, incluso botnets pueden ayudar en estos procesos.

## Ataques de criptoanálisis
- KPA: Known Plaintext Attack
	- Acceso a parte o la totalidad del texto simple de la información encriptada.
	- Se conoce el plaintext ("crib") y la versión encriptada.
	- No tiene etiqueta computacional, no tiene formato especial ni está escrito en código.
	- El objetivo es analizar el texto para determinar la clave
- CPA: Chosen Plaintext Attack
	- Atacante conoce el agoritmo de encriptación o tiene acceso a usarlo
	- Atacante puede obtener los textos según un set arbitrario que él envía
- ACPA: Adaptive chosen plaintext attack
	- Similar al CPA, pero va adaptando su análisis usando textos subsecuentes
- RKA: Related key attack
	- Similar al CPA, pero el atacante obtiene los ciphers encriptados con dos llaves diferentes.
	- Las llaves son desconocidas, pero se conoce su relación; ejemplo dos llaves difieren en el  bit 1
- COA: Cipher only attack
	- Sólo se conoce el mensaje encriptado.
	- Es la forma más común cuando se interceptan comunicaciones encriptadas

### Resultados
Algunos ataques logran la ruptura total de la encriptación, mientras que otros obtienen información que puede ayudar al atacante a causar daños.
- Deducción de instancias
	- Atacante descubre más texto sin formato o cifrado
	- No se obtuvo la clave pero con esto podemos usarlo para seguir analizando/atacando
- Deducción de la información
	- Atacante obtiene información sobre un texto sin formato o cifrado que no conocía
	- Se puede usar para obtener más datos sobre la clave
- Algoritmo de distinción
	- Atacante pudo distinguir el algoritmo de encriptación de una alteración aleatoria
- Deducción global
	- Identificación del algoritmo funcionalmente equivalente al que se usa en la clave
- Ruptura total
	- atacante logra obtener la clave completa y con ello tener acceso total


---
---
---

# PKI
#### Public key infraestructure - Infraestructura de llaves pública

Se utilizan muchos algoritmos para enviar y almacenar información. Mantener individualmente un manejo de todas estas llaves de encriptación es una tarea imposible para el individuo común. Para esto existe la PKI.

_PKI_ es un framework de encriptación que asegura el intercambio de información online.
Es un proceso de dos pasos el cual comienza con el intercambio de información encriptada.
Esto involucra la encriptación asimétrica, simétrica o ambas.

- Asimétrica
  - Involucra el uso de una llave pública y una privada para la encriptación y la desencriptación.
  - A grandes rasgos, es como una caja con la cual todos tienen una llave para abrirla e introducir cosas pero sólo el dueño de la caja puede sacarlas. Como un buzón de una sola vía.
  - Seguro, pero a la vez es más lento.

- Simétrica
  - Se utiliza sólo una llave secreta para el intercambio
  - Usando la caja nuevamente, el dueño puede abrirla, introducir cosas y sacarlas cuando quiera, pero para hacer intercambios debe facilitar tanto la caja como la llave.
  - Menos seguro, pero más rápido

PKI utiliza ambas encriptaciónes, a veces al mismo tiempo. Depende de si se prioriza la velocidad o la seguridad.
Sin embargo existe una vulnerabilidad común: establecer confianza entre emisor y receptor.
Ambos procesos se basan en compartir llaves que se pueden perder, robar o darles un mal uso.
__Es ahí donde el segundo proceso de las PKI entran.__
Se mitiga dicha vulnerabilidad al establecer la confiabilidad a través de un sistema de certificados digitales entre los computadores y las redes.

---
---
---
---

# Certificado Digital de seguridad.

Un certificado digital es un archivo que verifica la identidad de quien mantiene una llave pública. La mayoría de la información online se intercambia con estos certificados.
Una forma en que estos certificados se obtienen es cuando se registra un dominio web, quien hace de host envia la información del registrante a una autoridad de certificación. Ahí se provee de una llave pública. La autoridad luego encripta la información con su propia llave privada. Finalmente, se crea el certificado que contiene la información encriptada del registrante. También se incluye la firma digital de autenticidad por parte de la autoridad de certificación.

Una forma de simplificarlo es verlo como tarjetas de identificación online la scuales se usan para restringir o garantizar acceso a la información


---
---
---
---

# Algoritmos
Los más usados:

**Simétrico**
- Triple DES (3DES)
   - Cifrado por bloques. El original (DES) generaba claves de 64 bits. 3DES genera claves de 192 bits (24 caracteres).
   - Aún se utiliza por comptabilidad con versiones
 - AES
   - De los más seguros actualmente. Genera claves de 128, 192 y 256 bits.
   - Se considera seguro a los ataques de fuerza bruta ya que forzar una clave de 128 bits, le tomaría varios miles de millones de años a un computador moderno.

**Asimétrico**
- Rivest, Shamir y Adleman (RSA)
   - Desarrollado por el MIT. De los primeros asimétricos en generar pública y privada.
   - Significativamente más larga gracias a ser dos claves. Longitudes van desde 1024 bits a los 4096 bits.
- Algoritmo de firma digital (DSA)
   - Desarrollado por el NIST. Genera claves de 2048 bits.
   - Ampliamente usado como complemento de RSA para PKI

Su implementación se solía hacer a través de OpenSSL pero esto ya no es recomendado debido al error Heartbleed en el 2014. 
Hoy en día hay diversas formas de implementarlos.

**Importante mencionar el principio de Kerchoff. La criptografía debe diseñarse de modo que todos los detalles del algoritmo, excepto la clave privada, pueden ser públicos sin perder su seguridad.**

---
---
---
---

# HASH

Algoritmo que produce un código que **no puede ser desencriptado.**
A diferencia de los algoritmos de cifrado simétricos y asimétricos, este **no produce una llave de desencriptación.** Lo que produce, es un identificador, conocido como valor hash (Hash value) o digest. Estos, son valores cortos de una longitud fija derivada de una entrada de longitud variable.

La gracia de utilizar Hash es que sirven para determinar la integridad de los archivos y aplicaciones. Esto ya que puedes tener un programa que hace exactamente lo mismo pero basta con que se cambie una linea de código para que el valor hash sea diferente.

La integridad de la información se relaciona con la exactitud y la consistencia de la información. Esto se conoce como no repudio (non-repudiation), **el concepto de que la autenticidad de la información no se puede negar.**

Las funciones hash son controles de seguridad importantes que ayudan a mantener la integridad de la información.
Una forma de verificar esto es revisar los valores de archivos o aplicaciones y compararlos contra archivos maliciosos conocidos.

>En linux podemos usar el CLI para generar el valor hash de cualquier archivo.
[REFERIRSE A LOS ARCHIVOS DE LINUX PARA MÁS INFORMACIÓN](-AQUIVAELENLACE-)

---

El message digest 5 es una de las primeras funciones Hash creadas en los 90.
Originalmente las funciones hash eran utilizadas para encontrar ciertos datos más rápido mediante el uso de *una tabla hash*, que es una estructura de datos utilizada para almacenar y referenciar valores hash.

Una de las fallas del MD5 es la limitación con el conjunto de salidas. Si bien, las entradas pueden ser infinitas, las salidas son limitadas a una extensión de 32 caracteres. De ahí, aparece un problema llamado **colisión de hash**, diferentes entradas produciendo el mismo valor hash. Esto, puede ocacionar una duplicidad en la identidad y ser utilizado por atacantes maliciosos para suplantar datos auténticos.

Para evitar el hash colision, se necesitaban valores más largos. De ahí aparecen los algoritmos de hash seguro o *SHA*.
El NIST es el encargado de aprobar cada uno de estos algoritmos. Junto a cada función SHA se indica el tamaño de su valor en bits, a excepción de SHA-1 que produce 160 bits.
Son seguros a la colisión, pero no invulnerables a otros exploits.

Cinco funciones SHA

- SHA-1
- SHA-224
- SHA-256
- SHA-384
- SHA-512

### SALTING

Protección adicional usada para reforzar las funciones. Básicamente 'le echamos sal' que es una cadena aleatoria de caracteres que se agrega a una entrada durante el proceso.
Esto suele usarse al principio o al final de los datos. Un uso común para este condimentado es el de almacenamiento de contraseñas.