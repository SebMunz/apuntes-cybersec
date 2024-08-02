---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Ciclo de Red/02 Exfiltracion/"}
---

# Exfiltración

## Atacante
En la perspectiva del atacante, previo a lograr la exfiltración, primero necesita ganar acceso a la red y al sistema. Habitualmente, esto ocurre a través de la ingeniería social.
Al ganar la posición inicial en el sistema, el atacante debe mantener el acceso y evitar ser detectado. Para lograrlo, harán uso del pivoteo o movimiento lateral, en el cual exploran la red para expandir y mantener el acceso hacia otros sistemas.

Una vez establecida la posición en la red, identificarán los activos importantes buscando en las redes internas, repositorios de códigos, archivos compartidos y otros. Luego de identificar los activos de valor, necesitan recolectarlos, empaquetarlos y prepararlos para la exfiltración. Una forma común es reduciendo el tamaño de los paquetes, de esta forma se mantienen bajo el radar. Finalmente, se exfiltra la información. Esto puede ser de muchas formas distintas, pero una común es utilizar el correo electrónico de un empleado para enviarla.

## Defensa
La primera línea de defensa es prevenir el acceso no autorizado. Para ello, existen muchos métodos, siendo el más común requerir autenticación multifactor (MFA) y proporcionar un constante entrenamiento al personal en seguridad.

Si a pesar de estas medidas el atacante logra ganar acceso, es importante detectar su presencia en la red lo antes posible. Esto se puede lograr mediante el monitoreo continuo de la actividad de red en busca de actividades sospechosas, como múltiples inicios de sesión de usuarios desde ubicaciones inusuales.

Las organizaciones deben mantener un catálogo de activos críticos y aplicar los controles de seguridad adecuados a cada uno de ellos. Además, se deben implementar medidas para detectar y detener la exfiltración de datos. Esto incluye monitorear la red en busca de movimientos inusuales de archivos, cargas de datos grandes hacia el exterior y escrituras de archivos no autorizadas.

Las herramientas de gestión de la información y eventos de seguridad (SIEM) son útiles para detectar y alertar sobre actividades sospechosas en la red. En caso de detectar una exfiltración de datos, una respuesta rápida puede incluir el bloqueo de las direcciones IP asociadas con el atacante mediante reglas de firewall.

## Enlaces Adicionales
- [MITRE ATT&CK: Data Exfiltration Techniques](https://attack.mitre.org/tactics/TA0010/)
- [MITRE ATT&CK: Network Traffic Analysis](https://attack.mitre.org/datasources/DS0029/)