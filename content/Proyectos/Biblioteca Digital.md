---
aliases: [Biblioteca, biblioteca, biblioteca-HK]
tags: [proyecto, fullstack, typescript, monorepo, destacado]
categoria: Full-Stack / Monorepo
complejidad: Alta
estado: Completado
horas_estimadas: "80-100h (por version)"
---

# Biblioteca Digital

> [!tip] Monorepo de practica
> Dos implementaciones del mismo proyecto con stacks ligeramente diferentes, usadas como laboratorio para evaluar tecnologias antes de aplicarlas al [[ERP JLV - Sistema Empresarial]].

## Contexto

Sistema de gestion de biblioteca digital implementado dos veces con variaciones en el ORM y el framework de routing. Sirvio como banco de pruebas para decidir el stack del ERP v7.

## Version 1: biblioteca

**Repositorio:** `Gneomar/biblioteca` (privado)
**Fecha:** Marzo 2026

### Stack
| Capa | Tecnologia |
|------|-----------|
| Runtime | Bun |
| Monorepo | Turborepo |
| Backend | Elysia |
| API | tRPC |
| ORM | **Prisma** |
| Frontend | React + **TanStack Router** (SPA) |
| Auth | Better Auth |
| UI | TailwindCSS + shadcn/ui |
| Linting | Biome |
| Deploy | Docker Compose |

### Estructura
```
biblioteca/
├── apps/
│   ├── web/          # React + TanStack Router
│   └── server/       # Elysia + tRPC
├── packages/
│   ├── api/          # tRPC router definitions
│   ├── auth/         # Better Auth config
│   └── db/           # Prisma schema + client
└── turbo.json
```

## Version 2: biblioteca-HK

**Repositorio:** `Gneomar/biblioteca-HK` (privado)
**Fecha:** Marzo 2026

### Diferencias con v1

| Aspecto | biblioteca (v1) | biblioteca-HK (v2) |
|---------|----------------|---------------------|
| **ORM** | Prisma | **Drizzle** (mas ligero) |
| **Routing** | TanStack Router (SPA) | **TanStack Start (SSR)** |
| **Testing** | Sin tests | **Playwright E2E** |
| **Rendering** | Client-side only | **Server-side rendering** |

### Motivacion de las diferencias

- **Prisma vs Drizzle**: Prisma tiene mejor DX y ecosistema mas maduro, pero Drizzle es mas ligero y genera menos overhead en runtime. Se evaluo cual era mas adecuado para el ERP → **Prisma gano** (usado en typescript-erp-jlv)
- **TanStack Router vs TanStack Start**: Router es SPA puro, Start agrega SSR. Se evaluo si el ERP necesitaba SSR → **Router gano** (el ERP es una app interna, no necesita SEO)
- **Playwright**: Se incorporo a v2 para validar que el testing E2E funcionara con el stack → **Adoptado** en el ERP

## Que lo hace destacable

- **Evaluacion metodica de tecnologias**: No adopta herramientas a ciegas — construye prototipos funcionales para comparar
- **Documentacion de decisiones**: Las dos versiones sirven como registro de por que se eligio Prisma sobre Drizzle y Router sobre Start
- **Stack identico al ERP**: El stack ganador es el que se uso en [[ERP JLV - Sistema Empresarial]] v7
