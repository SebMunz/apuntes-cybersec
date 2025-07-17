---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)/"}
---

# Índice

1. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#Crear VM Windows Server\|#Crear VM Windows Server]]
2. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#Crear VM\|#Crear VM]]
3. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#Instalar Wazuh\|#Instalar Wazuh]]
	1. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#En Ubuntu\|#En Ubuntu]]
	2. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#En WinServer\|#En WinServer]]
4. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#Configuración de Agente\|#Configuración de Agente]]
5. [[Ciberseguridad/Prácticas/SIEM con Wazuh (Win & Linux)#Verificación\|#Verificación]]
---

# Crear VM Windows Server

Primero descargamos la ISO de Windows server 2022 <a href="https://www.microsoft.com/es-es/evalcenter/evaluate-windows-server-2022">desde el sitio oficial</a>
y procedemos a su instalación a través de Oracle's VirtualBox

```
nombre: WinServ22
RAM: >=4gb
Espacio: 50gb dinámico
Red: Puente <- Importante
Edición: Desktop Experience <- Para GUI, pero podría ser sin ella
```
![](https://i.imgur.com/StG9Zn4.png)


---

# Crear VM

Similar con win server, descargamos el iso  y realizamos instalación.
```
nombre: UbuntuServ
Ram: >=2gb
Espacio: 20gb dinámico
Red: Puente, la misma que Win
Edición: -
```
![](https://i.imgur.com/oc6pUmU.png)

---
# Instalar Wazuh

<a href='https://wazuh.com/'>Wazuh</a> es un [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR XDR#SIEM\|SIEM]] y [[Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Ciclo de vida de un incidente/05 IDS IPS EDR SIEM SOAR XDR#EDR (Detección y Respuesta de Puntos de Conexión)\|XDR]] open source.

## En Ubuntu

Lo primero es descargar Wazuh según las instrucciones que nos proveen:
```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```
![](https://i.imgur.com/2vw2rwW.png)

Cuando termina, nos enseña el usuario y la contraseña
asdf

>Para leer todas las contraseñas podemos usar el siguiente comando:
```bash
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

Podemos comprobar su existencia accediendo al dashboard con nuestra IP y entrando al puerto 443
![](https://i.imgur.com/ccvDPqr.png)

>asegurarnos de que los puertos que utiliza no esten bloqueados por firewall
>443, 5601, 55000, 1514, 1515

## En WinServer

Descargamos el agente como se nos menciona y guía <a href="https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html">en su sitio</a>. También nos explica para qué es:
> El agente corre en el endpoint que quieres monitorear y se comunica con el servidor Wazuh, enviando datos en tiempo casi-real a través de un canal encriptado y autenticado.

Instalarlo es sencillo con GUI, simplemente se descarga el msi, se instala de forma normal, al ejecutarlo vemos esto:
![](https://i.imgur.com/cOOyPZz.png)

Desde esa misma parte podemos acceder a logs y otras consultas a través del menú "manage"

---
# Configuración de Agente

<a href="https://documentation.wazuh.com/current/user-manual/agent/agent-enrollment/enrollment-methods/via-agent-configuration/windows-endpoint.html">En su documentación podemos encontrar el método para configurar el agente</a>
En resumidas cuentas:
Debemos ir a `C:\Program Files (x86)\ossec-agent\ossec.conf`
abrirlo y configurar lo siguiente
```xml
<client>
  <server>
	<!-- cambiar por la IP del wazuh manager> -->
    <address><WAZUH_MANAGER_IP_ADDRESS></address>    ...
  </server>
</client>
```

En el mismo Wazuh dashboard podemos agregar un agente. Al realizar esto, nos proporcionará una authkey para insertarla.

Otras formas alternativas incluyen el comando CMD


Reiniciamos el servicio
```powershell
Restart-Service -Name Wazuh
```



---

# Conclusión

Primero intenté hacerlo en Fedora, avanzó bien en un principio pero al no tener configurada una IP fija en la máquina, ésta murió completamente y la API key falló. La solución era simplemente irme a los archivos de Wazuh en Fedora, ver la key y configurar desde ahí, pero por una cosa de tiempo decidí hacerlo en ubuntu.

Definitivamente era más sencillo hacerlo con uno de los SO recomendados por Wazuh (Amazon Linux, CentOS, **Ubuntu** o Red Hat), dichos fallos son más escasos.