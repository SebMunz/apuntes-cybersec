---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 3 - Reglas/"}
---

# Índice

1. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 3 - Reglas#Política de Contraseña mínimo 3 mayúsculas\|#Política de Contraseña mínimo 3 mayúsculas]]
2. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 3 - Reglas#Política de Contraseña 3 números y 2 intentos fallidos\|#Política de Contraseña 3 números y 2 intentos fallidos]]
3. [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 3 - Reglas#SSH\|#SSH]]
<div class="page-break" style="page-break-before: always;"></div>

---

# Política de Contraseña: mínimo 3 mayúsculas

Aplicaremos una política que exija al menos 3 mayúsculas.
En Ubuntu deberiamos tener el archivo `/etc/security/pwquality.conf`

Si no lo tenemos, quiere decir que no estamos forzando ningún tipo de política, por lo tanto debemos instalar el módulo PAM (*Pluggable Authentication Modules*).

`sudo apt-get update`
`sudo apt-get install libpam-pwquality`

Antes
![](https://i.imgur.com/PO8vPs9.png)

Despues
![](https://i.imgur.com/1JmxCno.png)

Los pasos son los siguientes:
1. Abrir el archivo
`sudo nano /etc/security/pwquality.conf`

2. Agregar o editar una línea en específico
`ucredit=-3`
![](https://i.imgur.com/QgTG0X2.png)
Con esto forzamos que sean *al menos* 3 mayúsculas

3. Guardar y cerrar
4. Probar:
`passwd <usuario>`
![](https://i.imgur.com/keztiWe.png)
nota por si se me olvida: **USUARIO123**
<div class="page-break" style="page-break-before: always;"></div>

---
# Política de Contraseña: 3 números y 2 intentos fallidos

1. Volvemos al mismo archivo:
`sudo nano /etc/security/pwquality.conf`

2. Agregamos o modificamos la línea
`dcredit = -3`
![](https://i.imgur.com/c3UDHpA.png)

3. Con eso tenemos el requisito de 3 números.

Para los 2 intentos debemos ir a otro archivo:
`/etc/pam.d/common-auth`
y agregamos lo siguiente en versiones antiguas de Ubuntu:
![](https://i.imgur.com/bkBchP3.png)
`auth required pam_tally2.so deny=2 unlock_time=10 onerr=fail`

**Importante: verificar qué versión estamos porque en posteriores a 20.04 se usa pam_faillock en vez de pam_tally2**
Como es mi caso, usamos faillock así que lo agregamos de la siguiente forma:
![](https://i.imgur.com/bsJVolV.png)

4. Verificamos:
Contraseña con menos de 3 dígitos
![](https://i.imgur.com/NcoJIGG.png)

Intentos fallidos
![](https://i.imgur.com/lM7Vr5x.png)
nota: usamos faillock para ver los intentos inválidos y validos registrados

<div class="page-break" style="page-break-before: always;"></div>

---

# SSH
Esto es una continuación básicamente de un [[Fundamentos TI/Sistemas Operativos/Linux/Gestión de servicios y almacenamiento en Linux#SSH\|Ejercicio de SSH]] que había realizado previamente así que se asume que el lector tiene acceso a él.

Debemos primero instalar el servidor SSH si no lo está:
`sudo apt update && sudo apt install openssh-server -y`
y verificamos con
`sudo systemctl status ssh`
![](https://i.imgur.com/SlJNxHz.png)
Abrimos el archivo `sudo nano /etc/ssh/sshd_config` y cambiamos la línea del puerto:
![](https://i.imgur.com/X3et55A.png)

Ahora: podemos realizar verificaciones de varias formas pero la más común es:
`sudo netstat -tulnp | grep ":44"`

En mi caso no funciona porque netstat fue reemplazado con `sudo ss -tulnp | grep ":44"`

Sin embargo... dada las configuraciones realizadas en el [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux 2 - IP Tables#Regla para SSH\|ejercicio de Hardening previo]], sólo se aceptan conexiones SSH si es que entran por un puerto específico (el 22). Obviamente tenemos un conflicto porque SSH está ahora en el `:44`. Esto nos lleva a mi [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux#Conclusiones\|conclusión previa]] sobre las configuraciones causando conflicto entre ellas, por lo cual es importante llevar documentación acorde (como esta).

La verdad es que no lo voy a cambiar en este momento, pero a modo gráfico con este pantallazo vemos que la configuración está hecha y activa en el puerto 44:
![](https://i.imgur.com/BACc0Be.png)

<div class="page-break" style="page-break-before: always;"></div>
