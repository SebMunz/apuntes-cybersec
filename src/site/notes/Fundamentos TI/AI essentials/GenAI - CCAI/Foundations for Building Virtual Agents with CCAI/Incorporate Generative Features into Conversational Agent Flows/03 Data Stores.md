---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Foundations for Building Virtual Agents with CCAI/Incorporate Generative Features into Conversational Agent Flows/03 Data Stores/"}
---

# Índice

[[#Configurar un datastore como fallback]]
[[#Usar datastore con webhook]]
[[#Tipos de pruebas para la IA generativa]]

---

### **Implementación de almacenes de datos (`Data Stores`)**

Los almacenes de datos permiten a tu agente responder preguntas informativas basándose en información de sitios web o documentos. Tienes tres formas principales de usarlos:

1. **Agente independiente:** El almacén de datos actúa como el gestor de diálogo principal para toda la interacción.
    
2. **Aumentar un flujo estructurado:** Integrar la llamada a un almacén de datos dentro de un flujo existente.
    
3. **Aumentar un _Playbook_ generativo:** Llamar a un almacén de datos desde un _Playbook_.
    

Este resumen se centrará en la segunda opción: **aumentar un flujo estructurado**.

---

### **Opciones para llamar a un almacén de datos en flujos estructurados**

Tienes dos maneras de integrar un almacén de datos en un flujo existente:

#### **1. Como respuesta de reserva (`fallback`)**

- **Ventajas:**
    
    - **Integración nativa:** Funciona directamente sin configuraciones adicionales complejas.
        
    - **Sin latencia de _webhook_:** Evita el tiempo de espera asociado a las llamadas a _webhooks_.
        
    - **Menos mantenimiento:** No necesitas crear o mantener intenciones o parámetros específicos para las preguntas que manejará el almacén de datos.
        
- **Cuándo usarlo:** Ideal para situaciones donde el agente no puede hacer coincidir la intención o el parámetro del usuario.
    

#### **2. Mediante un _webhook_**

- **Ventajas:**
    
    - **Control preciso:** Te da control total sobre cuándo se llama al almacén de datos.
        
    - **Activación por intención:** Puedes configurar el almacén de datos para que se active en una ruta de intención específica.
        
    - **Selección de almacén:** Te permite elegir exactamente qué almacén de datos se activa, lo cual es útil si tienes varios (ej., uno para pedidos y otro para facturación).
        
- **Cuándo usarlo:** Cuando necesitas un control exacto sobre la activación y quieres dirigir consultas específicas a almacenes de datos particulares.

---

# Configurar un datastore como fallback

Los almacenes de datos se pueden configurar para que el agente los utilice cuando no encuentra una coincidencia para la intención o un parámetro del usuario.

#### **Pasos de configuración**

1. **Abre el agente** y la página donde quieres añadir el almacén de datos.
    
2. En la página, haz clic en **`Add State Handler`** (Añadir manejador de estado) y selecciona la opción **`Data Stores`** (Almacenes de datos).
    
3. Selecciona **`Edit Knowledge`** (Editar conocimiento) para elegir el almacén de datos que deseas usar. Ten en cuenta que solo verás los almacenes que ya están conectados a tu agente. Si necesitas uno nuevo, puedes crearlo o vincularlo desde la consola de **Vertex AI**.
    
4. Asegúrate de que la variable de respuesta **`$request.knowledge.answers`** esté en la sección de respuestas del agente, ya que esta variable contiene la respuesta generada por el almacén de datos.
    
5. Puedes personalizar la respuesta, por ejemplo, limitando el **número máximo de enlaces** que se envían con la respuesta (hasta un máximo de 5).
    

#### **Estrategias para la activación del almacén de datos**

Cuando un almacén de datos funciona como respuesta de reserva, se activa solo si no hay una coincidencia de intención o de parámetro. Por lo tanto, para que se active, debes asegurarte de que la frase del usuario no active otra cosa.

1. **Remover intenciones:** Si el almacén de datos reemplaza a una intención o un parámetro, asegúrate de que esa intención ya no esté en el ámbito del flujo.
    
2. **Manejar intenciones cercanas:** Si la frase del usuario coincide con una intención que no debería, pero que quieres mantener en el flujo:
    
    - **Intención negativa por defecto:** Puedes añadir la frase a la intención negativa por defecto.
        
    - **Subir el umbral de confianza:** Puedes aumentar el umbral de confianza del agente para que la coincidencia no se active fácilmente.

---

# Usar datastore con webhook

Invocar un almacén de datos mediante un _webhook_ te da un control preciso sobre cuándo y qué almacén se activa, especialmente útil cuando quieres que un almacén responda a consultas específicas que, de otro modo, podrían ser manejadas por intenciones o parámetros.

#### **Arquitectura general**

1. El usuario hace una consulta.
    
2. Esta consulta llega a una página del agente (Página A).
    
3. La Página A llama a un **webhook**.
    
4. El _webhook_ invoca una **función de Cloud Run**.
    
5. Esta función utiliza el método `detect intent` para llamar a otra página del agente (Página B), donde reside el almacén de datos.
    
6. El almacén de datos devuelve una respuesta.
    
7. La Página B responde con la respuesta del almacén de datos.
    
8. La función de Cloud Run devuelve esta respuesta a la Página A.
    
9. La Página A finalmente responde al usuario.
    

_Nota:_ La Página A y la Página B pueden pertenecer al mismo agente o a agentes diferentes.

#### **Pasos de implementación**

1. **Añadir el almacén de datos:** Conecta el almacén de datos a un agente y adjúntalo a una página específica (Página B).
    
    - **Configuración clave de la Página B:** Debe configurarse de modo que **solo el almacén de datos esté en el ámbito**. No debe tener intenciones en el ámbito ni permitir la recopilación de parámetros.
        
2. **Crear el webhook:**
    
    - Configura un **tiempo de espera aumentado** (ej., 30 segundos), ya que las respuestas del almacén de datos pueden tardar.
        
    - Otorga permisos a la cuenta del servicio de la API de Conversational Agents para que la función de Cloud Run pueda realizar la llamada.
        
    - El _webhook_ recibe la consulta del usuario y la información de sesión, la pasa a la función de Cloud Run, la cual usa `detect intent` para llamar a la Página B.
        
3. **Adjuntar el webhook al agente:** Ve a la sección **`Manage`** > **`Webhooks`** y crea uno nuevo.
    
4. **Añadir el webhook a la página:** En la Página A (o la página que iniciará la llamada), habilita los _webhooks_, selecciona el que creaste y añade la etiqueta (`tag`) apropiada.
    

Esta configuración permite "forzar" la invocación de un almacén de datos, incluso cuando el agente podría haber coincidido con otra intención.

---

# Tipos de pruebas para la IA generativa

1. **Pruebas unitarias (`Unit testing`)**
    
    - **Propósito:** Capturar errores en las primeras etapas del desarrollo. Ayudan a asegurar que componentes individuales (como un generador o un _playbook_) funcionen como se espera.
        
    - **Cómo se hacen:** Se pueden realizar en el simulador o con casos de prueba, a menudo son realizadas por los desarrolladores.
        
    - **Cuándo se hacen:** Durante el desarrollo inicial, ya que su objetivo es encontrar errores de forma temprana para que no causen problemas en interacciones más complejas.
        
2. **Pruebas de un solo turno (`Single-shot testing`)**
    
    - **Propósito:** Evaluar las respuestas del modelo a preguntas específicas.
        
    - **Cómo se hacen:** Se crea un conjunto de pruebas con consultas esperadas en producción y las respuestas que se esperan del agente. Las pruebas se pueden ejecutar de forma manual en el simulador o automáticamente con herramientas externas.
        
    - **Evaluación:** Se evalúan las respuestas comparándolas con las respuestas esperadas, usando una combinación de revisiones automáticas y manuales para verificar la similitud del contenido y su completitud.
        
3. **Pruebas de integración (`Integration testing`)**
    
    - **Propósito:** Asegurar que las funciones generativas se integren correctamente con el resto del agente.
        
    - **Qué evaluar:** Verifica que la aplicación funcione de extremo a extremo, incluyendo las transiciones entre flujos estructurados y _playbooks_, y el paso de parámetros entre ellos.
        
4. **Pruebas de rendimiento (`Performance testing`)**
    
    - **Propósito:** Identificar problemas de rendimiento, como latencia o fallos a escala.
        
    - **Métricas clave:**
        
        - **Tiempo de respuesta:** El tiempo promedio que tarda el agente en responder.
            
        - **Concurrencia:** La capacidad del agente para manejar a múltiples usuarios al mismo tiempo.
            
        - **Escalabilidad:** La habilidad para mantener el rendimiento al aumentar la carga de usuarios.
            
5. **Pruebas de aceptación del usuario (`User acceptance testing` - UAT)**
    
    - **Propósito:** Evaluar si el agente satisface a los usuarios reales.
        
    - **Cómo se hacen:** Se pide a usuarios que interactúen con el agente en conversaciones naturales.
        
    - **Aspectos a probar:** Manejo del contexto, sesgos, seguridad, satisfacción del usuario y experiencia general.
        
6. **Pruebas de caja negra (`Black box testing`)**
    
    - **Propósito:** Evaluar el agente desde la perspectiva de alguien que no conoce sus componentes internos.
        
    - **Participantes:** Personas fuera del equipo de desarrollo o usuarios reales.
        
7. **Pruebas de regresión (`Regression testing`)**
    
    - **Propósito:** Asegurarse de que las nuevas actualizaciones no hayan roto funcionalidades existentes.
        
    - **Cómo se hacen:** Las pruebas unitarias o de integración que se han pasado consistentemente se convierten en pruebas de regresión. Se ejecutan con regularidad para verificar que el agente sigue funcionando como se espera después de cada cambio. Se pueden ejecutar con herramientas como SCRAPI.