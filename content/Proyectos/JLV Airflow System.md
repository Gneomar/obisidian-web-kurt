---
aliases: [JLV System, Hub JLV, Infraestructura JLV]
tags: [proyecto, infraestructura, fullstack, docker, destacado]
categoria: Infraestructura / Full-Stack
complejidad: Alta
estado: Produccion
horas_estimadas: "150-200h"
---

# JLV Airflow System

> [!tip] Hub de infraestructura
> Sistema centralizado que orquesta 7 contenedores Docker interconectados: backend, frontend, triple base de datos, y herramientas de administracion.

## Contexto

Hub principal de infraestructura del ecosistema JLV. Centraliza todos los servicios de datos en una sola red Docker: API REST para consumo de datos, frontend para visualizacion, y tres motores de base de datos para diferentes necesidades.

**Problema que resuelve:** La empresa JLV operaba con datos dispersos en Excel, SQL Server local y scripts sueltos. Este sistema centraliza todo en una infraestructura containerizada, accesible via API y frontend web.

## Repositorio

`Gneomar/JLV-Airflow-System` (privado)
**Periodo:** Julio - Noviembre 2025

## Arquitectura de servicios

```
Docker Compose — 7 contenedores en red "holared":

┌──────────────────────────────────────────────────────┐
│                                                       │
│  ┌──────────────┐    ┌──────────────┐                │
│  │ React App    │    │ FastAPI      │                │
│  │ (Nginx)      │───▶│ (Backend)    │                │
│  │ :3000        │    │ :8000        │                │
│  └──────────────┘    └──────┬───────┘                │
│                             │                         │
│         ┌───────────────────┼───────────────┐        │
│         │                   │               │        │
│  ┌──────┴──────┐  ┌───────┴──────┐  ┌─────┴──────┐ │
│  │ PostgreSQL  │  │ SQL Server   │  │  MongoDB   │ │
│  │ 15          │  │ Express      │  │  4.4       │ │
│  │ :5432       │  │ :1433        │  │  :27017    │ │
│  └─────────────┘  └──────────────┘  └─────┬──────┘ │
│                                            │        │
│  ┌─────────────┐                    ┌──────┴──────┐ │
│  │ postgres-api│                    │Mongo Express│ │
│  │ (secundaria)│                    │ (Admin UI)  │ │
│  │ :8001       │                    │ :8081       │ │
│  └─────────────┘                    └─────────────┘ │
│                                                       │
│  Fileserver montado en /mnt/fileserver (read-only)   │
└──────────────────────────────────────────────────────┘
```

## Stack tecnico

| Servicio | Tecnologia | Puerto | Funcion |
|----------|-----------|--------|---------|
| **react** | React + Nginx | 3000 | Frontend web para visualizacion de datos |
| **fastapi** | FastAPI + SQLAlchemy + SQLModel | 8000 | API REST principal con autenticacion JWT |
| **postgres** | PostgreSQL 15 | 5432 | Base de datos relacional principal |
| **sqlserver** | MSSQL Express | 1433 | Base de datos para compatibilidad con Power BI |
| **mongodb** | MongoDB 4.4 | 27017 | Almacenamiento de documentos y logs |
| **mongo-express** | Mongo Express | 8081 | UI de administracion de MongoDB |
| **postgres-api** | FastAPI | 8001 | API secundaria para consultas PostgreSQL |

**Backend detallado:**
- FastAPI con async handlers
- SQLAlchemy + SQLModel como ORMs
- Pydantic para validacion
- PyJWT + bcrypt para autenticacion
- asyncpg para conexion async a PostgreSQL

## Detalles tecnicos

### Red Docker externa
Los servicios comparten una red Docker externa (`holared`), permitiendo que otros servicios (como los DAGs de Airflow) se conecten a las bases de datos sin duplicar contenedores.

### Fileserver montado
El fileserver corporativo se monta como volumen en solo lectura (`/mnt/fileserver`), permitiendo que el backend acceda a archivos Excel sin copiarlos.

### Scripts de mantenimiento
Scripts de limpieza Docker incluidos para mantenimiento de contenedores, imagenes y volumenes.

## Relacion con el ecosistema

- Provee las bases de datos que consume [[Airflow ETL Bancos]]
- Alimenta de datos al [[ERP JLV - Sistema Empresarial]]
- Los logs de validacion de [[Data Pipelines JLV]] se almacenan en el MongoDB de este sistema
- La replica MSSQL alimenta dashboards Power BI del equipo de negocio
