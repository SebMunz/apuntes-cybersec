---
{"dg-publish":true,"permalink":"/IT fundamentos/Computador/"}
---

Como se mencionó al inicio, la regla de oro es que "si hace cálculos, es un computador". Al fin y al cabo, un computador calcula, procesa y almacena información.

Un computador de escritorio es uno de los tipos de computador más comunes. Son los que colocamos debajo o encima del escritorio, conectados a un monitor, usando un mouse y un teclado independientes.

## Anatomía básica

Los componentes más típicos del computador de escritorio son:

- **CPU (Central Processing Unit)**: Básicamente el cerebro, que hace los cálculos y procesamientos.
- **RAM (Random Access Memory)**: La memoria a corto plazo del computador. Guarda temporalmente la información.
- **Almacenamiento**: Esto puede ser un HDD (Hard Disk Drive), SSD (Solid State Disk) u otros. Es el almacenamiento a largo plazo.
- **Motherboard (Placa base)**: Es el cuerpo del computador, donde conectamos todos los demás componentes.
- **GPU (Graphical Processing Unit)**: Lo que conocemos como "tarjeta de video". Puede ser integrada en la misma placa o una externa. Procesa todo lo relacionado con la visualización o el display.
- **PSU (Power Supply Unit)**: Fuente de alimentación. Si su potencia no es suficiente, los componentes no funcionarán adecuadamente o directamente no encenderán.

Además de estos componentes, hay otros que también pueden ser relevantes:

- **Ventiladores y Sistemas de Refrigeración**: Mantienen la temperatura adecuada para que los componentes funcionen correctamente.
- **Unidad Óptica (CD/DVD/Blu-ray)**: Permite leer y escribir datos en discos ópticos.
- **Tarjeta de Sonido**: Procesa la entrada y salida de audio.
- **Tarjeta de Red (NIC, Network Interface Card)**: Conecta el computador a una red, ya sea por cable o inalámbricamente.

Todo esto es aplicable a cualquier otro dispositivo, incluyendo teléfonos, relojes, etc.

## Componentes

Más detallado.

### CPU

Como mencionamos, la CPU es el cerebro. En su esencia, la CPU es una potente calculadora con instrucciones. Estas instrucciones son básicamente comandos para procesar datos. Para que estos datos viajen por todo el computador, se usan los EDB (Bus de Datos Externos).

Además, las CPU tienen "registros". Básicamente, son cajones donde almacenar información con la que deben trabajar.

Dada la naturaleza de la velocidad de cómputo, la CPU es más rápida en su procesamiento que en su lectura, por lo tanto utilizamos otros componentes que ayudan en esto, como la RAM.

De manera similar, dada la velocidad de cómputo, nuestra CPU debe saber cuándo una instrucción comienza y cuándo termina. Para ello, utiliza un reloj interno que sincroniza estas tareas, el cual se conecta al "cable de reloj". Este envía un voltaje al cable para que comience en sus cálculos (ciclo de reloj - ciclo de operaciones).

### RAM

La RAM es básicamente un almacenamiento que funciona mientras el computador esté encendido. Ciertos programas son copiados por la CPU a la RAM para agilizar ciertos procesos. La parte "Random" de RAM permite que nuestra CPU pueda leer rápidamente cualquier parte de la memoria.

La RAM almacena millones y millones de líneas, por lo tanto la transferencia a través de los EDB sería imposible. Para ello, usamos algo llamado MCC (Chip Controlador de Memoria), el cual se encarga de comunicar la CPU y la RAM. El proceso es a grandes rasgos así: la CPU se comunica con el MCC y pide X. El MCC encuentra X en la RAM y utiliza el EDB para enviarlo. Dentro de este proceso también nos encontramos con el Bus de Direcciones, que conecta la CPU al MCC y maneja las direcciones de la información (pero no la información en sí).

Sin embargo, la RAM no es la forma más rápida de entregarle información a la CPU para procesamiento. Para ello tenemos la caché.

### Caché

Es más pequeña que la RAM pero almacena información que se usa con frecuencia para el correcto funcionamiento. Usualmente tenemos tres niveles de esta caché: L1, L2 y L3, siendo L1 la más pequeña y rápida.

### Almacenamiento

El almacenamiento se refiere a la capacidad del computador para guardar datos a largo plazo. Los tipos más comunes son:

- **HDD (Hard Disk Drive)**: Utiliza discos magnéticos para almacenar datos. Es más lento pero más barato y con mayor capacidad de almacenamiento.
- **SSD (Solid State Drive)**: Utiliza memoria flash para almacenar datos. Es más rápido y resistente, pero generalmente más caro.
- **SD (Secure Digital)**: Utilizado principalmente en cámaras y dispositivos portátiles.

### Motherboard (Placa base)

Es el componente principal que conecta todos los demás componentes del computador. Incluye ranuras para la CPU, RAM, GPU y otros periféricos. También contiene el chipset, que controla la comunicación entre los componentes.

### GPU (Graphical Processing Unit)

La GPU se encarga del procesamiento gráfico. Puede estar integrada en la placa base o ser una tarjeta dedicada. Es esencial para aplicaciones gráficas intensivas como juegos y diseño gráfico.

### PSU (Power Supply Unit)

La fuente de alimentación proporciona la energía necesaria para todos los componentes del computador. Su potencia se mide en vatios (W) y debe ser suficiente para cubrir el consumo total del sistema.

### Otros Componentes Relevantes

- **Ventiladores y Sistemas de Refrigeración**: Esenciales para mantener una temperatura adecuada y evitar el sobrecalentamiento.
- **Unidad Óptica**: Permite leer y escribir datos en discos como CD, DVD y Blu-ray.
- **Tarjeta de Sonido**: Maneja la entrada y salida de audio.
- **Tarjeta de Red (NIC)**: Permite la conexión a redes, ya sea por cable (Ethernet) o inalámbrica (Wi-Fi).