---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Gestion de incidentes/Modelado de amenazas/"}
---

# Modelado de Amenazas

Atacar a un pequeño negocio es diferente de atacar a una agencia gubernamental, cada uno tiene activos distintos y diferentes protocolos de defensa. Para anticipar estos ataques, realizamos el modelado de amenazas.

Este es un proceso en el cual se identifican los activos, sus vulnerabilidades y cómo cada uno se expone a amenazas.

La creación de estos modelos requiere de expertiz y experiencia en el área, por lo tanto, es considerada una habilidad avanzada. Sin embargo, incluso los junior pueden involucrarse.

## Frameworks

Hay diversos modelos, algunos mejores para InfoSec, otros para NetSec, etc. En general, hay 6 pasos:

1. **Definir el alcance**:
   - Determinar qué se va a construir al hacer un inventario de activos y clasificarlos.

2. **Identificar amenazas**:
   - Definir todos los actores potenciales de amenaza.
   - Realizar un Árbol de Ataque, que es un diagrama que mapea las amenazas a los activos.

3. **Caracterizar el ambiente**:
   - Aplicar la mentalidad del atacante, considerando cómo los empleados y usuarios interactúan con el ambiente.
   - Considerar también agentes externos y terceros.

4. **Analizar amenazas**:
   - Examinar las protecciones existentes e identificar agujeros.

5. **Mitigar riesgos**:
   - Crear un plan de defensa ante cada amenaza.
   - Las opciones son evitar riesgo, transferirlo, reducirlo o aceptarlo.

6. **Evaluación**:
   - Todo lo realizado en el ejercicio se documenta, se aplican los arreglos y se anota cualquier suceso, ya sea eventos o lecciones aprendidas, para poder informar y saber cómo realizar un futuro modelado de amenazas.

---

## PASTA

***Process for Attack Simulation and Threat Analysis***

Es un framework de modelado de amenazas con 7 etapas:

- **Definir los objetivos del negocio y seguridad**:
  - Por ejemplo en una pequeña app de fitness, podemos proteger la informacion confidencial de usuarios

- **Definir el alcance técnico**:
  - Identificar los componentes de la aplicación que debemos evaluar (superficie de ataque).

- **Decomponer la aplicación**:
  - Identificar también los controles que tenemos para protegernos.
  - Generar un diagrama del flujo de la información.

- **Analizar amenazas**:
  - Entrar en la mentalidad del atacante.
  - Recolectar información actualizada sobre los ataques comunes.

- **Análisis de vulnerabilidad**:
  - Investigar las potenciales vulnerabilidades considerando la raíz del problema.

- **Modelado de ataque**:
  - Probar las vulnerabilidades analizadas en el paso anterior a través de la simulación de ataques.
  - Se crea el árbol de ataques.

- **Analizar riesgo e impacto**:
  - Recolectar información para poder realizar recomendaciones.

## STRIDE

Desarrollado por Microsoft, se centra en 6 categorías:

- **S**poofing: Suplantación.
- **T**ampering: Manipulación.
- **R**epudiation: Repudio.
- **I**nformation Disclosure: Divulgación de información.
- **D**enial of Service: Denegación de servicio.
- **E**levation of Privilege: Elevación de privilegios.

---

## Trike

Es de código abierto y adopta un enfoque centrado en la seguridad para el modelado de amenazas. Se enfoca comúnmente en permisos de seguridad, casos de uso de aplicaciones, modelos de privilegios y otros.

Utiliza tres aspectos clave:

- **Assets**: Activos.
- **Threats**: Amenazas.
- **Vulnerabilities**: Vulnerabilidades.

---

## VAST

Es parte de una plataforma automatizada de modelado llamada ThreatModeler, escalable a nivel empresarial. VAST significa:

- Visual
- Agile
- Simple Threat modeling.

Engloba todo el ciclo de desarrollo del software, utilizando la automatización, integración y colaboración.