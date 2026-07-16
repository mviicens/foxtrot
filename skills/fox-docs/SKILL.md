---
name: fox-docs
description: >
  This skill should be used when the user asks to "documenta este código", "escribe el README", "genera la documentación de la API", "añade JSDoc/docstrings", or needs clear technical documentation (README, API reference, inline docs) consistent with the Foxtrot standards.
metadata:
  version: "0.1.0"
---

# Fox-Docs — Technical Documentation

Genera documentación técnica clara, concisa y mantenible para el código y los proyectos del equipo Foxtrot.

## Instrucciones

1. **README de proyecto.** Incluye, en este orden: título y descripción de una frase, requisitos previos, instalación, uso básico con ejemplos, estructura de carpetas (árbol ASCII si aporta), scripts disponibles, variables de entorno necesarias (sin valores reales) y licencia.
2. **Documentación de API.** Por cada endpoint documenta: método y ruta, descripción, parámetros/body (con tipos), respuestas posibles (códigos y forma del JSON) y un ejemplo de petición/respuesta.
3. **Documentación inline (JSDoc/TSDoc/docstrings).** Documenta el "por qué" y los contratos (parámetros, retorno, excepciones), no reexpliques línea a línea lo que el código ya dice.
4. **Tono.** Directo y práctico. Frases cortas. Ejemplos ejecutables siempre que sea posible.
5. **Nunca inventes** comportamiento que no esté en el código: si algo no está claro, márcalo con un `TODO:` en vez de suponer.

## Reglas

- No incluyas secretos, tokens ni credenciales reales en la documentación; usa placeholders como `<TU_API_KEY>`.
- Mantén la documentación sincronizada con el código: si documentas algo que contradice el código, avisa.

## Formato de salida

Entrega la documentación en markdown (`.md`) listo para guardar, o como bloque de comentarios en el lenguaje correspondiente si es documentación inline.
