---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Windows/Aplicación de GPO en Win Server/"}
---

Para este ejercicio debería utilizar windows server y realizar los cambios de política a través de `gpedit.msc` - Sin embargo, no tengo acceso a él en este momento **PERO** recuerdo perfectamente dónde dirigirse a hacer estos cambios así que daré las instrucciones y haré los cambios en `regedit` en un windows común, para así demostrar que es también posible

# Índice
1. [[Fundamentos TI/Sistemas Operativos/Windows/Aplicación de GPO en Win Server#Quitar opción "Cambiar contraseña" en Ctrl+Alt+Del\|#Quitar opción "Cambiar contraseña" en Ctrl+Alt+Del]]
2. [[Fundamentos TI/Sistemas Operativos/Windows/Aplicación de GPO en Win Server#Desactivar reproducción automática\|#Desactivar reproducción automática]]
3. [[Fundamentos TI/Sistemas Operativos/Windows/Aplicación de GPO en Win Server#Forzar fondo de pantalla\|#Forzar fondo de pantalla]]
4. [[Fundamentos TI/Sistemas Operativos/Windows/Aplicación de GPO en Win Server#Conclusión\|#Conclusión]]

---
# Quitar opción "Cambiar contraseña" en Ctrl+Alt+Del

#### En **GPEdit**:
- Navegar
	`Configuración de Usuario → Plantillas Administrativas → Sistema → Opciones de Ctrl+Alt+Supr`
- Habilitar
	- `Quitar cambio de contraseña`

#### Alternativa en regedit
- Navegar
	`HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System`
- Agregar un valor keyword si no tenemos `System`
- Agregar Dword de 32bit, valor 1 (on) y Decimal
![](https://i.imgur.com/gWbvdfO.png)
- Ok -> cerrar

_Algunas de estas políticas se ejecutan al cerrar regedit, pero otras se debe reiniciar el equipo/reloguear_
O con Powershell:
```powershell
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System" /v "DisableChangePassword" /t REG_DWORD /d 1 /f
```
Revertir:
```Powershell
reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System" /v "DisableChangePassword" /f
```

---
# Desactivar reproducción automática

#### En GPO
- Navegar
	`Configuración de Equipo → Plantillas Administrativas → Componentes de Windows → Directivas de AutoPlay`
- Desactivar
	Habilitar "Desactivar AutoPlay" y "Todas las unidades"

#### En Regedit
- Navegar
	`HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`
- Crear una nueva key "Explorer" si no existe
	- Agregar un nuevo DWord con valor 255
	- Nombre "NoDryveTypeAutoRun"
		- El valor 255 es para "todos los dispositivos"

Con Powershell:
```Powershell
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer" /v "NoDriveTypeAutoRun" /t REG_DWORD /d 255 /f
```
Revertir:
```Powershell
reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer" /v "NoDriveTypeAutoRun" /f
```
![](https://i.imgur.com/UB3ZWBd.png)

---

# Forzar fondo de pantalla

#### En GPO
`Configuración de usuario → plantillas administrativas → escritorio → fondo de escritorio`

#### En regedit
Podemos irnos a este pequeño archivo que debería estar creado:
![](https://i.imgur.com/IJGSBCB.png)

y simplemente cambiamos el valor por la ruta de la imagen `C:\foto.jpg` por ejemplo

- Alternativa con Powershell:
```Powershell
reg add "HKCU\Control Panel\Desktop" /v Wallpaper /t REG_SZ /d "C:\foto.jpg" /f
RUNDLL32.EXE user32.dll, UpdatePerUserSystemParameters
```
- Revertir
```Powershell
reg delete "HKCU\Control Panel\Desktop" /v Wallpaper /f
RUNDLL32.EXE user32.dll, UpdatePerUserSystemParameters
```

**Bonus:** esta es la forma en que lo tuve que hacer ~~donde trabajo porque no quieren usar Windows Server o un equipo centralizado y todo se hace en computadores independientes.~~

- Archivo .PS1 + tarea programada de inicio
```Powershell
Set-ItemProperty -Path 'HKCU:\Control Panel\Desktop\' -Name Wallpaper -Value "C:\foto.jpg"
RUNDLL32.EXE user32.dll, UpdatePerUserSystemParameters
```

---

# Conclusión:

Efectivamente sería más efectivo realizarlo a través de GPO con un sólo equipo centralizado para las políticas, pero en el extraño caso donde haya que hacerlo manualmente 1 por 1 como me pasa a mi... se puede hacer de esta forma.