---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Conceptos fundamentales de seguridad/"}
---

# Conceptos Fundamentales de Seguridad

- **Riesgo:** Cualquier hecho que pueda afectar la confidencialidad, integridad o disponibilidad de un activo.
- **Amenaza:** Cualquier circunstancia o evento que pueda afectar negativamente a los activos.
- **Vulnerabilidad:** Debilidad que puede ser aprovechada por una amenaza.

Dado que cada empresa valora activos específicos, tienden a diferir en el modo en que interpretan y abordan el riesgo. Una manera de interpretar el riesgo es considerar los posibles efectos que los eventos negativos pueden tener en una empresa. Otra forma de presentar esta idea es con el siguiente cálculo:


*PROBABILIDAD* x *IMPACTO* = *RIESGO*


Los dos factores de riesgo comunes son las amenazas y las vulnerabilidades. El riesgo de que un activo sufra daños depende en gran medida de si una amenaza aprovecha las vulnerabilidades.

---

## Categorías de Amenazas

Las amenazas se clasifican en dos categorías: intencionales e involuntarias.

- **Amenaza Intencional:** Por ejemplo, un hacker malicioso que obtiene acceso a información confidencial al atacar una aplicación mal configurada.
- **Amenaza Involuntaria:** En cambio, un empleado que sostiene la puerta abierta para una persona desconocida y le otorga acceso a un área restringida.

---

## Categorías de Vulnerabilidad

Las vulnerabilidades se pueden clasificar en dos categorías: técnicas y humanas.

- **Vulnerabilidad Técnica:** Por ejemplo, un software mal configurado que permita a una persona no autorizada acceder a datos importantes.
- **Vulnerabilidad Humana:** Mientras tanto, un empleado olvidadizo que pierde su tarjeta de acceso en el estacionamiento.

---

# CIA TRIAD

### Confidentiality

**La confidencialidad apunta a proteger la información sensible de intrusos o usuarios no autorizados.**

Esto de 3 formas principales
- Encriptación
  - Convertir información en no legible para usuarios no autorizados.
- Authenticación
  - Asegurar la identidad de quién está intentando acceder al sistema o información. Generalmente con credenciales (password/biométrica/etc)
- Control de acceso
  - Definir y regular que recursos o información pueden acceder ciertos usuarios y bajo qué circunstancias
### Integrity
La integridad asegura que la información y sistemas estén protegidos contra usuarios no autorizados. Crucial para mantener consistencia, precision y fiabilidad en los sistemas y la información.

###### Los tres puntos principales
- Checksums
  - Cálculos matemáticos usados para verificar la integridad de la información y detectar cambios
- Permisos de archivos
  - Asegurar que sólo los usuarios autorizados tengan la habilidad de modificar o borrar archivos específicos
- Firmas digitales
  - Técnica criptográfica que puede ser usada para autenticar la fuente e integridad de la información o mensajes.
### Availability
La disponibilidad asegura que los sistemas sean accesibles y funcionales cuando sea necesario. Mientras mejor sea, más eficiente y fiable serán los sistemas

**Los tres puntos principales:**
- Redundancia
  - Duplicados o respaldos de sistemas o archivos críticos que pueden ser usados para garantizar la disponibilidad del sistema
- Tolerancia al fallo
  - Capacidad del sistema de continuar funcionando aun cuando hayan ciertas fallas
- Respaldos
  - Copias regulares de la información para prevenir pérdidas en caso de catástrofe (malwares, desastres naturales, fallas del sistema)
### Los planes de seguridad se basan en tres elementos
_Assets, Threats y Vulnerabilities_

- __ASSETS__
Un asset (activo) es un item percibido como de valor para la organización.
  - El edificio, equipos, información, empleados.
- __THREATS__
Los threats (amenazas) es una circunstancia o evento que tiene un impacto negativo en los activos.
  - Ataques directos, phishing, filtraciones
  - Pueden ser __involuntarios__ o __intencionales__
__VULNERABILITIES__
Las vulnerabilidades son debilidades que pueden ser explotadas por una amenaza.
  - Contraseñas no seguras, privilegios mal administrados, configuraciones por defecto.
  - Pueden ser __técnicas__ o __humanas__

