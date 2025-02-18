---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Windows/Hardening básico en Windows/"}
---

Así como en mi pequeña guía de [[Fundamentos TI/Sistemas Operativos/Linux/Hardening Linux\|Hardening Linux]], esto es **EXACTAMENTE IGUAL**.

Diferencias sustanciales:
- Debemos instalar el servidor SSH
- Utilizamos los mismos archivos de configuración, sólo que están en `C:\ProgramData\ssh\`
- El comando para reiniciar el servidor con PowerShell es `Restart-Service sshd`
- Se recomienda actualizar las reglas del firewall:
``` powershell
New-NetFirewallRule -Name "nuevo puerto SSH" -DisplayName "SSH 2222" -Protocol TCP -LocalPort 2222 -Action Allow
```

---

# Recomendaciones adicionales

- Utilizar y configurar Windows Defender Firewall
- Utilizar BitLocker para el cifrado de discos
- Deshabilitar SMBv1 para evitar exploits como WannaCry
- Configurar políticas de contraseñas con `gpedit.msc`
- Habilitar UAC en su nivel ideal para el uso que le vamos a dar
- Principio del mínimo privilegio
- Habilitar registros avanzados en el Visor de eventos
- Deshabilitar servicios que no serán usados como por ejemplo telnet o RDP
- LSA Protection
- ASR
- Forzar TLS1.2, etc.

Las recomendaciones, al igual que en Linux, son similares. Debemos buscar el balance ideal entre funcionalidad y seguridad.
