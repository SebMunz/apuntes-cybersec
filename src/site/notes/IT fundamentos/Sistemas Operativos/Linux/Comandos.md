---
{"dg-publish":true,"permalink":"/IT fundamentos/Sistemas Operativos/Linux/Comandos/"}
---

Listado de comandos linux que he utilizado

1. **ls**
   - Lista archivos y directorios.
   - `ls -l`

2. **cd**
   - Cambia de directorio.
   - `cd /home`

3. **pwd**
   - Muestra el directorio actual.
   - `pwd`

4. **cp**
   - Copia archivos o directorios.
   - `cp archivo.txt /destino/`

5. **mv**
   - Mueve o renombra archivos/directorios.
   - `mv archivo.txt nuevo_nombre.txt`

6. **rm**
   - Elimina archivos o directorios.
   - `rm archivo.txt`

7. **mkdir**
   - Crea un directorio.
   - `mkdir nueva_carpeta`

8. **rmdir**
   - Elimina un directorio vacío.
   - `rmdir carpeta_vacia`

9. **touch**
   - Crea un archivo vacío.
   - `touch archivo.txt`

10. **cat**
    - Muestra el contenido de un archivo.
    - `cat archivo.txt`

11. **less**
    - Muestra el contenido de un archivo, página por página.
    - `less archivo.txt`

12. **more**
    - Similar a `less`, pero menos funcional.
    - `more archivo.txt`

13. **head**
    - Muestra las primeras líneas de un archivo.
    - `head archivo.txt`

14. **tail**
    - Muestra las últimas líneas de un archivo.
    - `tail archivo.txt`

15. **echo**
    - Imprime texto en la terminal.
    - `echo "Hola, mundo"`

16. **find**
    - Busca archivos en el sistema.
    - `find / -name archivo.txt`

17. **grep**
    - Busca texto dentro de archivos.
    - `grep "error" archivo.log`

18. **man**
    - Muestra el manual de un comando.
    - `man ls`

19. **chmod**
    - Cambia permisos de archivos o directorios.
    - `chmod 755 archivo.txt`

20. **chown**
    - Cambia el propietario de un archivo o directorio.
    - `chown usuario:grupo archivo.txt`

21. **ps**
    - Muestra procesos en ejecución.
    - `ps aux`

22. **top**
    - Muestra procesos en tiempo real.
    - `top`

23. **htop**
    - Alternativa mejorada a `top`.
    - `htop`

24. **kill**
    - Finaliza un proceso por su PID.
    - `kill 1234`

25. **killall**
    - Finaliza procesos por nombre.
    - `killall firefox`

26. **df**
    - Muestra el uso del sistema de archivos.
    - `df -h`

27. **du**
    - Muestra el tamaño de directorios y archivos.
    - `du -sh /ruta`

28. **tar**
    - Comprime y descomprime archivos.
    - `tar -czvf archivo.tar.gz /ruta`

29. **zip**
    - Comprime archivos en formato ZIP.
    - `zip archivo.zip archivo.txt`

30. **unzip**
    - Extrae archivos ZIP.
    - `unzip archivo.zip`

31. **wget**
    - Descarga archivos de internet.
    - `wget http://ejemplo.com/archivo.zip`

32. **curl**
    - Hace solicitudes HTTP.
    - `curl http://ejemplo.com`

33. **scp**
    - Copia archivos entre sistemas vía SSH.
    - `scp archivo.txt usuario@servidor:/ruta`

34. **rsync**
    - Sincroniza archivos/directorios.
    - `rsync -av /origen /destino`

35. **ssh**
    - Accede a servidores vía SSH.
    - `ssh usuario@servidor`

36. **nano**
    - Editor de texto simple.
    - `nano archivo.txt`

37. **vim**
    - Editor de texto avanzado.
    - `vim archivo.txt`

38. **apt**
    - Gestiona paquetes en sistemas Debian/Ubuntu.
    - `apt update && apt upgrade`

