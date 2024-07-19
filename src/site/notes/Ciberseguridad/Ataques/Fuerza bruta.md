---
{"dg-publish":true,"permalink":"/Ciberseguridad/Ataques/Fuerza bruta/"}
---

# Brute Force - Ataque de Fuerza Bruta

Las contraseñas y nombres de usuario son comunes para evitar el acceso no autorizado, pero son propensos al robo o adivinación. El ataque de fuerza bruta consiste en probar numerosas combinaciones hasta encontrar la correcta. Aquí algunos tipos de ataques:

- **Ataque de fuerza bruta simple:**
    - Intento con combinaciones variadas hasta el acceso.

- **Ataque de diccionario:**
    - Similar al simple, pero con una lista de credenciales comunes.

- **Ataque de fuerza bruta inversa:**
    - Comienza con una credencial y se prueba en varios sistemas.

- **Relleno de credenciales:**
    - Utiliza credenciales robadas sin salteo para engañar el sistema de autenticación. También existe una variante especializada llamada **Pass the Hash**, donde se reutilizan credenciales robadas sin salteo.

A menudo se utilizan herramientas como:
- Aircrack-ng
- Hashcat
- John the Ripper
- Ophcrack
- THC Hydra
Si bien las herramientas pueden usarse de manera maliciosa, también puedes usarlas para fortalecer sistemas. 

### Medidas de Prevención

Para mejorar la protección solemos utilizar una combinación de los siguientes controles técnicos y administrativos:

- **Hashing y Salting:**
    - **Hashing:** Convierte información en un valor único para determinar integridad.
    - **Salting:** Agrega caracteres aleatorios para reforzar el hash.

- **MFA (Autenticación Multifactor):**
    - Verificación de identidad con dos o más formas.

- **Captcha:**
    - Prueba pública automatizada de Turing para diferenciar entre máquina y humano.

- **Políticas de Contraseñas:**
    - Requerimientos mínimos, como ocho caracteres, símbolos, números y combinación de mayúsculas y minúsculas. Bloqueo después de intentos fallidos.
  
Para obtener pautas detalladas, se puede hacer referencia al [NIST SP800-63B](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63b.pdf).