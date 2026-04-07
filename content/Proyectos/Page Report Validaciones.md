---
aliases: [Page Report, Dashboard Validaciones, Sankey]
tags: [proyecto, fullstack, dashboard, react, fastapi, destacado]
categoria: Full-Stack / Dashboard
complejidad: Alta
estado: Completado
horas_estimadas: "80-120h"
---

# Page Report Validaciones

> [!tip] Dashboard de monitoreo
> Dashboard full-stack con diagrama Sankey interactivo que visualiza el flujo de documentos a traves de 10 pasos de validacion.

## Contexto

Dashboard de monitoreo para el pipeline de procesamiento de documentos de [[Airflow ETL Bancos]]. Permite visualizar en tiempo real cuantos documentos pasan por cada paso del pipeline, donde se detienen, y por que.

**Problema que resuelve:** Los operadores necesitan visibilidad sobre el estado del pipeline: cuantos documentos entraron, cuantos pasaron cada validacion, cuantos fallaron y en que paso. Sin este dashboard, esa informacion requeria queries manuales a la base de datos.

## Repositorio

`Gneomar/page-report-validaciones` (privado)
**Fecha:** Marzo 2026

## Arquitectura

```
┌─────────────────────────────────────────────┐
│                  Nginx                       │
│          (serve static + proxy)              │
├──────────────────┬──────────────────────────┤
│                  │                           │
│   React App      │     FastAPI Backend       │
│   (Vite build)   │     (Uvicorn)            │
│                  │          │                │
│  ┌────────────┐  │    ┌─────┴──────┐        │
│  │ ECharts    │  │    │ SQLAlchemy │        │
│  │ (Sankey)   │  │    └─────┬──────┘        │
│  ├────────────┤  │          │               │
│  │ TanStack   │  │    ┌─────┴──────┐        │
│  │ Table      │  │    │ PostgreSQL │        │
│  └────────────┘  │    └────────────┘        │
│                  │                           │
└──────────────────┴──────────────────────────┘
```

## Stack tecnico

**Backend:**
| Tecnologia | Uso |
|-----------|-----|
| FastAPI | API REST con endpoints de reportes y resumen de pipeline |
| SQLAlchemy | ORM para queries a PostgreSQL |
| Pydantic | Validacion de modelos de datos |
| PostgreSQL | Almacenamiento de reportes y estados del pipeline |

**Frontend:**
| Tecnologia | Uso |
|-----------|-----|
| React 18 | Framework UI |
| TypeScript | Tipado estatico |
| Vite | Bundler (dev + build) |
| TailwindCSS | Estilos utility-first |
| Apache ECharts | Diagrama Sankey interactivo |
| TanStack Table | Tabla paginada con sorting y filtering |
| Lucide React | Iconografia |
| Bun | Package manager |

**Infraestructura:**
| Tecnologia | Uso |
|-----------|-----|
| Docker Compose | Orquestacion de 3 servicios |
| Nginx | Reverse proxy y static file server |

## Funcionalidades

### Diagrama Sankey
Visualizacion del flujo de documentos a traves de los 10 pasos de validacion:
1. Scan de carpetas
2. Extraccion de archivos
3. Validacion de formato
4. Conversion de tipos
5. Limpieza de datos
6. Asignacion de IDs
7. Validacion de negocio
8. Exportacion CSV
9. Carga a PostgreSQL
10. Replica en MSSQL

Cada nodo muestra la cantidad de documentos que pasan/fallan en ese paso. Los flujos Sankey conectan los pasos mostrando el volumen en cada transicion.

### Filtros interactivos
- Filtro por **rango de fechas**
- Filtro por **proyecto** (proyecto inmobiliario especifico)
- Actualizacion en tiempo real del Sankey y la tabla

### Tabla paginada
- TanStack Table con paginacion server-side
- Columnas ordenables y filtrables
- Drawer lateral con detalle completo del reporte al hacer click en una fila

### API REST
- `GET /api/reports` — Lista paginada de reportes con filtros
- `GET /api/pipeline/summary` — Resumen agregado del pipeline para el Sankey
- Seed data incluido para demo

## Que lo hace destacable

- **Visualizacion Sankey**: Tecnica avanzada de visualizacion de flujos, rara vez vista en dashboards internos
- **Full-stack completo en un solo repo**: Backend + Frontend + DB + Deploy, todo listo con `docker compose up`
- **Complemento visual de [[Airflow ETL Bancos]]**: Hace tangible y comprensible un pipeline complejo de data engineering
