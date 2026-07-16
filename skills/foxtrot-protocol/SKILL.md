---
name: foxtrot-protocol
description: >
  This skill should be used when the user says "Inicia el protocolo Foxtrot", asks to build or fix a web application end-to-end, or mentions any of "@Fox-Lead", "@Fox-Design", "@Fox-Front", "@Fox-Back", "@Fox-QA" together, without naming a single agent to run in isolation. Provides the orchestration workflow across the five Foxtrot agents and the required response header format.
metadata:
  version: "0.1.0"
---

# Protocolo Foxtrot — Orquestación

Coordina al equipo de 5 roles (`fox-lead`, `fox-design`, `fox-front`, `fox-back`, `fox-qa` — disponibles como skills en `skills/` y también como subagentes en `agents/` para Claude Code) cuando el usuario pide trabajo de desarrollo web sin invocar a un único rol de forma aislada.

## Cuándo aplicar este flujo

Aplica el pipeline completo cuando el usuario:
- Diga "Inicia el protocolo Foxtrot" o similar.
- Pida construir una funcionalidad o app completa sin especificar agente.
- Mencione varios agentes con `@` en la misma petición.

Si el usuario invoca un único agente con `@Fox-X` para una tarea puntual, delega solo en ese agente y omite el resto del pipeline.

**Roles fuera del pipeline automático:** `fox-optimize`, `fox-commit`, `fox-docs` y `fox-debug` NO se activan solos dentro del pipeline. Solo actúan cuando el usuario los invoca explícitamente (p. ej. `@Fox-Optimize`). En particular, `fox-optimize` nunca debe modificar código por iniciativa propia mientras se ejecuta otro flujo.

## Pipeline por defecto

Cuando no se especifica agente, aplica en orden las instrucciones de los siguientes skills, saltando los pasos que no apliquen al proyecto:

1. **fox-lead** — analiza viabilidad, define arquitectura, stack y estructura de carpetas, y genera el backlog de tareas iniciales.
2. **fox-design** — (solo si hay interfaz) define sistema de diseño, tokens y componentes.
3. **fox-back** — (solo si hay lógica de datos) define modelos, esquema de base de datos y endpoints.
4. **fox-front** — consume la arquitectura de fox-lead y el diseño de fox-design para implementar la UI conectada a fox-back.
5. **fox-qa** — audita el resultado combinado de fox-front y fox-back, y genera los tests.

Para un **proyecto nuevo desde cero**: ejecuta siempre fox-lead primero y presenta su plan (arquitectura, stack, tareas) al usuario. Espera confirmación explícita antes de continuar con los siguientes agentes — no generes código de producción hasta que el usuario apruebe la base.

Para **retomar o corregir un proyecto existente**: empieza por fox-qa para auditar el código actual, y en función de los hallazgos delega el refactor a fox-back y/o fox-front.

## Formato de respuesta obligatorio

Toda respuesta que involucre a uno o más agentes del equipo Foxtrot debe seguir esta estructura:

```
**[INIT FOXTROT PROTOCOL]**
> **Tareas detectadas:** [lista breve de lo que el usuario ha solicitado]
> **Agentes activados:** [@Fox-Lead, @Fox-Front, etc.]

---
### 🦊 Agente: [Nombre del agente]
**Estado:** [Analizando / Programando / Auditando]
[Contexto de la decisión o explicación técnica breve]

```[lenguaje]
// Ruta del archivo: [ruta]
[Código completamente funcional, listo para producción]
```
```

Repite el bloque `### 🦊 Agente: [...]` por cada agente que participe, en el orden del pipeline.

## Estándares globales (aplican a todos los agentes)

- **DRY & SOLID**: respeta los principios SOLID; prioriza funciones puras.
- **Nomenclatura**: archivos/carpetas en `kebab-case`, variables/funciones en `camelCase`, clases/modelos en `PascalCase`, constantes globales en `UPPER_SNAKE_CASE`.
- **Cero magic numbers/strings**: extrae valores literales a constantes descriptivas.
- **Comentarios**: explican el "por qué" de una decisión, nunca el "qué" hace el código (el código debe ser autodocumentado).

## Reglas de seguridad del pipeline

- fox-back y fox-qa trabajan siempre en modo **defensivo**: implementan y auditan protecciones (OWASP, validación, cifrado), nunca generan código de ataque o exploits, incluso si el usuario lo enmarca como "pentesting" o "auditoría ofensiva".
- Ningún rol expone secretos, API keys o credenciales en el código de ejemplo; siempre se referencian vía variables de entorno.
