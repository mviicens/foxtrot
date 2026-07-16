---
name: fox-commit
description: >
  This skill should be used when the user asks to "escribe el mensaje de commit", "genera un commit", "prepara la PR", "descripción de pull request", or needs help writing Conventional Commits messages or pull request descriptions consistent with the Foxtrot standards.
metadata:
  version: "0.1.0"
---

# Fox-Commit — Conventional Commits & PR Descriptions

Ayuda a redactar mensajes de commit y descripciones de pull request coherentes con los estándares del equipo Foxtrot.

## Conventional Commits

Formato: `<tipo>(<ámbito opcional>): <descripción en imperativo y minúscula>`

Tipos permitidos:
- `feat`: nueva funcionalidad para el usuario.
- `fix`: corrección de un bug.
- `refactor`: cambio de código que no corrige un bug ni añade funcionalidad.
- `perf`: cambio que mejora el rendimiento.
- `docs`: solo documentación.
- `style`: formato, punto y coma, etc. (sin cambios de lógica).
- `test`: añadir o corregir tests.
- `chore`: tareas de mantenimiento, dependencias, build.
- `ci`: cambios en configuración de CI/CD.

Reglas:
1. La descripción va en imperativo, en minúscula y sin punto final: `feat(auth): añade login con OAuth2`.
2. Si hay breaking change, añade `!` tras el tipo/ámbito y una sección `BREAKING CHANGE:` en el cuerpo.
3. El cuerpo (opcional) explica el "por qué" del cambio, no el "qué".
4. Referencia issues al final: `Refs #123` o `Closes #123`.

## Descripción de Pull Request

Estructura recomendada:

```
## Qué

[Resumen de una o dos frases de lo que hace la PR]

## Por qué

[Motivación / problema que resuelve]

## Cómo probarlo

- [ ] Paso 1
- [ ] Paso 2

## Checklist

- [ ] Tests añadidos/actualizados
- [ ] Sin `any` en TypeScript
- [ ] Inputs validados (si aplica)
- [ ] Documentación actualizada (si aplica)
```

## Formato de salida

Devuelve el mensaje de commit en un bloque de código listo para copiar, y la descripción de PR en markdown aparte si se solicita.
