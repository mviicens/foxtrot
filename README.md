# Foxtrot: Devops Web Plugin for Claude

Equipo de agentes de IA especializados en **desarrollo web** full-stack, orquestados bajo un protocolo único con estándares de código y formato de salida consistentes.

**Autor:** mviicens

> **Enfoque:** Foxtrot está orientado exclusivamente a proyectos de **desarrollo web** (aplicaciones y sitios web). Su stack (Next.js, React, Tailwind, Node.js/Go, PostgreSQL, etc.) y sus roles están pensados para construir, auditar y optimizar software para la web, no para otros dominios (móvil nativo, escritorio, embebidos, data science, etc.).

## Visión general

Este plugin convierte a Claude en un equipo de ingeniería web senior compuesto por roles especializados que colaboran siguiendo un pipeline definido, en lugar de responder como un asistente genérico.

## Componentes

### Skills del pipeline (`skills/`)

Se ejecutan en orden dentro del protocolo cuando construyes o arreglas una app:

| Skill        | Rol                                | Stack principal                                                  |
| ------------ | ---------------------------------- | ---------------------------------------------------------------- |
| `fox-lead`   | Project Manager & Cloud Architect  | Git, GitHub Actions, Docker Compose, Terraform, Turborepo         |
| `fox-design` | UI/UX & Accesibilidad (A11y)       | Tailwind CSS, shadcn/ui, Radix UI, Figma Tokens, Lucide Icons     |
| `fox-front`  | Senior Frontend Engineer           | Next.js (App Router), React 18+, TypeScript strict, Zustand/TanStack Query |
| `fox-back`   | Senior Backend & Security Engineer | Node.js (Hono/NestJS) o Golang, PostgreSQL, Prisma/Drizzle, Supabase, Zod |
| `fox-qa`     | QA Engineer & SecOps               | Vitest, Playwright, Supertest, ESLint                             |

### Skills bajo demanda (solo con invocación explícita)

No forman parte del pipeline automático; se activan solo cuando las llamas directamente:

| Skill          | Qué hace                                                                             |
| -------------- | ------------------------------------------------------------------------------------ |
| `fox-optimize` | Verifica y optimiza código existente: elimina variables/imports muertos, reformula procesos para mayor eficiencia (complejidad, memoria, renders), preservando el comportamiento. |
| `fox-commit`   | Redacta mensajes de commit (Conventional Commits) y descripciones de pull request.   |
| `fox-docs`     | Genera documentación técnica: README, referencia de API y documentación inline.      |
| `fox-debug`    | Diagnostica errores, stack traces y fallos de build/test, y propone la corrección mínima. |

### Orquestación

- `foxtrot-protocol` — define el pipeline entre roles (nuevo proyecto vs. proyecto existente) y el formato de respuesta obligatorio (`[INIT FOXTROT PROTOCOL]`).

### Agentes (`agents/`)

Los mismos roles están también disponibles como subagentes en formato `agents/*.md`, útiles en **Claude Code**, donde los subagentes se ejecutan como tareas delegadas con su propio contexto.

## Instalación

Hay dos formas de instalar Foxtrot según el cliente que uses. En ambos casos se instala la **estructura de carpetas** del plugin (`.claude-plugin/`, `agents/`, `skills/`); el archivo empaquetado `.plugin` es solo un formato de distribución para la instalación manual, no debe subirse al repositorio.

### Claude Code (desde este repositorio)

Claude Code lee la estructura de carpetas del repo directamente (busca `.claude-plugin/plugin.json`). No uses el archivo `.plugin` aquí. La sintaxis general es:

```bash
/plugin marketplace add mviicens/foxtrot
/plugin install foxtrot@foxtrot
```

> La función de plugins de Claude Code evoluciona con frecuencia y los nombres exactos de los comandos pueden cambiar. Confirma la sintaxis vigente en la documentación oficial: https://docs.claude.com

### Claude Cowork (instalación manual)

Descarga el archivo empaquetado `foxtrot.plugin` e instálalo desde la propia interfaz de Cowork (opción de añadir/instalar plugin). Este es el único caso donde se usa el `.plugin`.

## Uso

- **Proyecto nuevo:** "Inicia el protocolo Foxtrot. Quiero crear [tu idea]. @Fox-Lead, define la arquitectura, el stack y las tareas iniciales." → arranca el pipeline empezando por `fox-lead`.
- **Rol puntual:** "@Fox-Design, revisa la accesibilidad de este formulario."
- **Optimizar código:** "@Fox-Optimize, limpia y optimiza esta función."
- **Proyecto existente:** "Inicia el protocolo Foxtrot. @Fox-QA, audita este código."

## Notas de seguridad

`fox-back`, `fox-qa` y `fox-optimize` operan siempre en modo defensivo: implementan, auditan y mejoran protecciones de seguridad (OWASP, validación de inputs, cifrado), pero no generan código ofensivo, exploits ni backdoors bajo ninguna circunstancia.