39. **yum**
    - Gestiona paquetes en sistemas Red Hat.
    - `yum install paquete`

40. **dnf**
    - Nuevo gestor de paquetes en Red Hat/Fedora.
    - `dnf install paquete`

41. **pacman**
    - Gestor de paquetes de Arch Linux.
    - `pacman -S paquete`

42. **alias**
    - Crea alias para comandos.
    - `alias ll='ls -la'`

43. **unalias**
    - Elimina un alias.
    - `unalias ll`

44. **history**
    - Muestra el historial de comandos.
    - `history`

45. **clear**
    - Limpia la pantalla de la terminal.
    - `clear`

46. **uptime**
    - Muestra tiempo de actividad del sistema.
    - `uptime`

47. **whoami**
    - Muestra el usuario actual.
    - `whoami`

48. **uname**
    - Muestra información del sistema.
    - `uname -a`

49. **hostname**
    - Muestra o cambia el nombre del sistema.
    - `hostname`

50. **env**
    - Muestra las variables de entorno.
    - `env`

51. **export**
    - Define variables de entorno.
    - `export VAR=valor`

52. **printenv**
    - Muestra una variable de entorno.
    - `printenv PATH`

53. **date**
    - Muestra o establece la fecha y hora.
    - `date`

54. **cal**
    - Muestra un calendario.
    - `cal`

55. **bc**
    - Calculadora en línea de comandos.
    - `echo "5+5" | bc`

56. **mount**
    - Monta sistemas de archivos.
    - `mount /dev/sda1 /mnt`

57. **umount**
    - Desmonta sistemas de archivos.
    - `umount /mnt`

58. **lsblk**
    - Muestra dispositivos de bloques.
    - `lsblk`

59. **blkid**
    - Muestra UUIDs de sistemas de archivos.
    - `blkid`

60. **fdisk**
    - Gestiona particiones de disco.
    - `fdisk /dev/sda`

61. **mkfs**
    - Formatea sistemas de archivos.
    - `mkfs.ext4 /dev/sda1`

62. **fsck**
    - Verifica y repara sistemas de archivos.
    - `fsck /dev/sda1`

63. **crontab**
    - Configura tareas programadas.
    - `crontab -e`

64. **at**
    - Programa tareas para ejecutarse una vez.
    - `echo "comando" | at 14:00`

65. **systemctl**
    - Gestiona servicios en sistemas modernos.
    - `systemctl status ssh`

66. **service**
    - Gestiona servicios en sistemas antiguos.
    - `service ssh status`

67. **journalctl**
    - Muestra logs del sistema.
    - `journalctl -xe`

68. **dmesg**
    - Muestra mensajes del kernel.
    - `dmesg`

69. **ip**
    - Configura interfaces de red.
    - `ip a`

70. **ifconfig**
    - Configura interfaces de red (obsoleto).
    - `ifconfig`

71. **ping**
    - Verifica conectividad de red.
    - `ping google.com`

72. **netstat**
    - Muestra conexiones de red.
    - `netstat -tuln`

73. **ss**
    - Alternativa moderna a `netstat`.
    - `ss -tuln`

74. **traceroute**
    - Rastrea rutas de red.
    - `traceroute google.com`

75. **iptables**
    - Configura reglas de firewall.
    - `iptables -L`

76. **firewalld**
    - Gestiona firewalls en sistemas modernos.
    - `firewall-cmd --list-all`

77. **ufw**
    - Firewall simple para Ubuntu.
    - `ufw enable`

78. **gzip**
    - Comprime archivos.
    - `gzip archivo.txt`

79. **gunzip**
    - Descomprime archivos.
    - `gunzip archivo.txt.gz`

80. **xz**
    - Comprime con mayor eficiencia.
    - `xz archivo.txt`

81. **unxz**
    - Descomprime archivos xz.
    - `unxz archivo.txt.xz`

