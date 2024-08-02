---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Vulnerabilidades y exposiciones comunes/"}
---

# Vulnerabilidades y exposiciones comunes

Las vulnerabilidades son debilidades en el sistema.
En cambio, las exposiciones, son errores que pueden ser explotados por una amenaza.
Básicamente, una __vulnera el sistema_ y la otra __expone el sistema__.

### Lista CVE

Aquí entra la lista __CVE__ (Common vulnerabilities and exposures list - Lista de vulnerabilidades y exposiciones comunes), es de libre acceso y de los más populares.
Su función principal es de ofrecer una manera estandar de identificar y categorizar vulnerabilidades y exposiciones. La mayoría de la lista está reportada por investigadores independientes, vendedores de tecnología y hackers éticos, pero es de libre contribución.
Antes de aceptar un ingreso a la lista, el reporte pasa por una CNA (CVE Numbering authority) que es una organización qe se ofrece de voluntaria para analizar y distribuir información de los CVE. Son procesos rigurosos.

La lista tiene cuatro criterios para ingresar una vulnerabilidad a la CVE y asignarle una ID.
- Debe ser independiente de otros problemas
- Debe ser reconocida como un riesgo de seguridad potencial
- Debe ser demostrada con evidencia
- Debe afectar sólo un código base.

Estas vulnerabilidades agregadas a la lista suelen ser revisadas por otras bases de datos de vulnerabilidades donde se les hacen pruebas adicionales para entender sus problemas y determinar el tipo de riesgo que poseen.
Una de las más populares es __NIST National Vulnerabilities Database__
La NIST-NVD utiliza el CVSS (Common vulnerability scoring system) que entrega un puntaje según severidad.
Los equipos de seguridad suelen usar los CVSS para calcular el impacto en el sistema y qué tan prioritario es parcharlo.
El puntaje va de 0-10 y se entrega como base, es decir, no varia con el tiempo.
Un puntaje <4.0 se considera bajo riesgo y no es de atención inmediata. Sin embargo, uno de >9.0 se considera crítico y debe ser tratado de inmediato.