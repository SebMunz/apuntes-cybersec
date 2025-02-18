---
{"dg-publish":true,"permalink":"/Fundamentos TI/01 Introducción TI/"}
---

# Qué es

TI significa tecnologías de la información y esto engloba todo el espectro de la tecnología digital y su uso, como computadores, redes, equipamiento como servidores e impresoras, etc.
Si nos vamos a lo fundamental, es que todas estas tecnologías son en su base sólo 0 y 1, osea, código binario y por lo tanto todo funciona en base a puertas lógicas.

Importante mencionar que computador es también un término que **no** es exclusivamente para el computador de escritorio. También incluye servidores, relojes inteligentes, TV digital, domótica, etc.
La regla de oro es "si computa información, es un computador".

---
## Puertas lógicas

Básicamente componentes electrónicos que conducen electricidad según una regla, la cual suele ser **SÍ (ON, TRUE, OPEN, HIGH VOLTAGE)** y **NO (OFF, FALSE, CLOSED, LOW VOLTAGE)**.
Gracias a estas reglas, podemos acomplejar el mecanismo con la utilización de las puertas lógicas.
Por ejemplo:
##### AND
Una puerta **Y (AND)** tiene dos entradas **(A y B)**. Su salida ocurrirá sí, y sólo sí, ambas entradas son **ON**.
Osea, **A y B** deben ser verdadero para obtener una salida **verdadera**. Si A fuera verdadero y B fuera falso, entonces la salida de **AND** será falso.

##### OR
Una puerta O (**OR**) tiene dos entradas también (A y B). Su salida ocurrirá sí una de las dos entradas es verdadera.
Osea, A o B deben ser verdadero para obtener una salida verdadera. De lo contrario, será falso.
Esto quiere decir que A puede ser verdadero y B falso, B puede ser verdadero y A falso, A y B pueden ser verdaderos.

##### NOT
Una puerta NO (**NOT**) tiene una sola entrada (A). Si A es verdadera, su salida será falsa y viceversa.
Básicamente es un **inversor**.

##### XOR
Una puerta OR-EXCLUSIVA (**XOR**) tiene dos entradas. La salida será verdadera sí, y sólo sí, las dos entradas son distintas. Osea que sí son iguales, su salida será falsa.

##### NAND
Una puerta NO-Y (NAND). Su salida siempre es verdadera, excepto cuando ambas entradas son TRUE.
Osea, solamente Si y A y B son verdaderas, su salida será falsa. 

##### NOR
En una puerta NOR, su salida siempre es falsa, excepto cuando ambas entradas son FALSE.
Es decir que si A y B son falsas, entonces su salida es TRUE. Pero en todos los demás casos será FALSE.

##### XNOR
NOT EXCLUSIVE OR. Esto significa que su salida será TRUE si es que ambas entradas son iguales. Es el opuesto al XOR.

==**Este es el concepto más fundamental de cualquier dispositivo electrónico**==

---

## Capas principales

La infraestructura de un computador puede ser dividido en 4 capas principales:
- Hardware
- Sistema operativo
- Software
- Usuario
### [[Fundamentos TI/Computador#Componentes\|Hardware]]

Objetos tangibles que componen al computador. Estoy incluye almacenamiento (SD, SSD, HDD, etc), tarjetas gráficas (GPU), procesadores (CPU), periféricos (mouse, teclado, monitores) e incluso equipo como impresoras, teléfonos, etc.

### [[Fundamentos TI/Sistemas Operativos/Sistemas Operativos\|Sistemas Operativos]]

También escrito como OS (en inglés). Esto le permite al hardware comunicarse con el sistema a pesar de quién sea el fabricante. Tenemos distintos sistemas operativos pero los tres más populares son Windows, Linux y macOS. Sin embargo hay muchos más según el dispositivo y a su vez según el uso. Por ejemplo tenemos los sistemas para celulares como ios, Android, harmonyOS. Para otros dispositivos como Tizen (smartwatch), WebOS (TV, moviles), Zephyr (IoT, domótica), OpenVMS (servidores), z/OS (sistema IBM para mainframes), etc.

### Software

Facilita la interacción entre el humano y el computador. Es la forma en que damos ordenes al computador. Desde procesadores de palabras, un calendario, un navegador web o una aplicación móvil para pedir un completo, cada uno de ellos es un software que facilita la interacción entre usuario-computador.

### Usuario

El usuario es quien finalmente interactúa con los dispositivos. El usuario puede ser una persona común y corriente que utiliza su computador para jugar, enviar correos y navegar por internet o también una persona conectado a un sistema industrial para su trabajo.
Es importante que esta interacción sea efectiva para así evitar problemas y tener una buena experiencia de uso.

---

Por el momento, nos enfocaremos en lo que es el computador de escritorio/laptop moderno.