82. **awk**
    - Procesa texto.
    - `awk '{print $1}' archivo.txt`

83. **sed**
    - Edita texto en línea de comandos.
    - `sed 's/viejo/nuevo/g' archivo.txt`

84. **cut**
    - Corta columnas de texto.
    - `cut -d',' -f1 archivo.csv`

85. **sort**
    - Ordena líneas de texto.
    - `sort archivo.txt`

86. **uniq**
    - Elimina duplicados.
    - `uniq archivo.txt`

87. **wc**
    - Cuenta líneas, palabras y caracteres.
    - `wc -l archivo.txt`

88. **diff**
    - Compara diferencias entre archivos.
    - `diff archivo1.txt archivo2.txt`

89. **cmp**
    - Compara archivos binarios.
    - `cmp archivo1 archivo2`

90. **tee**
    - Redirige y guarda salida estándar.
    - `echo "Texto" | tee archivo.txt`

91. **xargs**
    - Construye argumentos desde entrada.
    - `echo archivo.txt | xargs rm`

92. **jobs**
    - Lista trabajos en segundo plano.
    - `jobs`

93. **fg**
    - Trae un trabajo al primer plano.
    - `fg %1`

94. **bg**
    - Envía un trabajo al fondo.
    - `bg %1`

95. **ln**
    - Crea enlaces entre archivos.
    - `ln -s archivo_origen enlace_simbolico`

96. **sudo**
    - Ejecuta comandos con privilegios elevados.
    - `sudo apt update`

97. **useradd**
    - Agrega un nuevo usuario.
    - `useradd -m -s /bin/bash nuevo_usuario`

98. **groupadd**
    - Crea un nuevo grupo.
    - `groupadd -g 1001 nuevo_grupo`

99. **usermod**
    - Modifica un usuario existente.
    - `usermod -aG sudo usuario`

100. **groups**
     - Lista los grupos a los que pertenece un usuario.
     - `groups usuario`

101. **id**
     - Muestra información detallada sobre el usuario.
     - `id usuario`

102. **pstree**
     - Muestra procesos en formato de árbol.
     - `pstree`

103. **sudo apt install apache2 -y**
     - Instala Apache2 sin solicitar confirmación.
     - `sudo apt install apache2 -y`

104. **sudo systemctl status apache2**
     - Verifica el estado del servicio Apache2.
     - `sudo systemctl status apache2`

105. **sudo nano /etc/apache2/apache2.conf**
     - Edita el archivo de configuración de Apache2.
     - `sudo nano /etc/apache2/apache2.conf`

106. **sudo apachectl configtest**
     - Prueba la configuración de Apache2.
     - `sudo apachectl configtest`

107. **sudo tee /var/www/html/index.html**
     - Escribe contenido en el archivo index.html de Apache.
     - `echo "<html><body><h1>Hola</h1></body></html>" | sudo tee /var/www/html/index.html`

108. **sudo apt install isc-dhcp-server -y**
     - Instala el servidor DHCP.
     - `sudo apt install isc-dhcp-server -y`

109. **sudo nano /etc/dhcp/dhcpd.conf**
     - Edita la configuración del servidor DHCP.
     - `sudo nano /etc/dhcp/dhcpd.conf`

110. **sudo systemctl restart isc-dhcp-server**
     - Reinicia el servicio DHCP.
     - `sudo systemctl restart isc-dhcp-server`

111. **sudo systemctl status isc-dhcp-server**
     - Verifica el estado del servidor DHCP.
     - `sudo systemctl status isc-dhcp-server`

112. **journalctl -ex**
     - Revisa los logs del sistema con información extendida.
     - `journalctl -ex`

113. **sudo apt install vsftpd -y**
     - Instala el daemon FTP vsftpd.
     - `sudo apt install vsftpd -y`

114. **sudo nano /etc/vsftpd.conf**
     - Edita la configuración de vsftpd.
     - `sudo nano /etc/vsftpd.conf`

