---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux/"}
---

Vamos a realizar un hardening básico de servidor en Ubuntu.
Si bien esto nos ayudará a tenerlo más controlado, es sólo una primera capa de defensa.

---

# Índice
1. [[#Remover root]]
2. [[#Certificación SSH]]
3. [[#Deshabilitar contraseña para SSH]]
4. [[#Cambiar puerto de conexión por defecto]]
5. [[#Pruebas de conexión con certificado]]
6. [[#Recomendaciones de hardening adicionales]]
7. [[#Conclusiones]]
<div class="page-break" style="page-break-before: always;"></div>

---
# Remover root

Pros
- Evita el acceso directo a Super Usuario
- Obliga a usar un usuario menos privilegiado
- Reduce el riesgo de daños en caso de que la cuenta sea comprometida
Cons
- Puede llegar a ser menos conveniente si es que necesitamos acceder como root directamente

Debemos primero editar el archivo de configuración SSH
`sudo nano /etc/ssh/sshd_config`
![](https://i.imgur.com/5DfzoxL.png)

Buscar la linea `PermitRootLogin` y cambiarla a `no` (nota: eliminar el # del comentario)
![](https://i.imgur.com/ArcyVVV.png)

Guardar y reiniciar el servicio
`sudo service ssh restart`
![](https://i.imgur.com/eDc05oj.png)

<div class="page-break" style="page-break-before: always;"></div>

---
# Certificación SSH

Pros
- Más seguro que usar contraseñas
- Claves virtualmente imposible de adivinar por fuerza bruta
- Simplifica inicio de sesión al no necesitar gestionar la contraseña nosotros mismos
Cons
- Si se expone la clave privada de alguna forma, vulneramos nuestra conexión
- Configuración inicial no es tan sencilla para usuarios comunes

Crear un par de claves SSH (privada y pública)
`ssh-keygen -t rsa -b 4096 -C "correo@example.com"`
Para la ubicación lo ideal es por defecto para facilitar su búsqueda pero también se puede considerar una medida de seguridad dejarla en otro sitio.
![](https://i.imgur.com/Ul9cvV5.png)

La pública se guarda en `~/.ssh/id_rsa.pub`
La privada en `~/.ssh/id_rsa`
![](https://i.imgur.com/1imN0PW.png)

<div class="page-break" style="page-break-before: always;"></div>

---
# Deshabilitar contraseña para SSH

Pros
- Evita los ataques de fuerza bruta
- Facilita el acceso automático en procesos (o scripts)

Cons
- Si se expone la clave privada, el acceso total está comprometido
- Dificulta la recuperación en caso de olvido o pérdida de la clave privada

Asegurarnos de copiar la clave pública (en este caso será local)
`ssh-copy-id nombreUsuario@localhost`
![](https://i.imgur.com/Ss554ZD.png)

Editamos el archivo de configuración SSH nuevamente
`sudo nano /etc/ssh/sshd_config`
Esta vez cambiamos lo siguiente:
```
PasswordAuthentication no
ChallengeResponseAuthentication no
```
![](https://i.imgur.com/Bp9yjaN.png)
(nota: eliminar el # del comentario)

Reiniciamos nuevamente el servicio
<div class="page-break" style="page-break-before: always;"></div>

---
# Cambiar puerto de conexión por defecto

Pros
- Disminuye los riesgos de ataques automáticos dirigidos al puerto por defecto (22)
- Reduce la probabilidad de escaneos de puertos malintencionados
Cons
- Administradores deben gestionar el nuevo puerto
- No es una protección sólida, solo es una medida disuasiva

En el mismo archivo de configuración SSH buscamos la línea `Port 22`
y la cambiamos por otro número que nos convenga y no haga conflicto, por ejemplo el 2222
![](https://i.imgur.com/fddry9s.png)

Reiniciamos el servicio
<div class="page-break" style="page-break-before: always;"></div>

---
# Pruebas de conexión con certificado

Pros
- Asegurarse de que la configuración es correcta antes de su implementación en producción
Cons
- Si no las realizamos de manera correcta, puede generar una falsa sensación de seguridad

Primero una prueba ssh directa como root:
`ssh -p 2222 root@localhost`
![](https://i.imgur.com/cIsiY5r.png)
Se nos niega el acceso.

Luego, una prueba de ingreso sin certificación:
`ssh otroUsuario@localhost -p 2222`
![](https://i.imgur.com/Qg9gBQ7.png)

Y ahora una prueba con el certificado explícito
![](https://i.imgur.com/1qiRXUw.png)

Desde windows, podemos utilizar este comando para copiar la clave pública directamente:
```
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh floure@localhost -p 2222 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
Como podemos ver, todo está bajo control.
<div class="page-break" style="page-break-before: always;"></div>

---
# Recomendaciones de hardening adicionales

**Desactivar el acceso de usuarios no autorizados**
- Menos usuarios con acceso = menos posibilidades de acceso no autorizado

**Limitar intentos de conexión fallidos (fail2ban)**
- Protege contra fuerza bruta limitando la cantidad de intentos fallidos permitidos

**Usar VPN para acceder**
- Encripta el tráfico y mejora la privacidad, restringe acceso a solo aquellos en la red privada

**Configurar 2FA**
- Requiere algo que el atacante no puede obtener fácilmente

**Parches de seguridad**
Quizás suena redundante pero es uno de los más importantes y dificultosos. Requiere de tiempo, pruebas adicionales y afinar detalles diversos.
Parchar la seguridad es como arreglar un bote con agujeros constantemente. Cada vez que tapas un agujero, encuentras otro. Es una tarea de nunca acabar.
Realizar estos parches es necesario y siempre ayuda, sin embargo un parche mal aplicado (o incluso de manera apresurada), puede provocar problemas de compatibilidad o fallos no previstos.

# Conclusiones

El hardening es una práctica que DEBE realizarse, mejorarse y monitorear constantemente. Si bien es una barrera de defensa importante, no debemos quedarnos con sólo una. La defensa debe realizarse en capas, como los ogros.

Un hardening incorrecto puede también traernos diversos problemas, es así como siempre debemos balancear las ventajas y desventajas de los mismos. Podríamos llegar a interrumpir sistemas, causar conflictos con nuestras propias herramientas, levantar falsos positivos constantemente, etc.

En Windows, el proceso [[Fundamentos TI/Sistemas Operativos/Windows/Hardening básico en Windows\|es muy similar, si no igual, con algunas cosas distintas que podemos realizar]].
