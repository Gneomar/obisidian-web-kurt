---
aliases: [ERP JLV, ERP, typescript-erp-jlv]
tags: [proyecto, erp, fullstack, typescript, destacado]
categoria: Full-Stack / ERP
complejidad: Muy Alta
estado: En desarrollo activo
horas_estimadas: "800-1200h (acumulado 7 versiones)"
---

# ERP JLV - Sistema Empresarial

> [!tip] Proyecto principal
> Este es el proyecto mas grande y complejo del portfolio. Ha evolucionado a traves de **7 iteraciones** durante 2 anos, desde scripts Python hasta un monorepo TypeScript full-stack en produccion.

## Contexto del negocio

Sistema de gestion empresarial (ERP) para **JLV**, empresa del sector bancario/inmobiliario en Peru. Gestiona el ciclo completo de informes bancarios: desde la recepcion de documentos hasta la emision final, con trazabilidad de estados, geolocalizacion de proyectos, y generacion de reportes.

**Dominio funcional:**
- Gestion de **proyectos inmobiliarios** con geolocalizacion
- Ciclo de vida de **informes bancarios**: borrador -> pendiente -> revision -> emitido
- Administracion de **entidades, servicios, promotores y funcionarios**
- **Dashboard con KPIs** y metricas de negocio
- **Importacion masiva** de datos desde Excel/CSV
- **Sistema de roles**: Visitante / Supervisor / Jefe / Administrador
- **Pipeline de datos**: procesamiento de reportes Excel del fileserver

---

## Version actual: typescript-erp-jlv (v7)

**Repositorio:** `Gneomar/typescript-erp-jlv` (privado)
**Ultima actualizacion:** 6 Abril 2026 (activamente desarrollado)
**Horas estimadas (esta version):** ~300-400h

### Arquitectura

```
typescript-erp-jlv/
├── apps/
│   ├── web/                    # Frontend React
│   │   ├── src/
│   │   │   ├── routes/         # File-based routing (TanStack Router)
│   │   │   ├── components/     # UI components (shadcn/ui)
│   │   │   └── lib/            # Utilities
│   │   └── package.json
│   └── server/                 # Backend Elysia
│       ├── src/
│       │   ├── routers/        # tRPC routers
│       │   ├── services/       # Business logic
│       │   └── index.ts        # Entry point
│       └── package.json
├── packages/
│   ├── api/                    # tRPC shared types & router definition
│   ├── auth/                   # Better Auth configuration
│   └── db/                     # Prisma schema & client
├── turbo.json                  # Turborepo pipeline config
├── docker-compose.yml
└── package.json                # Workspace root
```

### Stack tecnico detallado

| Capa | Tecnologia | Justificacion |
|------|-----------|---------------|
| **Runtime** | Bun | 3-5x mas rapido que Node.js para cold start, package manager nativo |
| **Monorepo** | Turborepo | Cache de builds, pipeline paralelo, compatible con Bun |
| **Backend** | Elysia | Framework Bun-native, tipado estatico, ~18x mas rapido que Express |
| **API Layer** | tRPC | Type-safety E2E: cambios en el servidor se reflejan automaticamente en el cliente sin generar schemas |
| **Frontend** | React + TanStack Router | File-based routing con type-safety completo en params y search params |
| **ORM** | Prisma 7.4 | Schema declarativo, migraciones automaticas, autocompletado de queries |
| **Auth** | Better Auth | Auth moderna con email/password, verificacion, sesiones, roles |
| **UI** | TailwindCSS + shadcn/ui | Componentes accesibles y personalizables, no dependen de runtime JS |
| **Mapas** | Leaflet | Mapas interactivos para geolocalizacion de proyectos inmobiliarios |
| **Graficos** | Recharts | Visualizacion de KPIs y metricas de negocio |
| **PDF** | react-pdf-viewer | Visualizacion de informes bancarios directamente en la app |
| **Linting** | Biome | Reemplazo de ESLint + Prettier, ~35x mas rapido |
| **Testing** | Playwright | E2E testing con screenshots y assertions visuales |
| **DB** | PostgreSQL | Base de datos principal para todos los datos del ERP |
| **Deploy** | Docker + Cloudflare | Containerizado con acceso seguro via Cloudflare Tunnels |

### Funcionalidades implementadas

