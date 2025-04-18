---
{"dg-publish":true,"permalink":"/Fundamentos TI/Sistemas Operativos/Linux/Instalación de sistema Linux moderno en computadores antiguos/"}
---

Me topé con un computador un poco antiguo, de mi suegro, que quería reparar para poder usarlo. El computador tenía win7 y por la edad del mismo funcionaba horrible gracias a los navegadores modernos.

Dije "quizás le hace falta una mantención general", es un computador viejo al que nunca le han hecho ningún tipo de mantención.
Para mi sorpresa el computador estaba bastante bien cuidado y limpio, salvo algunas marcas de óxido en algunas partes.

En fín, lo abrí, limpié, cambié algunas gomas, cambio de pasta, lo típico.
El tiempo de inicio del computador mejoró de 1 minuto a unos 35-40 segundos. Nada mal para un HDD, sin embargo seguía mostrando problemas con navegadores y otras tareas básicas así que pasamos al plan B:
**Instalar Mint**

Esto ya lo he hecho con diversos computadores más antiguos y funcionan de maravilla para gente que no suele hacer mucho con su computador más que lo básico.

---

# Problemas:
1. Clásico problema de inicio de booteo donde se iba directo a windows.
	- Solución: Cambiar el orden de booteo en la BIOS, o bien, iniciar directo si trae la opción (usualmente F9).
2. Instalación se quedaba trabada en un loop infinito al descargar paquetes
	- Solución: Venía desde la intermitencia del WiFi, así que se realizó con ethernet
3. La instalación no funcionaba posteriormente, salía error "non-system disk or disk error"
	- Solución: Aquí viene la parte larga...

## Non-system disk or disk error post fresh mint install

Los notebooks/laptops más antiguos se bootean en "legacy", lo que crea una tabla de particiones legacy. Esto hace que el grub (boot loader) esté en el primer sector del disco. Esto hace que comparta el espacio con la tabla de particiones.
Esto nos lleva a que la tabla de particiones GPT sea más grande que una tabla de particiones de legado, osea, no tiene espacio suficiente para el grub. El grub se coloca en una partición separada especial con un flag `bios_grub set`.
En teoría, esto hace que la BIOS lea esta partición y entienda lo que está pasando... pero la BIOS es antigua, por lo tanto no conoce de esto.

### La solución:

Diagnóstico: 
1. Bootear el instalador de linux
2. Abrir terminal
3. `efibootmgr`
	1. Si la respuesta es "EFI variables are not supported" - estás en Legacy
	2. Si es distinta a esa, estás en UEFI y el problema es mayor

Las instrucciones son simples si estás en legacy y puedes forzar UEFI
1. Ir a la BIOS
2. Cambiar el `boot mode` de legacy a `UEFI`
	1. Esto puede ser experimental en algunos así que no está soportado del todo y puedes tener algún problema a futuro
	2. No todos lo tienen...
3. Si lo tiene, simplemente cambiarlo, ejecutar el instalador de Linux
4. Reinstalar el OS con la opción `erase and install`

Si no puedes cambiar a `UEFI`
- La opción más simple: Instalar Linux Mint versión 20.3 o anterior.
- La opción más completa es forzar la instalación a través de MSDOS (?!)
	- Bootear el instalador, abrir `gparted`
	- `device > create partition table > msdos`
	- Crear una partición ext4 usando todo el espacio
	- cerrar `gparted`
	- Correr el instalador, decirle que instale en partición ext4 y darle a `change`
	- Pedirle que lo formatee nuevamente y usarlo para el root `/`
	- Lo más probable es que nos tire una advertencia de que necesitamos una partición EFI, pero a mi entender, para eso es la partición con msdos

Posterior a este engorroso procedimiento, asegurarnos que el orden de booteo es correcto.

# Apartado final:

Si no tiene UEFI, forzarlo
Si no se puede forzar... instalar una versión anterior que soporte legacy, las versiones 20 y previas suelen ser más compatibles.

El método con `msdos` no presenta problemas (hasta ahora) pero lo más seguro es irse con un sistema soportado y testeado.

Una tercera solución más técnica es la de `parted mklabel gpt` + 1 MiB BIOS‑GRUB`
Básicamente seguimos usando GPT, creamos una partición especial BIOS-GRUB separada y realizamos el resto.

``` terminal
gparted
parted /dev/sdX
mklabel gpt
mkpart bios_grub 1MiB 2MiB
set 1 bios_grub on
```

Es más compatible y suele ser la solución estándar al mismo problema.