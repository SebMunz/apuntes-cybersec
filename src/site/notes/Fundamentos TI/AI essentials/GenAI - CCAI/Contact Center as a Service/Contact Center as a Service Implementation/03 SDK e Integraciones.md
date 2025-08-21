---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Contact Center as a Service/Contact Center as a Service Implementation/03 SDK e Integraciones/"}
---

# Índice

- [[#Implementación SDK Móvil]]
- [[#Web SDK Implementation (CCAI-P)]]
- [[#Salesforce Integration (CCAI-P)]]
- [[#Zendesk Integration (CCAI-P)]]
- [[#Custom CRM Integration]]
- [[#External Storage – CCAI Platform]]
- [[#🤓☝️]]

---

# Implementación SDK Móvil

El **Mobile SDK** de CCAI Platform permite a las empresas integrar un centro de servicio moderno, que incluye chat y voz, directamente en sus **aplicaciones móviles nativas**. Esto ofrece una experiencia fluida y conveniente para los consumidores, al mismo tiempo que mejora la eficiencia operativa.

#### Canales y Funcionalidades Clave
- **Canal Principal (Chat):** El chat es el canal más popular para el soporte móvil. Permite a los agentes manejar múltiples conversaciones al mismo tiempo, lo que se traduce en un ahorro de costos y tiempo.
- **Canal Secundario (Voz):** El soporte de voz a través de **VoIP** es una alternativa que también puede reducir costos.
- **`SmartActions`:** Una función altamente recomendable que permite a los clientes enviar archivos multimedia como **videos e imágenes**, lo cual es esencial para el soporte técnico o para agilizar procesos como la gestión de reclamaciones en seguros.
- **Múltiples Aplicaciones:** Es posible configurar el SDK para que un mismo cliente lo use en múltiples aplicaciones móviles, como una para consumidores y otra para empleados.

#### Rol del Partner y Complejidad

La complejidad de la implementación varía, por lo que es crucial que el cliente cuente con un **equipo móvil experimentado**.

- **Tu Rol (El Partner):** Tu función principal es la **configuración de la plataforma CCAI-P**. No eres responsable del diseño de la aplicación móvil ni de la integración técnica del SDK.
- **Rol del Cliente:** El cliente debe encargarse del **diseño de la UI/UX**, la **integración del SDK** y las **pruebas** exhaustivas dentro de su entorno de desarrollo.

#### Preparación (Fase de Discovery)

Antes de iniciar la configuración, es vital tener una reunión de descubrimiento con el cliente para entender sus necesidades y expectativas. Estas son algunas preguntas clave:

1. **Experiencia de Usuario:** ¿Cómo quieren que se vea y se sienta la experiencia de soporte en la aplicación?
2. **Flujo del Consumidor:** ¿Cómo llegarán los clientes a la sección de soporte?
3. **Estructura de Colas:** ¿Cómo se organizarán las colas? (por ejemplo, por producto, idioma o prioridad).
4. **Agentes y Equipos:** ¿Qué agentes y equipos manejarán los canales de voz y/o chat?
5. **Funcionalidades:** ¿Qué características específicas desean implementar (ej. agentes virtuales, `SmartActions`)?
6. **Número de Aplicaciones:** ¿El SDK se integrará en una o varias aplicaciones?

#### Pasos de Implementación

El proceso de implementación sigue una secuencia lógica que divide las responsabilidades entre el partner y el cliente.

1. **Configuración de CCAI-P (Partner):** Utilizando la información del `discovery`, se crea la **estructura de colas**, se configuran los **canales** de voz y chat, y se **asignan** los agentes y equipos correspondientes.
2. **Integración del SDK (Cliente):** El equipo de desarrollo del cliente se encarga de integrar el SDK en su código base y de diseñar la interfaz de usuario.
3. **Pruebas (Cliente):** El cliente debe realizar pruebas exhaustivas del flujo de soporte dentro de su entorno de pruebas (por ejemplo, usando `Test Flight` en iOS).
    - **Nota:** El partner generalmente no participa en esta fase.
4. **Lanzamiento:** Una vez que las pruebas son satisfactorias, se lanza la nueva versión de la aplicación a los usuarios. Después del lanzamiento, el cliente pasa a ser responsabilidad del equipo de soporte.

#### Recomendaciones Finales

- **Tiempos de Publicación:** Es fundamental que el cliente sea consciente de los **tiempos de revisión** de las tiendas de aplicaciones, especialmente la de Apple, para planificar adecuadamente la fecha de lanzamiento.
- **Estrategia de Actualización:** Aconseja al cliente que defina una estrategia de actualización y comunicación para informar a sus usuarios sobre la nueva funcionalidad.
- **Soporte Post-Lanzamiento:** El cliente será el principal responsable de solucionar los problemas, a menos que se trate de un error directo en la configuración de la plataforma de CCAI.

---
# Web SDK Implementation (CCAI-P)

## Conceptos clave
- **Web SDK**: permite integrar un widget de chat en un sitio web en pocos minutos.  
- **Objetivo**: conectar consumidores con agentes (humanos o virtuales) y ofrecer servicio automatizado o en horarios offline.  
- **Tipos de implementación**:  
  - **Standard SDK**: simple, rápida, flexible (como pastel de caja).  
  - **Headless SDK**: compleja, personalizada, poco común (como pastel de boda desde cero).  
## Antes de la implementación
- Realizar **discovery call** con el cliente.  
- Participantes necesarios:
  - **Desarrollador web** (implementación en HTML).  
  - **Tomador de decisiones** (supervisor/admin).  
  - Otros miembros relevantes del cliente.  
- Decisiones clave:
  - ¿Cuándo aparece el widget?  
  - ¿Atención con agentes humanos, virtuales o ambos?  
  - ¿Qué preguntas resuelve el widget y cuáles se dirigen a cola?  
  - ¿Se requiere login del consumidor?  
## Discovery call
- Llevar un **archivo HTML de ejemplo** conectado a un tenant de CCAI-P.  
- Cambiar tenant requiere actualizar solo 3 líneas de código.  
- Preparar preguntas para el tomador de decisiones (si no asiste, enviar por correo).  

## Implementación estándar
1. **Obtener credenciales**  
   - En CCAI Platform → Developer settings.  
   - Copiar **company key** y **company secret**.  
   - Añadirlos en el archivo HTML (junto con el **host** URL).  

2. **Configurar plataforma**  
   - En *Settings → Chat*: activar *Web & Mobile chat* (solo admin).  
   - En *Settings → Queue*:  
     - Activar *Web queue*.  
     - Crear nuevas colas (ej. *sales*, *support*).  
     - Configurar ajustes y asignar agentes (humanos o virtuales).  
     - Guardar.  

``` JavaScript
const COMPANY_ID = 'REPLACE_WITH_YOUR_COMPANY_ID_FROM_CCAIP_HERE'
const COMPANY_SECRET = 'REPLACE_WITH_YOUR_COMPANY_SECRET_FROM_CCAIP_HERE'
const HOST = 'https://www.ourccaip.url.ccaiplatform.com/'
menuKey: "Loans"
```

## Pruebas
1. **Como Agente**  
   - Abrir *chat adapter* en CCAI-P.  
   - Verificar que el agente pueda ponerse disponible.  

2. **Como Cliente**  
   - Abrir archivo HTML implementado.  
   - Confirmar que aparezca el widget (burbuja en esquina).  
   - Probar mensaje → verificar recepción en *chat adapter*.  

## Notas
- Si falla la implementación:
  - Revisar **company key** y **secret**.  
  - Pueden refrescarse, pero con cuidado (afecta otras integraciones).  

## Documentación adicional
- [Guía oficial Web SDK CCAI-P](https://cloud.google.com/contact-center/ccai-platform/docs/Guide/publication--en)

---

# Salesforce Integration (CCAI-P)

## Requisitos previos
- **Reunión inicial** con un **Salesforce Administrator** del cliente.
  - No se comparte pantalla (confidencialidad).  
  - Aporta información de funcionalidades necesarias.  
- **Recurso de Google** con:
  - **Acceso administrador** (developer features y configuración).  
  - **Acceso agente** (probar en call adapter).  
- **Cuenta Salesforce con acceso administrador**.  
  - Preferible usar **sandbox** antes de producción.  
- **Datos clave**: URL de la organización en CCAI-P y nombre del tenant.  

## Casos de uso
- **Creación automática de tickets** al iniciar llamada/chat.  
- Registro de interacciones para futuros contactos.  

## Tipos de integración
- **Standard integration**: configuración predeterminada.  
- **Custom integration**: requiere cuestionario previo sobre necesidades específicas.  

---

## Proceso de integración

### 1. Instalación de paquete
- Administrador Salesforce instala el **paquete de integración** (para todos los usuarios).  
- Si ya está instalado → actualizar.  
- Verificar instalación: *Platform Apps → Installed Apps*.  

### 2. Configuración de permisos
- Crear **nuevo Permission Set** clonando *CC_Agents*.  
- Configurar permisos de objetos (object settings → apps → editar).  
- Configurar campo **Tasks object Type**.  
- Asignar usuarios: *Manage Assignments → Add Assignments*.  
  - Incluir admins y agentes que usarán adaptadores.  

### 3. Creación de Connected App
- *Setup → Apps → App Manager → New Connected App*.  
- Completar datos básicos (guardar el nombre).  
- Activar **Enable OAuth settings**:  
  - Añadir **callback URL**: `<tenantURL>/v1/salesforce/start`.  
  - Desactivar *Require proof for code exchange*.  
- Guardar (puede tardar 10 min).  

### 4. Políticas y perfiles
- Editar **policies**: seleccionar *Admin approved users are pre-authorized*.  
- En *Manage Profiles*: asignar perfiles (ej. *Standard User*, *Administrator*).  

### 5. Intercambio de claves
- En Connected App → *Manage Consumer Details*.  
- Copiar **Consumer Key** y **Consumer Secret**.  
- En CCAI-P → *Developer settings*:  
  - Seleccionar CRM = Salesforce.  
  - Ingresar **Key, Secret, Org Name, Org ID**.  
- En Salesforce → *Installed Packages → CC_Agent_App → Configure*.  
  - Ingresar **Key, Secret, Tenant** (desde URL).  
- Guardar cambios.  

### 6. Configuración de Call Center
- En Salesforce → *Call Center → Manage Call Center*.  
- Agregar usuarios que atenderán llamadas en CCAI.  

### 7. Configuración de consola
- **Salesforce Classic Console**:  
  - *Setup → Build → Create → Apps → Sample Console → Edit*.  
  - Añadir componente **_Chat**.  
  - Asignar perfiles de usuario.  

- **Salesforce Lightning Console**:  
  - *Setup → Apps → App Manager → Service Console → Edit*.  
  - En **Utility Items**, añadir:  
    - **CTI Softphone** (configurar label).  
    - **Chat**.  
  - Guardar configuración.  

---

## Notas importantes
- Usar siempre las **mismas claves** (si se regeneran, se rompe la integración).  
- **Connected App** puede tardar hasta 10 minutos en estar lista.  
- Añadir todos los usuarios relevantes en *Permission Sets* y *Call Center*.

---
# Zendesk Integration (CCAI-P)

## Requisitos previos
- **Kick-off call**:
  - Internamente: incluir **consultor técnico**.  
  - Cliente: usuario con permisos de **admin y agente** en CCAI-P y Zendesk.  
  - Incluir **decisor** para definir flujo de información y layout de tickets en Zendesk.  
- Compartir con cliente documentación de **requisitos de red, hardware y software** (evitar bloqueos como firewalls o allowlisting).  

## Proceso de integración

### 1. Descarga de paquetes
- Cliente descarga **dos paquetes** (call y chat).  
- Requiere ambos si se integrarán llamadas y chat.  

### 2. Instalación en Zendesk
1. En **Zendesk → Admin → Apps → Manage → Upload App**.  
2. Asignar nombre (ej. *call v1.3*, *chat v1.3*).  
3. Cargar archivo descargado → **Agree & Upload**.  
4. Configurar subdominio de cuenta.  
5. Habilitar **roles y restricciones**: comenzar con *admin*, luego agregar *agents* según decisión del cliente.  
6. Instalar y guardar.  
7. Repetir para ambos paquetes (call y chat).  

### 3. Configuración OAuth
1. En **Zendesk → Admin → Channels → API → OAuth Clients (+)**.  
2. Completar campos:  
   - Client Name, Description, Company, Logo, Unique Identifier, Redirect URL.  
3. Guardar → obtener **Secret** y **ID** generados automáticamente.  
   - Guardar en lugar seguro.  
   - No regenerar (rompe la integración).  

### 4. Configuración en CCAI-P
1. En **CCAI Platform → Settings → Developer settings**.  
2. Seleccionar CRM = **Zendesk**.  
3. Configurar:  
   - **Subdominio de Zendesk**.  
   - **Unique Identifier** (igual que en Zendesk).  
   - **OAuth Client Secret**.  
4. Guardar.  

### 5. Generación de API Token (Zendesk)
1. En **Zendesk → Admin → Channels → API → Settings**.  
2. Habilitar **Token Access**.  
3. Crear nuevo token (+), asignar descripción.  
4. Guardar token en ubicación segura (no se mostrará nuevamente).  

### 6. Configuración del token en CCAI-P
1. En **CCAI Platform → Settings → Developer settings → API Token**.  
2. Ingresar token generado en Zendesk.  
3. Guardar.  

---

## Notas importantes
- **Mantener sesiones abiertas** en Zendesk y CCAI-P durante todo el proceso.  
- **Claves, secretos y tokens**: si se regeneran → rompen la integración.  
- **Customer y ticket fields** en CCAI-P: configuración **opcional**.  
- Instalar y configurar **call y chat** para integración completa.  

---
# Custom CRM Integration

## Overview
- La integración con CRM personalizados puede ser muy **compleja**.  
- Requiere **conocimiento sólido de APIs**.  
- Es clave revisar la **documentación oficial de CCAI Platform sobre Custom CRM**.  
![](https://i.imgur.com/YoveQYX.png)


---

## Candidate Considerations
Preguntas a responder para evaluar si un cliente es buen candidato:  
- **Objetos principales**: ¿cuáles son los objetos de **Account** y **Record**?  
- ¿Cumplen con el flujo básico de CCAI Platform?  
  - Relación entre objetos.  
  - Soporte de uploads y comentarios.  
- **Método de autenticación**:  
  - ¿Básico o OAuth?  
  - ¿Soportan headers personalizados?  
- **Disponibilidad de REST API**:  
  - ¿Qué aspecto tiene la API?  
  - ¿Algún objeto requiere más de 1 paso para crearse?  
  - ¿Hay variables obligatorias o necesidades personalizadas?  

---

## Case Study: ServiceNow (antes de ser integración nativa)
- **Objetos**:  
  - Account → `Sys User`  
  - Record → `Incident`  
- **REST API**: disponible.  
- **Autenticación**: Basic Authentication.  
- **Características API**:  
  - No requiere procesos en 2 pasos para creación.  
  - Variables requeridas: mínimas, sin problemas.  
  - API permite llamadas exitosas incluso con parámetros faltantes.  
- **Clave**: usa objetos de tipo **Account** y **Record**, y se conecta vía **REST API**.  

---

## Next Steps
Una vez validada la viabilidad de la integración, el cliente debe definir **qué quiere que haga el Custom CRM**:  

- **Casos comunes**:  
  - No crear cuentas/registros → en lugar de eso, usar un **ID específico**.  
    - Aún así, deben configurarse los endpoints de lookup/creation para no romper el flujo.  
  - Sin CRM tradicional → usar API para otras funciones, como:  
    - Presentar datos recolectados de un VA al agente humano.  
    - Mostrar nombre del cliente en el agent adapter.  
  - Uso de **múltiples CRMs con middleware** (ej. Apigee).  
    - Apigee actúa como endpoint único.  
    - La creación/actualización se hace dentro de Apigee.  

- **Acción del desarrollador**: seguir la **documentación de Custom CRM** y configurar los endpoints API necesarios.  

---

## Troubleshooting
- Las integraciones de Custom CRM son **difíciles de depurar**.  
- Recomendación: usar **mock servers** (con herramientas de API o Cloud Functions en GCP).  
  - Permiten probar endpoints de forma aislada.  
  - Ayuda a encontrar dónde falla la integración antes de conectar el CRM real.  
- Importante: los comandos CRM son **secuenciales** → si uno falla, los siguientes también.
- <a href="https://cloud.google.com/contact-center/ccai-platform/docs/Custom_CRM">Documentación oficial</a>

---


# External Storage – CCAI Platform

## Opciones de almacenamiento externo

### 1. Cloud Storage (recomendado)

- Conecta el tenant de CCAI-P con un bucket de GCP
- Recomendado para almacenar información de sesiones.
- Ventaja: facilita el uso de otros productos de Google (ej. **Insights**).
- Configuración:
    - Crear bucket en un proyecto de GCP.
    - Crear **service account** con rol **Object Storage Admin**.
    - Generar **JSON key** de la cuenta de servicio.
    - Configurar la clave en _Developer Settings_ → vincular bucket.

### 2. SFTP Connection

- Útil si el cliente ya tiene un data store (ej. **Azure**).
- Configuración requiere:
    - **Host URL**
    - **Port** (normalmente `22`)
    - **Username**
    - **Password** **o** autenticación con **SSH Private Key**:
        - Pegar clave privada.
        - Ingresar passphrase de la clave.
    - Opción de especificar **Folder Path** para guardar sesiones en un directorio específico.

---

## Relación con CRMs

- Se puede usar **External Storage + CRM**
- Opciones:
    - Guardar datos en ambos (CRM + almacenamiento externo).
    - Guardar solo en almacenamiento externo (para no sobrecargar el CRM).
- Se puede compartir un **URL** al CRM o al **storage** como referencia de datos.

---

## External Storage sin CRM

- Si no hay CRM conectado, **el almacenamiento externo es obligatorio**.
- Razón: la plataforma no guarda datos de clientes (salvo ANI si está habilitado).
- Sin configuración → **no se guardan grabaciones, datos de sesión, transcripts, voicemails o media**.

---

## Funcionalidades que requieren External Storage (si no hay CRM)

- **Voicemail**
    - Necesita almacenamiento externo para guardar mensajes.
    - Sin esto → voicemails se pierden, afecta reportes (faltan Interaction IDs).
- **Call Recording**
    - Requiere CRM o almacenamiento externo.
- **Transcripts**
    - Tanto de **voz** como de **chat** (humano o VA).

---
# 🤓☝️

1. SmartActions es clave
2. Voicemail necesita conexión con almacenamiento
3. El equipo móvil debe preocuparse de que la estética se alineé con la funcionalidad y el UX
4. Los agentes pueden usar múltiples chats simultáneamente con el SDK
5. Cloud Storage es el almacenamiento preferido para CCAI-P
6. Al solucionar problemas de integración con CRM custom, la mejor estrategia es usar mock servers para probar cada endpoint de manera individual