- **Pipeline de datos**: Procesamiento de archivos Excel del fileserver (`pipeline_data`, `pipeline_excel`)
- **Reporte BCP**: Generacion de reportes especificos para el Banco de Credito del Peru
- **Mapa interactivo**: Leaflet con marcadores de proyectos inmobiliarios, filtrado por zona
- **Visor de PDF**: Visualizacion de informes bancarios sin salir de la app
- **Dashboard con graficos**: Recharts con metricas de negocio
- **Autenticacion SMTP/Outlook**: Login con verificacion de email via Nodemailer
- **Roles granulares**: 4 niveles de acceso con permisos diferenciados

### Patrones de diseno

- **Monorepo con workspaces**: Codigo compartido entre backend y frontend via `packages/`
- **Type-safety E2E**: El tipo de retorno del backend es automaticamente el tipo de input del frontend gracias a tRPC
- **Separation of concerns**: Routers (HTTP) -> Services (logica) -> Prisma (data)
- **File-based routing**: Cada archivo en `routes/` genera automaticamente una ruta

---

## Version de produccion anterior: erp-jlv-django-react (v6.5)

**Repositorio:** `Gneomar/erp-jlv-django-react` (privado)
**Periodo:** Enero - Marzo 2026
**Horas estimadas:** ~200-300h

### Arquitectura de produccion

```
Docker Compose (produccion):
┌─────────────────────────────────────────────┐
│                   Nginx                      │
│            (reverse proxy + static)          │
├──────────────────┬──────────────────────────┤
│   React (build)  │     Django API           │
│   Static files   │     (Gunicorn)           │
│                  │         │                 │
│                  │    ┌────┴────┐            │
│                  │    │  Redis  │            │
│                  │    └────┬────┘            │
│                  │         │                 │
│                  │   ┌─────┴──────┐         │
│                  │   │ PostgreSQL │         │
│                  │   └────────────┘         │
│                  │                           │
│                  │   ┌────────────┐         │
│                  │   │ Scheduler  │         │
│                  │   │ (sync job) │         │
│                  │   └────────────┘         │
└──────────────────┴──────────────────────────┘
```

**Stack:** Django 6.0, DRF, SimpleJWT, React 19, TypeScript 5.9, Vite 7.3, PostgreSQL 16, Redis, Nginx, Gunicorn, Docker, GitHub Actions

**Caracteristicas de produccion:**
- **GitHub Actions CI/CD**: Build automatico y despliegue
- **Scheduler**: Proceso background para sincronizacion periodica de datos
- **Redis**: Cache de sesiones y datos frecuentes
- **Nginx**: Reverse proxy, servir static files del frontend
- **Gunicorn**: WSGI server para Django con workers
- **Documentacion**: QUICKSTART.md, deployment guide, plan estrategico

---

## Linea evolutiva completa

| Version | Periodo | Repo | Stack | Salto clave |
|---------|---------|------|-------|-------------|
| v1 | May-Jun 2024 | Sistema-modelo-JLV, Sistema-bbdd-JLV | Python, pandas, PostgreSQL | Scripts ETL, primer pipeline de datos |
| v2 | Oct-Nov 2024 | Django-proyect-jlv | Django 5.1, PostgreSQL | Transicion de scripts a web app |
| v3 | Jun 2025 | django-web-erp2 | Django, Docker | Containerizacion, dashboard |
| v4 | Ago-Sep 2025 | django-erp-jlv-v2 | Django, Docker | Detalle de informes, formularios |
| v4.5 | Oct 2025 | erp-spa | NestJS, React, TypeORM | Experimento SPA (abandonado) |
| v5 | Sep-Dic 2025 | django-erp-v3 | Django, TailwindCSS, Cloudflare | Auth email, roles, UI moderna |
| v6 | Dic 2025-Ene 2026 | django-react-erp | DRF, React 19, TypeScript | Separacion frontend/backend |
| v6.5 | Ene-Mar 2026 | erp-jlv-django-react | DRF, React, Redis, Nginx, GH Actions | **Produccion real**, CI/CD |
| **v7** | **Mar 2026-presente** | **typescript-erp-jlv** | **Elysia, tRPC, Prisma, Bun, Turborepo** | **Type-safety E2E, monorepo moderno** |

### Que demuestra esta evolucion

1. **Capacidad de refactoring a gran escala**: No tiene miedo de reescribir cuando la arquitectura lo justifica
2. **Evaluacion critica de tecnologias**: Probo NestJS, lo evaluo y lo descarto en favor de Elysia por rendimiento y simplicidad
3. **Progresion hacia produccion**: Cada version agrega aspectos de produccion (Docker -> Nginx -> Redis -> CI/CD -> Cloudflare)
4. **Type-safety como prioridad**: La version final prioriza tipado estatico end-to-end sobre velocidad de desarrollo
