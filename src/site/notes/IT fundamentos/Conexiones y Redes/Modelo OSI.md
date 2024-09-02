---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones y Redes/Modelo OSI/"}
---

# Comparación Modelos TCP/IP y OSI:

- El Modelo de Interconexión de Sistemas Abiertos (OSI) estandariza funciones en siete capas, mientras que TCP/IP, con cuatro capas, simplifica el diseño y conceptualización de procesos en redes.
- Ambos modelos son ampliamente utilizados para entender cómo diferentes protocolos y tecnologías de red colaboran para la transmisión y comunicación eficientes de datos.

# Capas del Modelo OSI:

1. **Capa de Aplicación (7):**
   - Conecta al usuario a la red mediante aplicaciones y solicitudes.
   - Interfaz entre el usuario y el sistema de comunicación.
   - Ejemplos: HTTP, SMTP, DNS.

2. **Capa de Presentación (6):**
   - Traduce y cifra datos para la red.
   - Ejemplo: SSL para cifrado.

3. **Capa de Sesión (5):**
   - Establece conexiones entre dispositivos y maneja autenticación y reconexión.

4. **Capa de Transporte (4):**
   - Envía datos, maneja velocidad y flujo.
   - Protocolos de transporte: TCP y UDP.

5. **Capa de Red (3):**
   - Supervisa recepción y entrega de paquetes según direcciones IP.
   - Rutea paquetes de datos entre dispositivos, independientemente del medio físico.
   - Asigna direcciones lógicas (IP) a los dispositivos.

6. **Capa de Enlace de Datos (2):**
   - Organiza envío y recepción de paquetes.
   - Incluye switches y tarjetas de interfaz de red.
   - Crea enlaces confiables y detecta/corrige errores.

7. **Capa Física (1):**
   - Hardware físico de transmisión de red.
   - Transmite datos crudos entre dispositivos a través de cables de cobre o fibra óptica.
   - Incluye Hubs, módems y cableado.

![osi_tcpip.png](/img/user/Assets/osi_tcpip.png)

# Conclusiones Clave:

- Modelos TCP/IP y OSI son esenciales para diseñar procesos y protocolos de transmisión de datos.
- El Modelo OSI, con siete capas, se utiliza para comunicación detallada sobre problemas o amenazas.
- Ingenieros y analistas de seguridad emplean ambos modelos para conceptualizar procesos y detectar interrupciones o amenazas.
