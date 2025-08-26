---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI - CCAI/Documentación/"}
---


# Bot de Mesa de Ayuda con Dialogflow CX - Documentación Completa

## Tabla de Contenidos

[[#Resumen Ejecutivo]]
[[#Arquitectura del Sistema]]
[[#Requisitos Previos]]
[[#Implementación Paso a Paso]]
	[[#Fase 1 Configuración de Dialogflow CX]]
	[[#Fase 2 Knowledge Base Setup]]
	[[#Fase 3 Configuración de Firebase]]
	[[#Fase 4 Desarrollo de Webhooks]]
	[[#Fase 5 Configuración de Agent Assist]]
	[[#Fase 6 Desarrollo de Landing Page]]
[[#Mantenimiento y Actualizaciones]]
[[#Troubleshooting Común]]

---
## Resumen Ejecutivo

### Objetivo
Crear un bot conversacional inteligente para mesa de ayuda que automatice la resolución de problemas técnicos, con capacidad de escalamiento a agentes humanos y gestión de tickets.

![](https://i.imgur.com/fxK0IY3.png)

### Componentes Principales

- **Dialogflow CX**: Motor conversacional principal
- **Knowledge Base**: Base de conocimientos con PDFs de soluciones
- **Firebase**: Base de datos para tickets y gestión de estados
- **Agent Assist**: Features de IA para agentes humanos
- **Landing Page**: Demo funcional del sistema
---
---
## Arquitectura del Sistema

### Flujo de Conversación

1. **Nivel 1**: Bot autónomo con Knowledge Base
2. **Nivel 2**: Escalamiento con opciones (ticket/humano)
3. **Nivel 3**: Agente humano con asistencia de IA
4. **Persistencia**: Firebase para tickets y datos

### Stack Tecnológico

- **Backend**: Google Cloud Platform (Dialogflow CX, Firebase)
- **Frontend**: HTML/CSS/JavaScript (Landing page)
- **APIs**: Dialogflow CX API, Firebase API
- **Storage**: Cloud Storage (PDFs), Firestore (tickets)

---
## Requisitos Previos

### Cuentas Necesarias

- [ ] Cuenta de Google Cloud Platform con facturación habilitada
- [ ] Proyecto de GCP creado
- [ ] APIs habilitadas:
    - Dialogflow API
    - Cloud Storage API
    - Firestore API
    - Agent Assist API

### Herramientas Requeridas

- [ ] Google Cloud SDK instalado
- [ ] Node.js (versión 14+)

### Documentos de Preparación

- [ ] PDFs con soluciones técnicas organizados
- [ ] Listado de problemas más comunes
- [ ] Flujos de escalamiento definidos

---
## Implementación Paso a Paso

### Fase 1: Configuración de Dialogflow CX

#### 1.1 Crear el Agente Principal

```bash
# Crear agente en Dialogflow CX
# Navegar a: https://dialogflow.cloud.google.com/cx
# Crear nuevo agente con configuración:
```

**Configuración del Agente:**

- **Nombre**: -
- **Idioma por defecto**: Español
- **Zona horaria**: America/Santiago
- **Descripción**: Bot de mesa de ayuda con escalamiento automático

#### 1.2 Estructura de Flujos

```yaml
Flujos a crear:
- Default Start Flow: Saludo y categorización inicial
- Problem Resolution Flow: Resolución con Knowledge Base
- Escalation Flow: Manejo de escalamientos
- Ticket Creation Flow: Creación de tickets
- Human Handoff Flow: Transferencia a humanos
```

### Fase 2: Knowledge Base Setup

#### 2.1 Configuración de Knowledge Base

**En Dialogflow CX Console:**

1. Ir a "Manage" → "Knowledge"
2. Crear nuevo Knowledge Base: "nombre"
3. Agregar documentos desde Cloud Storage/Upload
4. Configurar extracción automática de FAQ

### Fase 3: Configuración de Firebase

#### 3.1 Configuración de Firestore

```javascript
```

#### 3.2 Reglas de Seguridad de Firestore

```javascript

```

### Fase 4: Desarrollo de Webhooks

#### 4.1 Webhook para Creación de Tickets

```javascript
```

#### 4.2 Webhook para Escalamiento

```javascript
```

### Fase 5: Configuración de Agent Assist

#### 5.1 Habilitar Features de IA

```bash
# Habilitar Agent Assist API
gcloud services enable agentassist.googleapis.com

# Configurar knowledge base para Agent Assist
# Esto se hace desde la consola de Contact Center AI
```

#### 5.2 Features a Configurar

- **Smart Reply**: Sugerencias de respuestas automáticas
- **Article Suggestion**: Sugerencias de artículos relevantes
- **Conversation Summarization**: Resúmenes automáticos
- **Real-time Entity Extraction**: Extracción de entidades en vivo

### Fase 6: Desarrollo de Landing Page

#### 6.1 Estructura HTML Base

```html
```
---
## Mantenimiento y Actualizaciones

### Mantenimiento Rutinario

- **Semanal**: Revisar logs y métricas de performance
- **Mensual**: Actualizar Knowledge Base con nuevos documentos
- **Trimestral**: Revisar y optimizar intents del bot

### Proceso de Actualización

1. **Backup**: Exportar configuración actual
2. **Testing**: Probar cambios en ambiente de staging
3. **Deployment**: Desplegar gradualmente
4. **Monitoring**: Supervisar métricas post-despliegue

---
## Troubleshooting Común

### Problemas Frecuentes

**Bot no entiende las consultas:**

```yaml
Síntomas: Respuestas irrelevantes, fallback frecuente
Solución:
  - Revisar y expandir training phrases
  - Verificar configuración de NLU
  - Añadir más ejemplos de entrenamiento
```

**Tickets no se crean:**

```yaml
Síntomas: Error 500 en webhook, datos no aparecen en Firestore
Solución:
  - Verificar permisos de Firestore
  - Revisar logs de Cloud Functions
  - Validar estructura de datos
```

**Knowledge Base no responde:**

```yaml
Síntomas: "No encontré información relevante"
Solución:
  - Verificar indexación de documentos
  - Revisar formato de PDFs
  - Ajustar configuración de similarity threshold
```