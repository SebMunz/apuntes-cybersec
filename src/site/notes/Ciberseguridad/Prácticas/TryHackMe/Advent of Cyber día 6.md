---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 6/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 5\|Advent of Cyber día 5]]

Objetivos:
- Utilizar sandboxes para testear
- Reglas YARA para detectar patrones maliciosos
- Técnicas de evasión de malware
- Implementar una técnica de evasión para evitar las reglas de detección YARA

Herramientas y conocimientos:
- [[Ciberseguridad/Ataques/Malware\|Malware]]
- YARA

---

# Sandbox

Un sandbox es un entorno aislado generalmente usado para probar el comportamiento de código malicioso, sin afectar al sistema. Usualmente se instalan además algunas herramientas para monitorear el comportamiento.

Para detectar si un entorno es de sandbox, lo más común es primero verificar si existe la carpeta `C:\Program Files` que no está presente en la mayoría de los entornos de sandbox.

En C se vería de esta forma:

```c
void registryCheck() {
    const char *registryPath = "HKLM\\Software\\Microsoft\\Windows\\CurrentVersion";
    const char *valueName = "ProgramFilesDir";
    
    // Prepare the command string for reg.exe
    char command[512];
    snprintf(command, sizeof(command), "reg query \"%s\" /v %s", registryPath, valueName);
    // Run the command
    int result = system(command);
    // Check for successful execution
    if (result == 0) {
        printf("Registry query executed successfully.\n");
    } else {
        fprintf(stderr, "Failed to execute registry query.\n");
    }
}
int main() {
    const char *flag = "[REDACTED]";
    registryCheck();
        return 0;

} 
```

Básicamente utiliza la ruta del registro, busca el valor, revisa si fue exitoso y retorna la respuesta si es verdadera.

---

# YARA

Herramienta usada para identificar y clasificar malware basado en patrones de código. Se pueden buscar cadenas específicas, headers, patrones de comportamiento, etc.

Por ejemplo:
```javascript
rule SANDBOXDETECTED
{
    meta:
        description = "Detects the sandbox by querying the registry key for Program Path"
        author = "TryHackMe"
        date = "2024-10-08"
        version = "1.1"

    strings:
        
    $cmd= "Software\\Microsoft\\Windows\\CurrentVersion\" /v ProgramFilesDir" nocase

    

    condition:
        $cmd
}
```
Es una regla que busca en el $cmd si es que se está buscando la cadena donde está el registro. De forma que si se detecta un True Positive, hace un log de ello.

---

# Pruebas
Vamos a ejecutar powershell, dirigirnos a `C:\Tools` y correr el comando: `\JingleBells.ps1`, esto se mantendrá ejecutado y va a monitorear los event logs. Alertará si encuentra que se buscó la cadena anterior.
![](https://i.imgur.com/eVokJFz.png)

Ejecutaremos un malware preconfigurado:
`C:\Tools\Malware\MerryChristmas.exe`.
Si todo sale bien, saltará el EDR (Endpoint detection and response) y nos dará la bandera de la pregunta 1.
![](https://i.imgur.com/N6qpm2n.png)

Ahora, podríamos ofuscar el comando del malware, de modo que técnicamente nos saltaríamos la regla YARA.
Por ejemplo la línea:
```C
    const char *registryPath = "HKLM\\Software\\Microsoft\\Windows\\CurrentVersion";
    const char *valueName = "ProgramFilesDir";
```

Podríamos codificarla en base64:
```javascript
    const char *encodedCommand = "RwBlAHQALQBJAHQAZQBtAFAAcgBvAHAAZQByAHQAeQAgAC0AUABhAHQAaAAgACIASABLAEwATQA6AFwAUwBvAGYAdAB3AGEAcgBlAFwATQBpAGMAcgBvAHMAbwBmAHQAXABXAGkAbgBkAG8AdwBzAFwAQwB1AHIAcgBlAG4AdABWAGUAcgBzAGkAbwBuACIAIAAtAE4AYQBtAGUAIABQAHIAbwBnAHIAYQBtAEYAaQBsAGUAcwBEAGkAcgA=";
```
![](https://i.imgur.com/C3GK1Fb.png)

---
# Floss
Floss es una herramienta que extrae y decodifica cadenas, especializado en malwares.
Para usarlo:
`PS C:\Tools\FLOSS> floss.exe C:\Tools\Malware\MerryChristmas.exe |Out-file C:\tools\malstrings.txt`
El comando hace lo siguiente:
- `floss.exe C:\Tools\Malware\MerryChristmas.exe`Escanea las strings.
- `|` pipe similar al de linux para redirigir el output
- `Out-file C:\tools\malstrings.txt` indica donde guardar el resultado

Con esto obtenemos lo siguiente:
![](https://i.imgur.com/BEkTpcz.png)
La primera bandera
![](https://i.imgur.com/JTZpzhu.png)


---

# YARA rules en sysmon logs
Una regla yara usualmente buscará eventos con un id determinado. Podemos extraerlos de Sysmon de windows. Afortunadamente con el monitor EDR que levantamos con anterioridad, ya tenemos el ID que necesitamos:
![](https://i.imgur.com/aAdEXra.png)
Iremos al `windows event viewer -> Apllications and services logs -> Microsoft -> Windows -> Sysmon -> Operational -> Filter Current Log`
![](https://i.imgur.com/14pjnS5.png)
Vamos a la pestaña XML y editaremos manualmente:
![](https://i.imgur.com/6czbgvW.png)
![](https://i.imgur.com/kg2HHW9.png)
- `ParentImage` nos muestra que proceso padre ejecutó cmd.exe para ejecutar el chequeo de registro. Con eso podemos ver que fue el archivo `C:\Tools\Malware\MerryChristmas.exe`.
- `ParentProcessId` y `ProcessId` nos sirven para seguir investigando. Podriamos revisar otros logs por eventos relacionados
- `User` nos ayuda a determinar qué privilegios se usaron para lanzar el comando de `cmd.exe`. Se pudo haber creado una cuenta oculta para hacerlo.
- `CommandLine` qué comando se ejecutó, en detalle.
- `UtcTime` la hora y fecha en que ocurrió. Nos podría ayudar a saber en qué rango horario enfocar nuestra investigación.

---

Con todo este proceso hemos logrado obtener todas las respuestas como están detalladas más arriba :)
![](https://i.imgur.com/f5m5sJj.png)
Procedamos al [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 7\|Advent of Cyber día 7]]