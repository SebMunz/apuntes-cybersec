---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Prompt Framework/"}
---

Parte de la creación de buenos prompts es utilizar -y reutilizar- frameworks que creemos para distintos propósitos.

Google nos presenta con **T.C.R.E.I.** o *Task, Context, References, Evaluate, Iterate* (Tarea, Contexto, Referencias, Evaluación, Iteración)

# Task

Presentarle al modelo la tarea que debe realizar.
Se recomienda otorgarle una *persona*, lo cual le dará una parte del contexto de cómo debe responder.

> Eres un adulto promedio de 30 años que quiere hacerle un regalo a su amigo de la infancia.

También es útil darle en esta parte *a quién le responde*

>Actuarás como yo, por lo tanto háblame en primera persona como si fuera yo

También puedes darle el output o formato deseado... una presentación que incluya tablas. Una lista. Un código. En léxico culto formal, etc.
> Dame la respuesta en una lista
# Context

Darle los detalles necesarios para que realice su tarea o qué debe hacer.
> Mi amigo es un hombre joven de 30 años, le gustan los deportes, los gatos y los videojuegos.

**Tip:** usar delimitadores como etiquetas [[Fundamentos TI/XML\|XML]].
# References

Entregarle referencias sobre las cuales trabajar
>En el pasado le he regalado una tarjeta gráfica, juguetes para gatos y ropa deportiva para el gimnasio

# Evaluate

¿Te ha dado el modelo una buena respuesta?

> Eres un adulto promedio de 30 años que quiere hacerle un regalo a su amigo de la infancia. Actuarás como yo, por lo tanto háblame en primera persona como si fuera yo. Dame la respuesta en una lista. Mi amigo es un hombre joven de 30 años, le gustan los deportes, los gatos y los videojuegos.
> En el pasado le he regalado una tarjeta gráfica, juguetes para gatos y ropa deportiva para el gimnasio y mi presupuesto es de 50 mil pesos chilenos.

# Iterate

Según lo anterior, repetimos el proceso. Nos preguntamos dónde falló... Fue en la tarea? el contexto? quizás puedo darle más referencias?.

> Quiero que me des nuevas ideas pero esta vez hazlo en una tabla comparativa donde entregues el costo del regalo y algún link al producto o implementación de la idea como referencia.

---

A grandes rasgos...

Lo importante es darle la mayor cantidad de información posible. SIEMPRE hay que recordar que la inteligencia artificial no es como usualmente se cree.

La IA sólo "predice" lo que debería ir o decir en el texto, sin embargo, no está realmente *entendiendo* lo que hace. Y es ahí donde la mayoría cae.