![imagen](https://github.com/SebMunz/Cybersec/assets/104586558/a8003fe9-c477-48de-9b3e-11411c51669b)
*Ejemplo de un inventario de activos conectados en mi casa*

La información tiene tres estados
- En uso
  - Que ha sido accedida por una o más persona (por ej buzón de correo electrónico)
- En tránsito
  - Que está viajando de un punto a otro (una respuesta a un correo electrónico)
- En descanso
  - Cuando no está siendo activamente usada (cuando cerramos dicha sesión y no estamos activamente revisandolo)
## D.A.D.
El opuesto de CIA.
- **D**isclosure
	- El divulgar la información rompe la confidencialidad
- **A**lteration
	- Alterar la información rompe la integridad de la misma, ya no es confiable
- **D**estruction/**D**enial
	- Destruir la información haría que esta ya no esté disponible, lo mismo el denegar su acceso a quien lo necesite

---

# ISO/IEC 19249
5 principios de arquitectura para principios de seguridad:

1. **Separación de dominios**: Cada componente relacionado se agrupa en una sola entidad. Cada entidad se le debe asignar un grupo común de atributos de seguridad.
	- Por ejemplo: los niveles de seguridad de los procesadores x86: El kernel del SO funciona en el ring 0 (más privilegio), pero las aplicaciones corren en el ring 3 (menos privilegio). La separación de modelos se incluye en el modelo Goguen-Meseguer.
2. **Realizar capas**: Un sistema estructurado en capas se vuelve más fácil de imponer políticas de seguridad en distintos niveles.
	- Por ejemplo: En el [[IT fundamentos/Conexiones y Redes/Modelo OSI\|Modelo OSI]], cada capa provee de un servicio específico a la capa que le precede.
3. **Encapsulación**: Simplificar los métodos a realizar. Por ejemplo en la programación orientada a objetos (OOP), escondemos implementaciones de bajo nivel para prevenir manipulación directa y proveemos de un método específico para ese objetivo.
	- Por ejemplo: Una API es un método de encapsulación.
4. **Redundancia**: Asegurar la disponibilidad y la integridad.
	- Por ejemplo: un servidor con dos PSU. Si una falla, el sistema continua funcionando.
5. **Virtualizacion**: Compartir el hardware para múltiples sistemas operativos. Esto permite tener entornos de prueba, potenciar el alcance de la seguridad, detonación segura de material desconocido y la observación controlada de programas maliciosos.

ISO/IEC 19249 entrega 5 principios de diseño seguro:

1. **Menor privilegio**: Respondiendo la pregunta "¿quién puede acceder qué?". El principio enseña que debes proveer el mínimo de permisos a alguien para que pueda realizar la tarea necesaria.
	- Por ejemplo: Una persona necesita leer un documento para realizar su trabajo. Sólo le damos permisos de lectura y no de escritura.
2. **Minimizar superficie de ataque**: Todos los sistemas tienen vulnerabilidades que pueden ser explotadas para comprometer un sistema. Algunas son conocidas y [[Ciberseguridad/Ataques/Exploits y Vulnerabilidades#**Zero Day **\|otras no]]. Hay que minizar el riesgo que poseen.
	- Por ejemplo: Al realizar un [[hardening\|hardening]] de un SO, deshabilitamos todos los servicios que no necesitamos.
3. **Validación de parámetros centralizados**: Muchas amenazas ocurren al recibir información ingresada por usuarios. Ingresos inválidos pueden ser usados para explotar vulneraciones, como [[Ciberseguridad/Ataques/SQL Injection\|la inyección SQL]].
	- Por ejemplo: Utilizar un sistema ORM para sanitizar las entradas de usuarios en una aplicación web.
4. **Servicios de seguridad general centralizados**: Apuntar a centralizar todos los servicios de seguridad.
	- Por ejemplo: Un servidor centralizado para auth.
5. **Prepararse para los errores y manejo de errores**: Siempre considerar que los errores y excepciones **VAN** a ocurrir y hay que estar preparado para ello.
	- Por ejemplo: Un usuario intentando comprar un producto que no está en stock.

---

# Zero Trust vs Trust but Verify

- **Confiar pero verificar**: Este principio enseña que siempre debemos verificar, incluso cuando confiamos en la entidad y su funcionamiento. Una entidad puede ser un usuario o un sistema. Verificar usualmente requiere de un mecanismo de [[IT fundamentos/Logs\|logging]] eficiente. También indica revisar dichos logs para asegurar que todo está normal. Revisar estos logs puede ser una tarea titánica si lo hiciéramos a mano y es por ello que utilizamos sistemas automatizados de seguridad como [[Ciberseguridad/Habilidades y conocimientos básicos/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR\|IDS, IPS, SIEM, SOAR]], [[Proxies\|Proxies]], etc.
- **Zero Trust**: Este principio enseña que todas las entidades son adversarios, hasta que se pruebe lo contrario. Zero Trust no le otorga confianza a una entidad basada en quién es el dueño o su lugar, contrario a otros sistemas donde si confiaríamos en entidades dentro de nuestra propia red o incluso equipos de la propia compañía.

La micro segmentación es un punto clave en el principio de Zero Trust, subdividimos y segmentamos distintas porciones de la red para diferir los permisos y accesos, necesitando una serie de cumplimientos para poder acceder y moverse en la red.

Existe un límite en cuanto podemos aplicar el zero trust sin afectar la [[Ciberseguridad/Habilidades y conocimientos básicos/CIA triad#Availability\|Disponibilidad]]. Pero debemos aplicarla lo más posible e ir de-escalando hacia Trust but Verify.


---

# Amenaza vs Riesgo

- Una vulnerabilidad es algo susceptible a ser atacado o dañado, una debilidad.
- Una amenaza es un potencial peligro asociado a dicha vulnerabilidad.
- El riesgo es básicamente que tan probable es que un oponente explote una vulnerabilidad y dicho impacto que podría causar.

#to-do 

---

