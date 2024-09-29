---
{"dg-publish":true,"permalink":"/Balanceadores de carga/"}
---

Supervisan y enrutan tráfico de red que fluye desde y hacia un grupo de servidores físicos o virtuales. Pueden ser hardware (routers de balanceo) o software (Citrix ADC).
Distribuyen el tráfico de manera uniforme o con reglas personalizadas. De esta forma, se maximiza el uso del servidor, evita que el tráfico sobrecargue los servidores, etc.
Además pueden incluir otros recursos como aplicaciones, servidores de archivos, de DDBB, etc.

Automáticamente pueden detectar si un servidor falla y redireccionar y balancear el tráfico al resto de los servidores.

## Glosario:
- Cliente
	- Computador o programa que envía solicitudes.
- Host o Nodo
	- Servidor físico o virtual que recibe el tráfico desde un controlador de entrega de aplicaciones (ADC)
- Miembro
	- Host o nodo que recibe tráfico de red en un puerto TCP específico.
- Grupo/Cluster/Granja
	- Conjunto de hosts que ofrecen servicios similares
- ADC
	- Controladores de entrega de aplicaciones. Aparatos físicos, virtuales o software que proporciona balanceo de cargas. También pueden entregar seguridad y encriptación
- Enrutamiento basado en rutas
	- Enruta el tráfico según rutas de URL
- Listening object
	- Proceso de software que verifica el tráfico de red para solicitudes de clientes y reenvía a grupo de destino
- Frontend
	- En balanceo, frontend incluye ADC y cualquier servidor virtual que actúe como proxy para las comunicaciones con los clientes mediante ADC y backend
- Backend
	- En balanceo, incluye los sistemas de grupo, también puede incluir el almacenamiento en disco
- Aplicaciones distribuidas
	- Software almacenado en cloud o servidores físicos que pueden ejecutarse en varios computadores a la vez
- Creador de contenedores
	- Entorno de ejecución aislado que puede implementar y ejecutar aplicaciones distribuidas a través de virtualización. Más rápido y escalable que las soluciones antiguas
- Zona de disponibilidad (AZ)
	- Centros de datos regionales que alojan plataformas cloud y están configurados para alta disponibilidad
- Elastic Load Balancer (ELB)
	- Permite el uso de más de una AZ

---
## Transacción

![](https://i.imgur.com/yiFlyyJ.png)

1. Flecha Azul: Cliente envía conexión y solicitud al servicio ADC
2. Flecha azul: ADC Principal detecta y acepta conexión. Servicio de balanceo de cargas analiza la mejor ruta del host (o miembro) para la solicitud del cliente. ADC cambia IP de destino a la dirección (y TCP si aplica) del host seleccionado
3. Flecha verde: Host o miembro aprueba conexión del cliente y enruta respuesta al cliente a través del ADC
4. Flecha naranja: ADC cambia IP origen a una IP de servidor virtual antes de reenviar la respuesta al cliente.

---

## Tipos de balanceo

### Balanceador de cargas de aplicaciones
Funciona en la [[IT fundamentos/Conexiones y Redes/Modelo OSI#Capas del Modelo OSI\|capa de aplicación]] del [[IT fundamentos/Conexiones y Redes/Modelo OSI\|Modelo OSI]]
analiza el tráfico en busca de errores HTTP y de programación, protege las aplicaciones contra ataques [[Ciberseguridad/Ataques/Red#DDoS\|DDoS]]

### Balanceador de cargas de red
Opera en la [[IT fundamentos/Conexiones y Redes/Modelo OSI#Capas del Modelo OSI\|Capa de transporte]] del [[IT fundamentos/Conexiones y Redes/Modelo OSI\|Modelo OSI]]
Puede enrutar millones de solicitudes de cliente por segundo y controlar cargas de trabajo volátiles. Admite asignación de direcciones IP estáticas y creación de contenedores, entre otros.

### Balanceador de cargas clásico
Puede operar en [[IT fundamentos/Conexiones y Redes/Modelo OSI#Capas del Modelo OSI\|capa de aplicación]] o en la [[IT fundamentos/Conexiones y Redes/Modelo OSI#Capas del Modelo OSI\|Capa de transporte]] del [[IT fundamentos/Conexiones y Redes/Modelo OSI\|Modelo OSI]]
Usa puertos fijos para la comunicación.

### Balanceador de cargas de puerta de enlace
Opera en la [[IT fundamentos/Conexiones y Redes/Modelo OSI#Capas del Modelo OSI\|capa de red]] del [[IT fundamentos/Conexiones y Redes/Modelo OSI\|Modelo OSI]]
Tiene objetos de escucha en todos los puertos que analizan cada paquete IP del tráfico de red y enrutan cada solicitud a los grupos de destino, según configuración del objeto de escucha.
Último punto de entrada y salida para el tráfico de red.

---

## En entornos cloud
Se configura mediante la plataforma de la [[IT fundamentos/Nubes/Mayores proveedores de Cloud\|misma nube]].

Por ejemplo:
- [[IT fundamentos/Nubes/Mayores proveedores de Cloud#GCP\|Google cloud]]
	- Ofrece diversas opciones, como a nivel aplicación y de red, definido por software, conmutación por error multirregional y ajuste automático.
	- También ofrece balanceo externo, interno, global y regional
	- Integrados en Cloud Armor lo que protege contra [[Ciberseguridad/Ataques/Red#DDoS\|DDoS]]
- [[IT fundamentos/Nubes/Mayores proveedores de Cloud#AWS\|Amazon Web Service]]
	- Tres soluciones ELB: balanceador de aplicaciones, puerta de enlace y red
	- Seguridad mediante autenticación de usuario, administración de certificados y desencriptación SSL/TLS
- [[IT fundamentos/Nubes/Mayores proveedores de Cloud#Azure\|Microsoft Azure]]
	- Opera en la capa de transporte del [[IT fundamentos/Conexiones y Redes/Modelo OSI\|Modelo OSI]].
	- Único punto de frontend que acepta solicitudes de clientes para enrutar al servicio backend.
	- Backend puede constar de VM de azure o instancias que se ejecuten en <a href="https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview">Sets de escala de máquinas virtuales</a>
	- 