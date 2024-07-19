---
{"dg-publish":true,"permalink":"/Ciberseguridad/Conexiones/Capa de red/"}
---

# Operaciones en la Capa de Red

**Funciones en la Capa de Red**

> Las funciones en la capa de red se centran en organizar la dirección y entrega de paquetes de datos a través de la red e Internet. Esto implica dirigir paquetes de un enrutador a otro mediante la dirección IP de destino y almacenar esta información en tablas de enrutamiento. Todos los paquetes de datos incluyen una dirección IP, y un router utiliza esta dirección para enrutarlos.

---

**Formato de un Paquete IPv4**

- *Encabezado del Paquete:*
  - Tamaño variable entre 20 y 60 bytes.
  - Compuesto por 13 campos, incluyendo versión, longitud del encabezado, tipo de servicio, longitud total, identificación, indicadores, desplazamiento de fragmentación, TTL, protocolo, suma de comprobación, dirección IP de origen, dirección IP de destino y opciones.
- *Datos del Paquete:*
  - Tamaño variable, máximo de 65,536 bytes.
  - Contiene el mensaje a transmitir, como información de un sitio web o texto de correo electrónico.

**Diferencia entre IPv4 e IPv6**

- *Longitud de Direcciones:*
  - IPv4: 4 bytes, hasta 4.3 mil millones de direcciones.
  - IPv6: 16 bytes, hasta 340 undecillones de direcciones.
- *Encabezado del Paquete IPv6:*
  - Más simple que el IPv4, con campos como etiqueta de flujo y clase de tráfico.
- *Seguridad:*
  - IPv6 ofrece enrutamiento más eficiente y elimina colisiones de direcciones privadas.

---

**Conclusiones Clave**

Analizar paquetes de direcciones IP utilizando herramientas de captura de paquetes puede proporcionar información crucial para la seguridad. Comprender los campos en un paquete IPv4 permite tomar decisiones informadas sobre las implicaciones de seguridad de los paquetes inspeccionados. El agotamiento de direcciones IPv4 llevó al desarrollo de IPv6 para abordar la creciente demanda de direcciones IP.
