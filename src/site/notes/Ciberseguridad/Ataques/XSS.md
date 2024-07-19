---
{"dg-publish":true,"permalink":"/Ciberseguridad/Ataques/XSS/"}
---

# Web Exploits

La Inyección XSS, o Cross Site Scripting, es una forma de ataque que aprovecha vulnerabilidades en aplicaciones web. Dado que estas interactúan con numerosos usuarios, la exposición de información personal sensible es considerable. Un método común es la inyección de código malicioso, particularmente en el contexto de ataques de inyección.


## XSS

**Cross Site Scripting (XSS):** Un ataque de inyección que inserta código en un sitio web vulnerable, explotando las dos tecnologías web principales: HTML y JS. Hay tres tipos principales de ataques XSS:

1. **Reflejado:**
   - El script se envía al servidor y se activa durante la respuesta del servidor. Se puede lograr mediante la modificación de la URL.
> En este ataque se podría usar la barra de búsqueda para primero insertar el código malicioso en la página y modificar ligeramente la URL. Si el sitio web no sanitiza adecuadamente la entrada del usuario, se ejecutará el script cuando otro usuario visite la misma URL.

---

2. **Almacenado:**
   - El script malicioso se almacena en el servidor y se entrega a los usuarios cuando solicitan una página específica, como en secciones de comentarios.
> Supongamos que un sitio web tiene una sección de comentarios de los usuarios. Cada comentario se almacena en la base de datos con una ID. Si un usuario hace un comentario con un código malicioso, este se almacenaría en la DB y cuando su ID sea requerido por otro usuario, se ejecutará el código almacenado.

---

3. **DOM-based:**
   - El script manipula el Document Object Model (DOM) interpretado por el navegador. Puede ocurrir al manipular la configuración de una página.
> Supongamos que una página web permite cambiar el fondo según preferencia. La configuración se almacena en una URL. Un atacante podría aprovecharse de la URL para inyectar un script. De esta forma, cuando el usuario visite la URL, se ejecutará el script.

Además, existen variantes como XSS basado en el navegador, de terceros, de imagen, basado en el evento, basado en el tiempo y basado en el historial. Cada uno explota diversas vulnerabilidades para inyectar scripts maliciosos.

En resumen, los ataques XSS se centran en la manipulación directa del código HTML y JS para infiltrarse en el código fuente y comprometer la seguridad de las aplicaciones web.

### Input Sanitization

La sanitización de entradas es crucial para prevenir ataques de inyección. Las aplicaciones web, debido a su variedad de interacciones con usuarios, a menudo enfrentan dificultades para lograr una sanitización efectiva.
