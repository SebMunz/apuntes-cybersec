---
{"dg-publish":true,"permalink":"/Ciberseguridad/Ataques/SQL Injection/"}
---

# SQL Injection

El **SQL Injection** es un ataque que envía consultas SQL maliciosas a la base de datos. Este tipo de inyección ocurre en áreas del sitio web diseñadas para aceptar entradas de usuario, como formularios de inicio de sesión o cualquier sección que interactúe con la base de datos. La vulnerabilidad radica en que lo que se ingresa en el campo de entrada se copia directamente en la consulta SQL.

Los ataques de SQL Injection permiten a un atacante insertar declaraciones maliciosas en la consulta SQL, lo que les da acceso indebido a la base de datos. Esto puede resultar en la modificación de tablas, eliminación de información o inserción de datos no autorizados.

## Sanitización y Solución

La solución fundamental es sanitizar las entradas, y una técnica eficaz para lograrlo son los "***prepared statements***".

### Prepared Statements

Los **Prepared Statements** son técnicas que implican ejecutar el código antes de pasarlo a la base de datos. Esto garantiza la sanitización de los inputs al validar la información antes de ser utilizada en una consulta SQL. Al emplear prepared statements, se reduce significativamente la posibilidad de inyecciones SQL, ya que el motor de base de datos trata las consultas y los datos por separado.

---