---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/Production-Ready Conversational Agents/Build Production-Ready Conversational Agents/06 Programmatic access to Conversational Agents/"}
---

# Índice

[[#Acceso programatico]]
[[#Desarrollo con SCRAPI]]


---
# Acceso programatico

### **Herramientas para acceso programático**

Hay tres herramientas principales para automatizar las operaciones y el mantenimiento de los agentes conversacionales:

1. **API de Dialogflow CX:** Permite automatizar despliegues y reconfiguraciones. Se basa en **RPC** (`Remote Procedure Calls`), lo que puede ser un desafío si solo estás familiarizado con las **API RESTful**. Existen múltiples versiones de la API, cada una con un ciclo de vida propio (**`Generally Available`**, **`Beta`**, **`Alpha`**).
    
2. **Bibliotecas de cliente:** Similares a las API, permiten acceder a sus funcionalidades desde lenguajes de programación populares.
    
3. **SCRAPI:** Es una **API** de **Python** de alto nivel que simplifica la experiencia de desarrollo al manejar la complejidad subyacente de las **API nativas de Google**.
    

---

### **SCRAPI: una alternativa de código abierto**

**SCRAPI** (`Dialogflow Scripting API`) es una herramienta de código abierto ideal para automatizar operaciones.

- **Ventajas:**
    
    - Simplifica la autenticación y regionalización.
        
    - Reduce la cantidad de código necesaria.
        
    - Permite trabajar con datos en estructuras de **Python** familiares (listas y diccionarios).
        
- **Extensiones:**
    
    - **`Pandas DataFrames`:** Permite manejar los datos en un formato de tabla.
        
    - **`Google Sheets`:** Permite sincronizar las frases de entrenamiento y otros recursos entre el agente y una hoja de cálculo. Esta integración es **bidireccional**.
        
    - **`Cloud Functions`:** Facilita la construcción de _webhooks_.
        
- **Flujo de trabajo:** Se pueden extraer recursos del agente con **SCRAPI** para modificarlos y luego escribirlos de vuelta al mismo agente o a otro. Esto permite usar **sistemas de control de versiones** externos (como **Git**) para gestionar **CI/CD** (`Continuous Integration/Continuous Deployment`).

---
# Desarrollo con SCRAPI

El desarrollo de agentes conversacionales con **SCRAPI** se basa en tres bloques principales: **`Core`**, **`Tools`** y **`Builders`**.

---

### **Autenticación**

- **Local o Colab:** Autentícate usando la interfaz de línea de comandos de **gcloud** (`gcloud CLI`).
    
- **Servicios de Google Cloud:** Asegúrate de que la cuenta de servicio tenga el rol de **`Dialogflow IAM`** si la aplicación se ejecuta en servicios como **Cloud Run**.
    

---

### **Bloques de SCRAPI**

1. **`Core`**: Contiene las clases y métodos de alto nivel que representan los recursos principales de **Dialogflow CX** (agentes, intenciones, flujos, etc.). Estos son los bloques fundamentales para construir métodos o herramientas personalizadas.
    
2. **`Tools`**: Incluye _toolkits_ para tareas de gestión más complejas, como:
    
    - Manipular recursos del agente en estructuras de datos como **`DataFrames`**.
        
    - Copiar recursos entre agentes y proyectos de **Google Cloud**.
        
    - Transferir datos entre **Dialogflow CX** y otros servicios de **Google Cloud** como **BigQuery** o **Google Sheets**.
        
3. **`Builders`**: Ofrece métodos para construir **`protos`**, que son los componentes fundamentales de **Dialogflow CX**. Permite construir recursos del agente sin necesidad de hacer llamadas a la **API**, para luego subirlos de forma masiva a un agente activo.

---

