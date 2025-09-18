---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/05 Deployment Lifecycle/"}
---

# Índice
[[#Gestión de entornos]]
[[#Elegir el mejor]]
[[#Versiones]]
[[#Change history]]

---

### **Concepto de versión de flujo**

Una **versión de flujo** es una instantánea inmutable del flujo borrador (`draft flow`) en un momento específico. Permite guardar el estado de un flujo, incluyendo todos los datos asociados al agente (intenciones, entidades, _webhooks_, etc.), lo que lo hace ideal para probar actualizaciones sin alterar el flujo original.

### **Creación de una nueva versión**

- **Convención de nombres:** Define una convención clara para nombrar las versiones (ej. **`v2.5_03-09-2025`**) y añade una descripción de los cambios realizados.
    
- **Proceso de guardado:** Al guardar, el estado de la versión pasa a **`In Progress`**. Una vez creada por completo, el estado cambia a **`Ready`** y el modelo **NLU** se re-entrena automáticamente.
    
- **Límite:** Solo se pueden almacenar hasta 20 versiones por flujo. Para crear una nueva, es necesario borrar la más antigua.
    

### **Uso y pruebas de versiones**

- **Cargar en borrador:** Se puede cargar una versión guardada en el entorno borrador para seguir trabajando en ella.
    
- **Probar en el simulador:** La función **`Test agent with specific flow versions`** en el simulador permite probar versiones específicas sin afectar el borrador. Esto facilita la colaboración entre múltiples desarrolladores.
    
- **Funcionalidades:** Las versiones permiten gestionar **entornos**, especificar versiones para llamadas de sesión y habilitar la colaboración entre equipos.
    

### **Mejores prácticas**

- **Usar versiones en producción:** Siempre utiliza versiones de flujo estables para el tráfico de producción, ya que el flujo borrador puede romperse fácilmente, especialmente si hay múltiples desarrolladores trabajando en él.
    
- **Guardar el progreso:** Crea una nueva versión después de completar y probar una nueva función o corrección de error para tener un punto de recuperación.
    
- **Coordinación de equipos:** Si varios desarrolladores trabajan en el mismo flujo, es crucial coordinar la creación de versiones para evitar conflictos.
    
- **Errores por cambio de versión:** Cambiar una versión en un entorno de producción con sesiones activas puede causar errores. Se recomienda hacerlo en horarios de bajo tráfico.

Los libros de estrategias (`Playbooks`) también cuentan con la función de **versiones**, similar a la de los flujos, lo que permite guardar instantáneas de su estado para pruebas y control de cambios.

---

### **Cómo crear y usar versiones de _Playbooks_**

1. **Crear una versión:**
    
    - Selecciona el _playbook_ que deseas versionar.
        
    - Haz clic en **`Version history`**.
        
    - Asigna un nombre a la versión en el cuadro de diálogo.
        
    - Haz clic en **`Save`**.
        
2. **Cargar una versión:**
    
    - Selecciona el _playbook_ de interés y ve a **`Version history`**.
        
    - Haz clic en **`view version history`**.
        
    - Haz clic en el ícono del reloj para cargar la versión deseada en el entorno borrador (`draft environment`).
        
    - Al cargar, tienes la opción de **reemplazar los datos a nivel de agente**. Si la seleccionas, se borrarán las actualizaciones realizadas después de la versión que estás cargando.
        
    - Este proceso debe repetirse para cada _playbook_ que necesites versionar.

---

# Gestión de entornos

- **Creación:** Se accede a la función **`Environments`** desde el menú de la consola. Al crear un nuevo entorno, se deben seleccionar las versiones de flujo que se incluirán y asignar un nombre y una descripción.
    
- **Nombres:** Se recomienda usar nombres basados en el propósito del entorno (`"development"`, `"testing"`, `"production"`, etc.) para mantener la organización.
    
- **Historial y gestión:** Es posible ver el historial de ediciones de un entorno, copiar su nombre de recurso para usarlo en llamadas a la **API** y eliminar entornos que ya no se necesiten.
    

### **Casos de uso y mejores prácticas**

- **Aislamiento de tareas:** Tener diferentes entornos permite que los equipos trabajen de manera aislada. Por ejemplo, el equipo de desarrollo puede hacer cambios en un entorno sin afectar el entorno de pruebas, donde se ejecutan los casos de prueba.
    
- **Lanzamientos seguros:** Un entorno de producción (`production`) asegura que los flujos ya probados y aprobados no se vean afectados por los cambios en desarrollo, lo que garantiza un lanzamiento seguro.
    
- **Pruebas en el simulador:** Para probar un entorno específico, se debe seleccionar la opción **`Test agent environment`** en el simulador.
    
- **Comparación de versiones:** Puedes usar la herramienta **`compare versions`** para ver una comparación lado a lado de las versiones de un flujo.

---

# Elegir el mejor

Al momento de elegir el mejor modelo de despliegue para tu equipo de desarrollo, es fundamental considerar la complejidad del flujo de tu agente, el tamaño del equipo y los requisitos del proyecto en Google Cloud.

---

### **Factores de evaluación**

- **Complejidad del flujo:** Los flujos con un solo propósito son más simples de desplegar, mientras que los flujos más complejos, que involucran a múltiples desarrolladores, requieren soluciones que permitan trabajar en paralelo de forma independiente.
    
- **Tamaño del equipo:** Los equipos pequeños pueden usar métodos de despliegue más sencillos. Por el contrario, los equipos grandes se benefician de soluciones personalizadas o de un **CI/CD** (`Continuous Integration/Continuous Deployment`) para una mayor autonomía.
    
- **Requisitos del proyecto:** Las necesidades específicas del proyecto en Google Cloud, como la gestión de roles de usuario o la separación de proyectos para desarrollo y producción, pueden hacer necesaria una solución personalizada.
    

---

### **Configuración sugerida en Google Cloud**

Una configuración recomendada consiste en tener cuatro proyectos separados para cada etapa del ciclo de vida del desarrollo:

1. **Proyecto `Lab`:** Para el desarrollo inicial del agente por parte del equipo.
    
2. **Proyecto `Dev`:** Para que el cliente o usuario pueda evaluar la calidad del agente.
    
3. **Proyecto `Non-prod`:** Para el trabajo de integración y las pruebas de aceptación del usuario (**UAT**).
    
4. **Proyecto `Prod`:** Para la versión de producción del agente, que atiende al tráfico real.

---

# Versiones

Las versiones son copias guardadas de un flujo o agente. Siempre trabajas en un **entorno borrador (`draft`)**, donde todos los cambios se guardan automáticamente. Puedes guardar este borrador como una versión inmutable para futuras referencias y despliegues.

- **Creación:** Para crear una versión, debes asignarle un nombre y una descripción. **Dialogflow** genera un **ID** de versión y entrena el modelo **NLU** automáticamente.
    
- **Estado:** Una versión no puede ser utilizada hasta que su estado cambie de **`In Progress`** a **`Ready`**.
    
- **Características:** Una versión es una instantánea de todos los datos asociados al flujo (intenciones, entidades, _webhooks_, páginas, etc.). Puedes comparar versiones para ver los cambios entre ellas y cargarlas en el borrador para seguir trabajando en ellas.
    
- **Mejores prácticas:**
    
    - Siempre usa versiones estables para el tráfico de producción. El borrador puede romperse fácilmente si hay múltiples desarrolladores trabajando en él.
        
    - Crea versiones para guardar el progreso después de completar una función.
        
    - Prueba los flujos del borrador antes de promoverlos a una versión de producción.
        

---

### **Entornos**

Los entornos te permiten desplegar versiones específicas de tus flujos o agentes. Son cruciales para mantener separados los diferentes pasos del ciclo de desarrollo. Cada entorno tiene una **URL única** para llamadas de sesión.

- **Creación:** Puedes crear tantos entornos como necesites, dándoles nombres que reflejen su propósito (ej. **`development`**, **`testing`**, **`production`**).
    
- **Tipos de entornos comunes:**
    
    - **`Development`:** Ambiente de trabajo para los desarrolladores. Aquí se crean los agentes y se corren las validaciones iniciales.
        
    - **`Staging`** o **`Testing`:** Se usa para pruebas rigurosas. No se hacen cambios directos, sino que los errores se reportan y se arreglan en el ambiente de desarrollo.
        
    - **`Production`:** Se reserva para el tráfico real. Se pueden realizar análisis en vivo y ejecutar experimentos (como pruebas **A/B**).
        
- **Despliegue:** Puedes apuntar una versión específica de un flujo a un entorno diferente. Por ejemplo, la **versión 1** del flujo `A` en el entorno de producción, mientras la **versión 2** está en pruebas.
    
- **URL de entorno:** Para usar un entorno específico, solo necesitas alterar la **URL** del _endpoint_ de la **API** para incluir el **ID** del entorno.

---

# Change history
El historial de cambios (`Change History`) de **Dialogflow CX** es una herramienta que te permite revisar las modificaciones recientes en tu agente, similar a un control de versiones como **Git**.

---

### **Cómo funciona**

1. **Acceso:** Navega hasta la sección **`Change history`** en la consola.
    
2. **Filtrado:** Usa el botón **`Filter`** para refinar la búsqueda por los siguientes criterios:
    
    - **Nombre de visualización (`Display name`):** Nombre del flujo o página.
        
    - **Acción (`Action`):** Tipo de cambio (crear, actualizar, eliminar, restaurar).
        
    - **Tipo de recurso (`Resource type`):** Agente, copia de seguridad, tipo de entidad, flujo, intención, página, etc.
        
    - **Editor (`Editor`):** Dirección de correo electrónico del usuario que hizo el cambio.
        
    - **Marca de tiempo (`Timestamp`):** Fecha y hora del cambio.
        
3. **Visualización:** Los resultados muestran una comparación lado a lado de los cambios, similar a la interfaz de **Git**. Esto te permite ver exactamente qué se ha modificado.
    

### **Características clave**

- **Detalle de cambios:** Al hacer clic en una entrada, se muestra una comparación del estado "antes" y "después" de cada cambio.
    
- **Gestión de objetos:** Todos los objetos de **Dialogflow CX** son representados por objetos **JSON** en el _backend_, lo que te permite importarlos, exportarlos y gestionarlos como si fueran código.