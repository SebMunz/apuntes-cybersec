---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones/Modelo TCP_IP/"}
---

# Modelo TCP/IP:

- Organiza la comunicación en red mediante protocolos.
- Dos modelos comunes: TCP/IP y OSI (más detallado).

## Capas del Modelo TCP/IP:

1. **Acceso a la red:**
   - Organiza envío y recepción de paquetes dentro de una red.
   - Involucra hardware físico como hubs, módems y cables.
   - Protocolo ARP asigna direcciones IP a direcciones MAC.
   - Interpretación de las señales que recibe, como ethernet.

2. **Internet/Network:**
   - Asegura entrega al host de destino en diferentes redes.
   - Protocolo IP posibilita comunicación entre redes.
   - Protocolo ICMP comparte información de errores.
   - Permite la comunicación entre redes a través de routers

3. **Transporte:**
   - Entrega datos de manera confiable.
   - TCP asegura transmisión segura.
   - UDP para aplicaciones sensibles al rendimiento.
   - Resuelve en qué cliente y servidor los programas serán entregados

4. **Aplicación:**
   - Realiza solicitudes o responde a ellas.
   - Define accesos a servicios y aplicaciones.
   - Protocolos incluyen HTTP, SMTP, SSH, FTP, DNS.

![osi_tcpip.png](/img/user/Assets/osi_tcpip.png)
## Comparación con Modelo OSI:

- Modelo OSI visualiza protocolos en siete capas.
- Modelo TCP/IP combina capas del modelo OSI.
- Ambos ayudan a entender procesos y protocolos de transmisión de datos.

## Conclusiones Clave:

- Modelos TCP/IP y OSI facilitan visualización de procesos y protocolos en redes.
- Modelo TCP/IP tiene cuatro capas, más simple que el modelo OSI de siete capas.
- A veces suele encontrarse con 5 capas, agregando la siguiente:
	- Capa física: Todo lo "físico" que interconecta los computadores como cables, conectores y emisores de señal en general.