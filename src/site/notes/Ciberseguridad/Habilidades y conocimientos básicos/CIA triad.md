---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/CIA triad/"}
---

# CIA TRIAD

> Confidentiality
#### La confidencialidad apunta a proteger la información sensible de intrusos o usuarios no autorizados.

###### Esto de 3 formas principales
- Encriptación
  - Convertir información en no legible para usuarios no autorizados.

- Authenticación
  - Asegurar la identidad de quién está intentando acceder al sistema o información. Generalmente con credenciales (password/biométrica/etc)

- Control de acceso
  - Definir y regular que recursos o información pueden acceder ciertos usuarios y bajo qué circunstancias

---

> Integridad
#### La integridad asegura que la información y sistemas estén protegidos contra usuarios no autorizados. Crucial para mantener consistencia, precision y fiabilidad en los sistemas y la información.

###### Los tres puntos principales
- Checksums
  - Cálculos matemáticos usados para verificar la integridad de la información y detectar cambios

- Permisos de archivos
  - Asegurar que sólo los usuarios autorizados tengan la habilidad de modificar o borrar archivos específicos

- Firmas digitales
  - Técnica criptográfica que puede ser usada para autenticar la fuente e integridad de la información o mensajes.

---

> Availability
#### La disponibilidad asegura que los sistemas sean accesibles y funcionales cuando sea necesario. Mientras mejor sea, más eficiente y fiable serán los sistemas

###### Los tres puntos principales:
- Redundancia
  - Duplicados o respaldos de sistemas o archivos críticos que pueden ser usados para garantizar la disponibilidad del sistema

- Tolerancia al fallo
  - Capacidad del sistema de continuar funcionando aun cuando hayan ciertas fallas

- Respaldos
  - Copias regulares de la información para prevenir pérdidas en caso de catástrofe (malwares, desastres naturales, fallas del sistema)


---

#### Los planes de seguridad se basan en tres elementos
_Assets_, _Threats_ y _Vulnerabilities_.

- __ASSETS__
Un asset (activo) es un item percibido como de valor para la organización.
  - El edificio, equipos, información, empleados.

- __THREATS__
Los threats (amenazas) es una circunstancia o evento que tiene un impacto negativo en los activos.
  - Ataques directos, phishing, filtraciones
  - Pueden ser __involuntarios__ o __intencionales__
- __VULNERABILITIES__
Las vulnerabilidades son debilidades que pueden ser explorata por una amenaza.
  - Contraseñas no seguras, privilegios mal administrados, configuraciones por defecto.
  - Pueden ser __técnicas__ o __humanas__
 
--- 

Ejemplo de un inventario de activos conectados en mi casa
![imagen](https://github.com/SebMunz/Cybersec/assets/104586558/a8003fe9-c477-48de-9b3e-11411c51669b)

---

#### La información tiene tres estados
- En uso
  - Que ha sido accedida por una o más persona (por ej buzón de correo electrónico)
- En tránsito
  - Que está viajando de un punto a otro (una respuesta a un correo electrónico)
- En descanso
  - Cuando no está siendo activamente usada (cuando cerramos dicha sesión y no estamos activamente revisandolo)
