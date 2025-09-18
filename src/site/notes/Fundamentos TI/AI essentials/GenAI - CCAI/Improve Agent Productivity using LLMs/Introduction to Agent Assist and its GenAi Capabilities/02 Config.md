---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Improve Agent Productivity using LLMs/Introduction to Agent Assist and its GenAi Capabilities/02 Config/"}
---

Toda interacción en Agent Assist requiere un Conversation Profile.

Intentan resolver al cliente antes de escalar a un humano.
También pueden saltar directo al humano sin interactuar con el agente conversacional.
Esto se define en el perfil conversacional (conversation profile)

Como hacer el setup
1. Elegir o crear un nuevo agente conversacional
2. En la consola: crear o editar un profile
3. En los detalles del perfil activar "Enable Convesational Agent"
4. Linkear el agente al perfil

Un perfil configura los parámetros que controlan las sugerencias.
Configura también las categorías de sugerencias.

---

# Crearlo a través de API

![Pasted image 20250817210249.png](/img/user/Assets/Pasted%20image%2020250817210249.png)

##### JSON
![Pasted image 20250817210301.png](/img/user/Assets/Pasted%20image%2020250817210301.png)

##### PYTHON
![Pasted image 20250817210212.png](/img/user/Assets/Pasted%20image%2020250817210212.png)

##### REST
![Pasted image 20250817210350.png](/img/user/Assets/Pasted%20image%2020250817210350.png)![Pasted image 20250817210442.png](/img/user/Assets/Pasted%20image%2020250817210442.png)

##### Curl
![Pasted image 20250817210450.png](/img/user/Assets/Pasted%20image%2020250817210450.png)
##### PowerShell
![Pasted image 20250817210458.png](/img/user/Assets/Pasted%20image%2020250817210458.png)

# User-participant
![Pasted image 20250817210526.png](/img/user/Assets/Pasted%20image%2020250817210526.png)
##### REST
![Pasted image 20250817210538.png](/img/user/Assets/Pasted%20image%2020250817210538.png)

##### REST
![Pasted image 20250817210549.png](/img/user/Assets/Pasted%20image%2020250817210549.png)
##### CURL
![Pasted image 20250817210558.png](/img/user/Assets/Pasted%20image%2020250817210558.png)
![Pasted image 20250817210607.png](/img/user/Assets/Pasted%20image%2020250817210607.png)

# Agent-participant
##### PYTHON
![Pasted image 20250817210633.png](/img/user/Assets/Pasted%20image%2020250817210633.png)
![Pasted image 20250817210641.png](/img/user/Assets/Pasted%20image%2020250817210641.png)
![Pasted image 20250817210652.png](/img/user/Assets/Pasted%20image%2020250817210652.png)
![Pasted image 20250817210659.png](/img/user/Assets/Pasted%20image%2020250817210659.png)

# PGKA

![Pasted image 20250817210911.png](/img/user/Assets/Pasted%20image%2020250817210911.png)
![Pasted image 20250817210922.png](/img/user/Assets/Pasted%20image%2020250817210922.png)
![Pasted image 20250817210930.png](/img/user/Assets/Pasted%20image%2020250817210930.png)
![Pasted image 20250817210939.png](/img/user/Assets/Pasted%20image%2020250817210939.png)

## En resumen:

El proceso se divide en los siguientes pasos clave:

#### 1. Crear un perfil de conversación

- Se realiza una llamada al método `create` en el recurso **Conversation Profile**.
- Es crucial reemplazar los valores de **Project ID**, **Location ID** y **Agent ID** con los datos correctos de tu proyecto.
#### 2. Gestionar las conversaciones en tiempo de ejecución

- **Crear una conversación:** Primero, se llama al método `create` en el recurso **Conversation**. Para esto, se requiere el **Project ID**, **Location ID** y el **Conversation Profile ID** que obtuviste en el paso anterior.
- **Añadir participantes:** Una vez creada la conversación, se deben agregar un participante de usuario y un participante de agente. Ambos se crean llamando al método `create` en el recurso **Participant**. Este paso necesita el **Project ID**, **Location ID** y el **Conversation ID**.
#### 3. Analizar el contenido

- Para procesar los mensajes, se utiliza el método `analyzeContent` en el recurso **Participant**.
- Cada mensaje escrito por el usuario o el agente debe enviarse a la API para que el agente del almacén de datos pueda analizarlos y generar sugerencias para el agente humano.