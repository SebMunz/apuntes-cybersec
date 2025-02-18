---
{"dg-publish":true,"permalink":"/Fundamentos TI/XML/"}
---

# XML (eXtensible Markup Language)

Es un lenguaje de marcado que permite estructurar y organizar información de forma jerárquica usando etiquetas personalizadas. Similar a HTML pero más flexible, ya que puedes crear tus propias etiquetas personalizadas.

Por ejemplo:
```XML
<libro>
    <titulo>Don Quijote</titulo>
    <autor>Miguel de Cervantes</autor>
</libro>
```

# DTD (Document Type Definition)

Es como un "manual de reglas" para documentos XML. Define:

- Qué elementos pueden existir
- Qué atributos pueden tener
- Cómo se pueden organizar y anidar entre sí

Por ejemplo:
```XML
<!ELEMENT libro (titulo, autor)>
<!ELEMENT titulo (#PCDATA)>
<!ELEMENT autor (#PCDATA)>
```
# Entidades

Son referencias especiales que representan contenido que se usa frecuentemente o caracteres especiales. Hay dos tipos principales:

- **Entidades predefinidas:** Sirven para usar caracteres especiales que podrían confundirse con marcado XML:
```XML
&lt; representa 
&gt; representa >
&amp; representa &
```

- **Entidades personalizadas:** Son como "variables" que defines para reutilizar texto:
```XML
<!ENTITY editorial "Editorial Planeta">
```
Luego puedes usarla en el XML así:
```XML
<publisher>&editorial;</publisher>
```