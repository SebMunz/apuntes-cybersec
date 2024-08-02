---
{"dg-publish":true,"permalink":"/Ciberseguridad/Habilidades y conocimientos básicos/Controles de acceso/"}
---

# Controles de acceso

Controles de seguridad que se encargan del acceso, autorización y responsabilidad de la información.
Un buen control de acceso mantiene la triada CIA y además expedita el trabajo de los usuarios.

Estos sistemas suelen separarse en tres funciones:
- Autenticación
- Autorización
- Responsabilidad

---

## Autenticación

Controles de acceso que tienen un propósito básico: Preguntar quién está tratando de ingresar.
La forma de responder a estas preguntas depende del sistema, empresa u organización pero en general se basan en tres factores, están ordenados desde el más sencillo al más complejo:
- Conocimiento
  - Identificar algo que el usuario ya sabe, como una contraseña o la respuesta de una pregunta de seguridad
- Propiedad
  - Referirse a *algo* que el usuario posee. Por ejemplo un OTP.
- Características
  - Algo que el usuario *es*. Como la biométrica. Por ejemplo el escaner de huella digital en el teléfono.

Para evitar la frustación que trae el tener que identificarse, existe el SSO (Single sign-on). Una tecnología que combina diferentes sesiones de inicio en una. Esto hace más expedito el acceso a los recursos.
Aunque esto es más conveniente, adhiere una debilidad: identificar a la persona incorrecta le otorga más accesos.
Para esto, existe el MFA (Multi-factor authentication). Con ello, además se agrega una capa adicional de seguridad donde se requiere de una segunda (o más) forma de corroborar quién es el usuario.

##### SSO y MFA
SSO es una tecnología que combina varios inicios de sesión en uno. Esto por tres razones: Mejora la experiencia de usuario, permite a las empresas reducir costos y mejora la seguridad general.
La tecnología surge para combatir la fatiga de contraseñas. Un fenónemo común cuando la gente reutiliza la misma contraseña en distintos servicios. Tener variadas contraseñas es difícil para el usuario pero usar la misma contraseña es un riesgo.

El inicio de sesión único (SSO) simplifica la autenticación al automatizar la confianza entre un usuario y un proveedor de servicios. Utiliza terceros de confianza y tokens cifrados para verificar la identidad, intercambiados mediante protocolos como LDAP (protocolo ligero de acceso a directorios) para la transmisión interna y SAML (lenguaje de marcado para confirmaciones de seguridad) para la externa, comúnmente usados en conjunto.

Si bien tiene sus ventajas, también introduce la vulnerabilidad de que si alguien accede, tendra acceso a más cuentas.

Es ahí donde se introduce el MFA o autenticación de multiples factores.
Esto pide que el usuario verifique su identidad de dos o más formas. Los cajeros automáticos son un buen ejemplo de ello. Ingresas la tarjeta (propiedad) y luego ingresas la contraseña (conocimiento).

---
---
---
---

## Autorización

El siguiente proceso se encarga de _qué pueden hacer_. La autorización utiliza nuevamente el principio del menor privilegio. El acceso sólo debe durar mientras se necesita.
Los sistemas también son influenciados por la idea de la _segregación de funciones_.
La **segregación de funciones** es el principio de que los usuarios no deben recibir niveles de autorización que les permita darle un mal uso al sistema. Esto reduce el riesgo de fallas o de abusos.

---
---
---
---

## Responsabilidad

Se trata de auditar y monitorear el acceso a los sistemas.
Analizar y auditar dichos logs es útil para encontrar irregularidades. 

Cada vez que un usuario accede al sistema, se inicia una sesión. Una sesión es una secuencia de requisitos y respuestas básicos de autentificación asociados al mismo usuario. Estos logs, son como un libro de anotaciones donde se ingresa toda esta información, el cómo, cuándo y qué hizo.

Dos acciones ocurren cuando se inicia una sesión.
- La primera es la creación de una ID de sesión; esta sesión es una token única que identifica al usuario y su equipo. Las ID son relacionadas directamente con el usuario hasta que este cierra el navegador o la sesión expira.
- La segunda es el intercambio de las cookies entre el servidor y el equipo del usuario. Una cookie de sesión, es una token que el sitio web usa para validar la sesión y determinar _cuánto_ debe durar la sesión. Cuando las cookies son intercambiadas, la ID es leida para determinar que información debe mostrarte el sitio web.

Las cookies hacen las sesiones más eficientes. El intercambio asegura que la información sensible, como usuarios y contraseñas, no sea compartida. Sin embargo, existe la vulnerabilidad de que un atacante robe la cookie y suplante la identidad. Este ataque se llama [secuestro de sesión](-ENLACE-)

---
---
---

### Marcos de autorización

- MAC
- DAC
- RBAC

##### MAC
Control de acceso obligatorio. Es el más estricto. El acceso a la información debe ser otorgado manualmente por una autoridad central o administrador.

##### DAC
Control de acceso discrecional. El propietario decide los niveles de acceso. Como por ejemplo cuando el propietario comparte archivos en google drive y escoge quienes son comentadores, editores, solo lectura, etc.

##### RBAC
Se determina según la función que tiene una persona dentro de una organización.

