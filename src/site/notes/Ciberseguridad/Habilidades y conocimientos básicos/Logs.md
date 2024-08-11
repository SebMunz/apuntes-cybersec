---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Logs/"}
---

Los logs son un registro de eventos ocurridos en los sistemas.
Casi todos los sistemas generan logs de algún tipo, los que contienen múltiples entradas detalladas sobre eventos ocurridos u ocurrencias.

Útiles durante la fase de investigación de incidentes, dado que graban 3  de las 4 W (what, where y when - **qué, dónde y cuándo** (la 4ta siendo why - **por qué**)). Esto suele incluir detalles como fecha, hora, lugar, acción realizada, ID de usuario o sistema, etc.

## Análisis de logs
Proceso de examinar dichos logs para identificar eventos de interés. Dada la inmensa cantidad de información que podríamos registrar, es importante ser selectivo en **qué** logeamos.
Por ejemplo, una aplicación web genera un volumen enorme de información, pero no toda esa información podría ser relevante para una investigación; es más esto podría entorpecer la investigación.
**Excluir información reduce el tiempo de investigación**

Las [[Ciberseguridad/Habilidades y conocimientos básicos/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SIEM\|herramientas SIEM]] proveen mucha información de alto-nivel sobre lo que ocurre en una red. Esto lo realiza recolectando información de multiples fuentes, es consolidada en un solo lugar y por último es normalizada o convertida a un formato preferido.
De esta forma, ayudan a procesar dichos logs en tiempo real.

### Recopilación
Los direccionadores de logs ayudan a recolectarlos de varias fuentes y enviarlos a un repositorio común para almacenamiento.
Diversos sistemas y dispositivos generan diversos logs; Como las [[wip folder/Ciclo de Red\|Redes]] que generan logs sobre [[Proxies\|Proxies]], [[Ciberseguridad/Conexiones/Arquitectura de Red#6. Enrutadores (Routers)\|Routers]], [[Ciberseguridad/Conexiones/Arquitectura de Red#5. Hubs y Switches\|Switches]], [[Ciberseguridad/Conexiones/Arquitectura de Red#3. Cortafuegos (Firewalls)\|Firewalls]], etc. O los [[IT fundamentos/Sistemas Operativos\|Sistemas Operativos]], las aplicaciones o software, logs de seguridad elaborados por [[Ciberseguridad/Habilidades y conocimientos básicos/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#IDS (Sistema de Detección de Intrusiones)\|Sistemas de detección de intrusiones]] y [[Ciberseguridad/Habilidades y conocimientos básicos/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#IPS (Sistema de Prevención de Intrusiones)\|Sistemas de prevención de intrusiones]], y finalmente logs de [[Ciberseguridad/Habilidades y conocimientos básicos/Controles de acceso#Autenticación\|Autenticación]] que registran los intentos de log-in.

## Buenas prácticas

Importante entender cómo recopilar, almacenar y proteger los registros ya que son parte integral de la investigación.
La gestión de registros es el proceso de recopilar, almacenar, analizar y eliminar datos del registro.

**Qué registrar** es quizás la tarea más importante, un registro excesivo ralentiza las investigaciones, podría contener información de identificación personal ( ==PII== ), etc. Lo importante es configurar para obtener sólo lo estrictamente necesario según la organización.
Si bien registrar todo es tentativo y podría ser útil, los costos se empiezan a acumular rápidamente en sistemas complejos, tanto en rendimiento como en almacenamiento.

Algunas empresas trabajan con regulaciones determinadas por la industria. Por ej. ciertas normativas exigen que las empresas retengan registros durante un período determinado.
Tenemos industrias como el sector público, atención médica y servicios financieros que tienen estos estándares.
Algunos ejemplos de estas normativas son por ejemplo [[wip folder/Otras normativas\|HIPAA, PCI DSS, etc]].

**Proteger los registros** es importante ya que los atacantes pueden modificar estos registros, eliminar otros y así engañar a los equipos.
