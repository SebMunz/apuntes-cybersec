---
{"dg-publish":true,"permalink":"/Ciberseguridad/HabilidadesBasicasSeguridad/OWASP/"}
---

# OWASP

La **Open Web Application Security Project (OWASP)** es una fundación sin fines de lucro que se dedica a mejorar la seguridad del software. Actúa como una plataforma abierta para compartir información, herramientas y eventos centrados en proteger la web.

## 🔗 [OWASP Top 10](https://owasp.org/www-project-top-ten/)

Desde 2003, OWASP publica la lista **OWASP Top 10**, destacando vulnerabilidades específicas. Esta lista se enfoca principalmente en software nuevo o por encargo, actualizándose cada ciertos años. Su orden se basa en la frecuencia y nivel de riesgo de las vulnerabilidades descubiertas.

### Top 10 actualizado a enero de 2024:

1. **Pérdida de Control de Acceso:**
   - Asegurarse de que los usuarios solo realicen acciones autorizadas en una aplicación web. La pérdida de este control puede conducir a la revelación de información no permitida o acceso no autorizado.

2. **Fallas Criptográficas:**
   - Problemas en la protección de información importante mediante cifrado. Es crucial utilizar métodos de cifrado fuertes para evitar vulnerabilidades, especialmente al manejar datos sensibles.

3. **Inyección:**
   - Introducción de código malicioso en una aplicación vulnerable, permitiendo a los atacantes obtener acceso no autorizado. Proteger contra este tipo de ataques es esencial para garantizar la seguridad de las aplicaciones.

4. **Diseño Inseguro:**
   - Creación de aplicaciones sin considerar la resistencia a ataques, haciéndolas más vulnerables. Es fundamental implementar controles de seguridad durante el desarrollo para prevenir riesgos.

5. **Configuración de Seguridad Incorrecta:**
   - Vulnerabilidad causada por configuraciones incorrectas o falta de auditorías. La correcta configuración y auditoría son esenciales para evitar riesgos de seguridad.

6. **Componentes Vulnerables y Desactualizados:**
   - Riesgos asociados al uso de componentes de software no actualizados. Utilizar bibliotecas de código abierto requiere mantenerlas actualizadas para evitar explotaciones por amenazas.

7. **Fallas de Identificación y Autenticación:**
   - Problemas cuando las aplicaciones no reconocen quién debe tener acceso y qué acciones están autorizadas. La identificación precisa es clave para evitar problemas de seguridad.

8. **Fallas en el Software y la Integridad de los Datos:**
   - Instancias donde las actualizaciones o parches no se revisan adecuadamente, permitiendo a los atacantes distribuir software malicioso. Un ejemplo es el ataque a la cadena de suministro, como el caso de SolarWinds en 2020.

9. **Fallas en el Registro y Monitoreo:**
   - Importancia de registrar eventos y monitorear su origen para identificar y solucionar problemas de seguridad. El monitoreo efectivo es crucial para la respuesta a incidentes.

10. **Falsificación de Solicitudes del Lado del Servidor (SSRF):**
    - Manipulación de operaciones normales de un servidor para acceder a recursos no autorizados. Este tipo de ataque ocurre cuando hay una aplicación vulnerable en el servidor.

Estos puntos clave del OWASP Top 10 ofrecen una guía esencial para desarrolladores y empresas en la creación y mantenimiento de aplicaciones seguras. Asegurar la implementación de medidas de seguridad sólidas es fundamental en un entorno digital cada vez más complejo.