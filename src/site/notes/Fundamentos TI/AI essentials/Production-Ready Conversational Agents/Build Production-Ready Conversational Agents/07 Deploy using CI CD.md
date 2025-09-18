---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/07 Deploy using CI CD/"}
---

# Índice

asdf

---

# Usar GIT

Mientras que la función de importación y exportación de **Dialogflow CX** es útil para copias de seguridad, no es ideal para el trabajo en equipo o para rastrear cambios. Usar un servicio de _hosting_ de **Git** (como **GitHub**, **GitLab** o **Bitbucket**) permite:

- **Control de versiones:** Mantener un historial de cambios.
    
- **Colaboración en equipo:** Varios desarrolladores pueden contribuir de forma simultánea.
    
- **Flujos de trabajo familiares:** Utiliza las metodologías de **Git** para gestionar el desarrollo.
    
- **Respaldo y recuperación:** Crea copias de seguridad y permite restaurar versiones anteriores.
    

---

### **Configuración de la integración con Git**

La integración se configura en la sección **`General`** de las opciones del agente. Necesitas proporcionar:

1. **Nombre de visualización:** Para identificar la integración.
    
2. **URL del repositorio:** La ruta a tu repositorio Git.
    
3. **Ramas:** La(s) rama(s) que se sincronizarán con el agente.
    
4. **Token de acceso:** Para la autenticación. Es una buena práctica almacenarlo de forma segura en **Secret Manager**.
    

---

### **Uso de Secret Manager**

**Secret Manager** es un servicio seguro para almacenar información sensible. Para integrarlo con **Dialogflow CX**, sigue estos pasos:

1. **Crear el token:** Genera un token de acceso personal en tu servicio **Git** y almacénalo en **Secret Manager**.
    
2. **Asignar permisos:** Otorga a la cuenta de servicio de **Dialogflow CX** el rol de **`Secret Manager Secret Accessor`** para que pueda acceder al token.
    

### **Operaciones básicas**

- **`Push`:** Envía los cambios del agente al repositorio **Git**. Debes escribir un mensaje de _commit_ para describir los cambios.
    
- **`Restore`:** Te permite volver a un cambio guardado previamente en una rama de Git.

---

# CI/CD

La automatización de pruebas y despliegues en **Dialogflow CX** se logra mediante las funciones de **Pruebas Continuas** (`Continuous Tests`) y **Despliegue Continuo** (`Continuous Deployment`). Estas herramientas son esenciales para garantizar que las versiones de los flujos funcionen correctamente antes de ser utilizadas en un entorno en vivo.

---

### **Pruebas Continuas (`Continuous Tests`)**

Las pruebas continuas ejecutan automáticamente un conjunto de casos de prueba para un entorno específico. Puedes configurar estas pruebas para que se ejecuten una vez al día o cada vez que se seleccione una nueva versión del flujo.

- **Configuración:**
    
    1. Selecciona el nombre de un entorno.
        
    2. Incluye los casos de prueba que quieres usar en el **conjunto de evaluación**.
        
    3. Activa el botón de **`Continuous test`** en la configuración.
        
- **Resultados:** Para ver los resultados, ve a la pestaña **`Continuous tests`** y luego a **`Results`**.
    
- **Estado:** En el menú **`Environments`**, en la columna **`Continuous Test`**, puedes ver si las pruebas continuas están activas para un entorno.
    

### **Despliegue Continuo (`Continuous Deployment`)**

El **Despliegue Continuo** automatiza la ejecución de las pruebas de verificación antes de que una versión del flujo se despliegue en un entorno. Esto evita que una versión defectuosa llegue a producción.

- **Configuración:** Activa el botón de **`Continuous deployment`** en la configuración del entorno.
    
- **Estado:** La columna **`Continuous deployment`** en la lista de entornos indica si las pruebas se ejecutarán cada vez que se active una versión.
    
- **Flujo de trabajo:** El **Despliegue Continuo** actúa como un **control de calidad** automático: si las pruebas fallan, el despliegue se detiene, previniendo errores en el entorno.

---

# Automatización DevOps y CI/CD

La **automatización** es clave en el marco de **DevOps** para estandarizar el desarrollo, las pruebas y el despliegue de agentes conversacionales. Esto ayuda a eliminar errores humanos, garantiza la seguridad y permite volver a versiones anteriores de manera eficiente.

---

### **Puntos clave de la automatización**

- **Integración y pruebas continuas:** Cada vez que se envía un nuevo código al repositorio, se debe activar automáticamente un **proceso de compilación y prueba**. Esto incluye pruebas unitarias y de integración para asegurar que los cambios no rompan la lógica del sistema.
    
- **Despliegue automatizado:** El despliegue de cambios debe ocurrir solo después de que la compilación cumpla con criterios de prueba específicos. Esto garantiza que solo el código validado llegue a los entornos en vivo.
    

---

### **Monitoreo y análisis**

El **monitoreo** es esencial para dar seguimiento a los sistemas después del despliegue. Consiste en recopilar y analizar información para tomar decisiones informadas.

- **Objetivos del monitoreo:**
    
    - Tomar decisiones informadas ante cambios que afectan el rendimiento.
        
    - Aplicar un enfoque científico a la respuesta a incidentes.
        
    - Medir la alineación del servicio con los objetivos del negocio.
        
    - Analizar tendencias a largo plazo y comparar experimentos.
        
    - Definir alertas sobre métricas críticas y construir paneles en tiempo real.
        
    - Realizar análisis retrospectivos.
        
- **Métricas para planificar:**
    
    - Utilización promedio y pico.
        
    - Patrones de uso y picos estacionales (ej. en periodos festivos).
        
    - Cantidad de sobreaprovisionamiento necesario para manejar picos de tráfico.
        

---

### **Proceso de escalamiento**

Un proceso de **escalamiento** bien definido es crucial para reducir el tiempo y el esfuerzo necesarios para resolver problemas.

- **Elementos clave:**
    
    - Definir cómo y cuándo escalar los problemas internamente.
        
    - Crear casos de soporte.
        
    - Documentar la arquitectura del sistema.
        
    - Establecer permisos de acceso para quienes necesiten soporte.
        
    - Incluir pasos para configurar monitoreo y alertas.
        
    - Documentar las acciones y la planificación de sucesión para capacitar a nuevos miembros del equipo.
---

