---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/Introduction to Agent Assist and its GenAi Capabilities/01 Customer engagement Suite architecture (CES)/"}
---

Lo primero es saber una diferencia en la arquitectura cloud:


| <center>Projectos</center>                                                                                                                                                                                        | <center>Conversational Agents</center>                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Colección lógica de recursos cloud que delegan los mismos IAM a cada recurso                                                                                                                                      | Colección lógica de interacciones que están enfocados a un tipo particular de end-user                                                                                                              |
| Para CES:<br>1 projecto conteniendo todos los recursos CES que no sean de producción (con entorno dev y de pruebas)<br>- 1 projecto conteniendo todos los recursos CES de producción (entorno stage y producción) | - Un agente conversacional tiene entornos internos, asi que usualmente sólo 1 por proyecto<br>- Si tienen distintos grupos de usuario o equipos dev, usa proyectos separados para control de acceso |
![](https://i.imgur.com/Rz5pxGJ.png)


