---
{"dg-publish":true,"permalink":"/Fundamentos TI/AI essentials/GenAI/03 Architecture and security/"}
---

Por defecto, google guarda la información encriptada. Si debemos cumplir normativas regulatorias especiales relacionadas a como se manejan dichas llaves... Customer Managed Encryption Keys (CMEK)

#### CMEK
Para necesidades regulatorias o de cumplimiento con [[Ciberseguridad/Habilidades y conocimientos básicos/Normativas y Estándares/Otras normativas e información susceptible\|normativas]].

Limitaciones:
- No se pueden cambiar las llaves, rotadas o removidas cuando se registran.
- Sólo soporta almacenamiento en ciertas regiones
- La información no puede ser retroactivamente protegida
- Requiere edición enterprise

Cualquier Acceso realizado está en los logs y es traceable.
Se respetan los controles VPC y de residencia.
Siempre están protegidas en tránsito.
La información está aislada.

#### LLM Specific Security
- Modelos sin estado o congelados que no almacenan datos, incluyendo los parámetros específicos de cliente.
- Se pueden procesar datos cloud alternativos pero deben ser pre-procesados 

---

# Precio

Consideraciones para elegir un modelo de texto:
Context window
- PaLM hasta 32k caracteres
- Gemini hasta 1M de caracteres
Tamaño del modelo:
PaLM
- Gecko
- Bison
- Unicorn
Precisión:
- PaLM y Gemini 1.0 dan precisión similar
- Gemini 1.5 puede ser más preciso
Multi modalidad:
- PaLM sólo texto
- Gemini es multimodal

Vertex AI Search:
Indexing para guardar datos = $5/GiB por mes (primeros 10GiB gratis)
Servicio cobra por el número de queries
- Standard (no estructurado) $2 por 1k queries
- Enterprise (website + no estructurado) $4 por 1k queries
Search LLM ADD-ON (summarization) $4 adicionales por 1k queries

Standard vs Enterprise:
Standard: estructurado y no estructurado, search LLM add-on (summarization y multi-turn), búsquedas mejoradas con snippets
Enterprise: más fuentes de búsqueda y de indexación, seguridad avanzada (CMEK, Access control lists), resultados de búsqueda mejorados.

---

# Situación Competitiva

- Evitar las comparaciones de modelos unos con otros. Todos responden a distintas necesidades y hay que ajustarse a lo necesario para balancear costos vs necesidades
- Enfocarse en el valor de la plataforma de manera extensa y a largo plazo
- Empresas necesitan el grado empresarial para evitar problemas de todo tipo
- Ciclo de vida de ML en mente
- Evitar el hype

