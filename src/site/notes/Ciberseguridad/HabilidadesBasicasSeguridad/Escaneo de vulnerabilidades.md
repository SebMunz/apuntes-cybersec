---
{"dg-publish":true,"permalink":"/Ciberseguridad/HabilidadesBasicasSeguridad/Escaneo de vulnerabilidades/"}
---

# Métodos para el Escaneo de Vulnerabilidades

En la mayoría de los casos, se emplea alguna herramienta capaz de automatizar los escaneos de vulnerabilidades. Estas herramientas simulan amenazas, buscando debilidades en una superficie de ataque.

Un escáner de vulnerabilidades (Vulnerability Scanning Tools) es un software que compara automáticamente las vulnerabilidades y exposiciones conocidas con las tecnologías de la red. Por lo general, analizan los sistemas. Durante un escaneo, la herramienta compara los hallazgos con las bases de datos de amenazas de seguridad, marcando cualquier vulnerabilidad encontrada y agregándola a su base de datos de referencia. Aunque son generalmente no intrusivos, en raros casos pueden provocar problemas como el colapso de un sistema.

Existen diversas formas de realizar estos escaneos, cada uno contemplando un posible camino que un atacante podría tomar.

## Tipos de Escaneo:

- **Externo vs Interno:**
    - *Externo:* Prueba la capa perimetral fuera de la red interna, analizando sistemas como firewalls y sitios web externos. Puede descubrir puertos de red o servidores vulnerables.
    - *Interno:* Examina sistemas internos, por ejemplo, analizando software en busca de debilidades en la forma en que gestiona la entrada de usuarios.

- **Autenticado vs No Autenticado:**
    - *Autenticado:* Prueba un sistema iniciando sesión con una cuenta de usuario real, verificando vulnerabilidades como controles de acceso mal configurados.
    - *No Autenticado:* Simula ataques externos sin acceso, por ejemplo, analizando recursos compartidos de archivos internos. Deberían recibir "acceso denegado" al intentar abrirlos.

- **Limitado vs Completo:**
    - *Limitado:* Analiza dispositivos específicos en una red, como configuraciones erróneas en un firewall.
    - *Completo:* Analiza TODOS los dispositivos en una red (SO, DB, etc.).
    - *Recomendación:* Realizar un escaneo de descubrimiento previo.

Este enfoque estratégico en diferentes dimensiones proporciona una comprensión más completa de la postura de seguridad de una organización.
