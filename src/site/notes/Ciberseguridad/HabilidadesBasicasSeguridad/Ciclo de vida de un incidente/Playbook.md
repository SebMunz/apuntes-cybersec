---
{"dg-publish":true,"permalink":"/Ciberseguridad/HabilidadesBasicasSeguridad/Ciclo de vida de un incidente/Playbook/"}
---

Su funcionamiento es para ayudar a dirigir el la respuesta al [[01 Introducción \| Ciclo de vida de incidentes]]
Proveen de una estructura y un orden para *qué acciones* tomar de manera efectiva y rápida.

Siguiendo el playbook, se puede reducir el tiempo de respuesta, la incertidumbre y el tener que estar adivinando.

Dentro de ellos, tenemos los pasos necesarios para responder a un ataque como [[Ciberseguridad/Ataques/Malware#4. Ransomware \| Ransomware]], [[Ciberseguridad/Ataques/Malware#12. Data breach \| Data Breach]], [[Ciberseguridad/Ataques/Malware\|Malware]] en general o incluso [[Red \| Ataques de red]].
![Pasted image 20240724120755.png](/img/user/Pasted%20image%2020240724120755.png)Ejemplo de un flowchart que podríamos encontrar en un playbook (simplificado).

## Tipos de Playbook
Tenemos 3 tipos de playbooks:
- Automatizado
- No Automatizado (Manual)
- Semi-automatizado

### Automatizado
Los automatizados, como dice su nombre, se automatizan ciertas tareas de los procesos de respuesta de incidentes. Por ejemplo categorizar la severidad de un incidente, juntar evidencia, ordenar logs, etc. Las herramientas [[Ciberseguridad/HabilidadesBasicasSeguridad/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SOAR \| SOAR]] y [[Ciberseguridad/HabilidadesBasicasSeguridad/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR#SIEM \| SIEM]] pueden configurarse para automatizar estas tareas.

### No automatizado
Su nombre es descriptivo, sólo incluye tareas que deben ser realizadas de forma manual

### Semi automatizado
Combinan acciones manuales con la automatización. Tareas tediosas, tareas que pueden contener errores humanos como juntar evidencia y registros, pueden ser automáticas. Los analistas pueden priorizar su tiempo con otras tareas que requieran la atención humana.

---
Para finalizar, los playbook deben estar en constante cambio ya que las amenazas evolucionan, se pueden encontrar formas más efectivas de realizar ciertas operaciones, etc.
La mejor etapa para actualizar los playbooks es en la fase post-actividad