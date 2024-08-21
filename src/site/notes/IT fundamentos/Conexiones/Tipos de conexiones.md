---
{"dg-publish":true,"permalink":"/IT fundamentos/Conexiones/Tipos de conexiones/"}
---

# TIPOS DE CONEXIONES
_Conexiones comunes en el área y su impacto_

#### **Cable**

Ethernet, la conexión más común, transmite datos de manera segura y rápida mediante cables Cat5 o superior. Es considerada más confiable y segura que la inalámbrica debido a su menor vulnerabilidad a interferencias y accesos no autorizados.

---

#### **USB**

Ampliamente utilizado para conectar periféricos a computadoras. Aunque es conveniente, plantea riesgos de seguridad al conectar dispositivos no confiables. Es crucial garantizar que sean dispositivos de confianza.

---

#### **Inalámbricas**

Wi-Fi, el más común, ofrece flexibilidad y movilidad sin cables físicos. Introduce riesgos de seguridad comunes. Para mitigar algunos riesgos, se recomienda el cifrado WPA3, el uso de contraseñas seguras y actualizaciones del firmware del router. Wi-Fi es conveniente por su fácil configuración y escalabilidad.

###### Riesgos comunes:
- Escuchas: Interceptación de datos transmitidos.
- Puntos de Acceso Falsos.
- Man in the Middle: Interceptación de datos entre dispositivos en la red, alterando los datos.

###### Mejores prácticas para mitigar riesgos:
- Cifrado fuerte.
- Cambiar credenciales predeterminadas.
- Actualizar firmware del router.
- Red de invitados.
- Desactivar WPS.
- Usar VPN.

---

#### **Bluetooth**

Conexión de corto alcance entre dispositivos. Conveniente pero no exento de ataques como Bluesnarfing, BlueBorne y Bluejacking. Para mitigar riesgos, se recomienda mantener dispositivos actualizados, usar Bluetooth 4.0 (mínimo) y desactivarlo cuando no está en uso. Opera en la frecuencia 2.4 GHz.

###### Ataques Bluetooth:
- Bluejacking: Comunicación no solicitada.
  - Mitigación: Desactivar visibilidad y rechazar conexiones no solicitadas.
- Bluesnarfing: Acceso al dispositivo de forma maliciosa a través de una vulnerabilidad en el protocolo.
  - Mitigación: Mantener actualizado, desactivar visibilidad si no está en uso.
- BlueBorne: Vulnerabilidad crítica que explota debilidades del protocolo, utilizada para ganar control del dispositivo infectado e infectar otros dispositivos cercanos.
  - Mitigación: Mantener actualizado, desactivar Bluetooth si no está en uso.

---

#### **Enmascaramientos**

O conexiones de red. Los VPN son túneles seguros que crean conexiones de red privada sobre una red pública. De esta forma, se protege la información de interceptaciones. Útiles al usar Wi-Fi público. Utilizar proveedores confiables.

---

#### **P2P**

Peer-to-Peer. Conexión descentralizada, común en servicios de intercambio de archivos. Sin medidas de seguridad adecuadas, presentan un inmenso riesgo. Evitar servicios no confiables y nunca compartir información sensible en ellos.

---

#### **NFC**

Near Field Communication, derivado del área de las RFID. Tecnología inalámbrica de corto alcance. Opera a 13.56 MHz, muy utilizada en aplicaciones como pagos sin contacto y control de acceso. Conecta a través de etiquetas y lectores. Tiene tres modos: Lector/Escritor, P2P y Emulación de tarjeta.

- **Lector/Escritor:**
  - Permite al dispositivo leer o escribir en etiquetas NFC, como posters.
- **P2P:**
  - Permite que dos dispositivos intercambien información, como compartir datos de contacto.
- **Emulación de Tarjeta:**
  - Permite que un dispositivo actúe como tarjeta inteligente, facilitando pagos.

A pesar de su conveniencia, presenta riesgos de seguridad como la manipulación de datos por terceros y accesos no autorizados. Para mitigar estos riesgos, se recomienda:
- Mantener firmware y aplicaciones actualizadas.
- Uso de contraseñas fuertes.
- Desactivar si no está en uso.
- Escanear etiquetas NFC de confianza.
- Usar aplicaciones confiables y seguras para las transacciones.

**NOTA: Ver FLIPPER ZERO como herramienta para PenTest.**

---

#### **Infrarroja (IR)**

Utiliza ondas de luz para transmitir datos. Común en comunicación de corto alcance, utilizado en controles remotos, teclados y mouse inalámbricos y comunicación entre computadoras e impresoras. Aunque es privado, de fácil configuración y de bajo consumo, se deben considerar medidas de seguridad, como cifrado, autenticación y seguridad física.

Algunos ataques a considerar:
- Replay Attack: transmisión previamente grabada y legítima que se reproduce posteriormente para engañar.
- Spoofing: emular un dispositivo autorizado para ganar acceso.
- Interceptación: A través de dispositivos especializados se puede interceptar y reproducir la señal.
- Ingeniería Social: persuadir a la víctima para realizar acciones no seguras, como aceptar conexiones desconocidas.

---
#### Wi-Fi