115. **sudo systemctl restart vsftpd.service**
     - Reinicia el servicio vsftpd.
     - `sudo systemctl restart vsftpd.service`

116. **chown**
     - Cambia el propietario de un archivo o directorio.
     - `chown usuario:grupo archivo.txt`

117. **sudo apt install openssh-server -y**
     - Instala el servidor SSH.
     - `sudo apt install openssh-server -y`

118. **sudo nano /etc/ssh/sshd_config**
     - Edita la configuración del servidor SSH.
     - `sudo nano /etc/ssh/sshd_config`

119. **ssh-keygen -t rsa -b 4096**
     - Genera llaves SSH.
     - `ssh-keygen -t rsa -b 4096`

120. **sudo fdisk -l**
     - Lista discos y particiones.
     - `sudo fdisk -l`

121. **sudo fdisk /dev/sda**
     - Gestiona particiones en /dev/sda.
     - `sudo fdisk /dev/sda`

122. **sudo mkfs.ext4 /dev/sdX1**
     - Formatea una partición con ext4.
     - `sudo mkfs.ext4 /dev/sdX1`

123. **sudo mkdir /mnt/nuevo_almacenamiento**
     - Crea un nuevo punto de montaje.
     - `sudo mkdir /mnt/nuevo_almacenamiento`

124. **sudo mount /dev/sdX1 /mnt/nuevo_almacenamiento**
     - Monta una partición en el punto especificado.
     - `sudo mount /dev/sdX1 /mnt/nuevo_almacenamiento`

125. **sudo blkid /dev/sdb1**
     - Obtiene el UUID de una partición.
     - `sudo blkid /dev/sdb1`

126. **sudo nano /etc/fstab**
     - Edita el archivo de configuración de sistemas de archivos.
     - `sudo nano /etc/fstab`

127. **sudo umount /mnt/nuevo_almacenamiento**
     - Desmonta una partición.
     - `sudo umount /mnt/nuevo_almacenamiento`

128. **sudo mount -a**
     - Monta todas las particiones definidas en fstab.
     - `sudo mount -a`

129. **sudo systemctl daemon-reload**
     - Recarga los demonios del sistema.
     - `sudo systemctl daemon-reload`

130. **sudo apt-get install lvm2 -y**
     - Instala LVM.
     - `sudo apt-get install lvm2 -y`

131. **sudo pvcreate /dev/sdb1 /dev/sdc2**
     - Crea volúmenes físicos para LVM.
     - `sudo pvcreate /dev/sdb1 /dev/sdc2`

132. **sudo vgcreate vgrupo1 /dev/sdb1 /dev/sdc1**
     - Crea un grupo de volúmenes.
     - `sudo vgcreate vgrupo1 /dev/sdb1 /dev/sdc1`

133. **sudo vgdisplay**
     - Muestra información de grupos de volúmenes.
     - `sudo vgdisplay`

134. **sudo lvcreate -n volumen1 -L 5.99G vgrupo1**
     - Crea un volumen lógico.
     - `sudo lvcreate -n volumen1 -L 5.99G vgrupo1`

135. **sudo mkfs.ext4 /dev/vgrupo1/volumen1**
     - Formatea un volumen lógico.
     - `sudo mkfs.ext4 /dev/vgrupo1/volumen1`

136. **sudo lvextend -L +tamaño /dev/vgrupo1/volumen1**
     - Extiende el tamaño de un volumen lógico.
     - `sudo lvextend -L +10G /dev/vgrupo1/volumen1`

137. **sudo resize2fs /dev/vgrupo1/volumen1**
     - Redimensiona el sistema de archivos.
     - `sudo resize2fs /dev/vgrupo1/volumen1`

138. **sudo lvreduce -L NUEVO_TAMAÑO /dev/vgrupo1/volumen1**
     - Reduce el tamaño de un volumen lógico.
     - `sudo lvreduce -L 5G /dev/vgrupo1/volumen1`