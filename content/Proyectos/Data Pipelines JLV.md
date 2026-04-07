---
aliases: [Data Pipelines, ETL JLV, airflow-ETL-JLV]
tags: [proyecto, data-engineering, airflow, etl]
categoria: Data Engineering
complejidad: Alta
estado: Produccion
horas_estimadas: "100-150h"
---

# Data Pipelines JLV

> Pipelines ETL con Airflow para el ecosistema JLV, con soporte para ejecucion distribuida via Celery.

## Contexto

Pipeline ETL basado en Apache Airflow que procesa datos geoespaciales y archivos Excel del fileserver de JLV. Predecesor de [[Airflow ETL Bancos]], enfocado en datos generales (no solo bancarios).

## Repositorio

`Gneomar/airflow-ETL-JLV` (privado)
**Periodo:** Diciembre 2025 - Marzo 2026

## Stack tecnico

| Componente | Tecnologia |
|-----------|-----------|
| **Orquestador** | Apache Airflow |
| **Executor** | LocalExecutor + **CeleryExecutor** |
| **Procesamiento** | pandas, geopandas, openpyxl, xlrd, pyarrow |
| **Auth** | MSAL (Microsoft Azure AD) |
| **DB** | PostgreSQL, MongoDB (pymongo) |
| **Deploy** | Docker Compose (3 variantes) |

## Variantes de despliegue

```
docker-compose.yml          → Standard (LocalExecutor)
docker-compose-celery.yml   → Distribuido (CeleryExecutor + workers)
docker-compose-test.yml     → Testing
```

### CeleryExecutor
Configuracion para ejecucion distribuida de tareas. Permite escalar horizontalmente agregando workers, util cuando el volumen de archivos a procesar crece.

## Caracteristicas tecnicas

- **Procesamiento geoespacial**: geopandas para datos con coordenadas
- **Autenticacion MSAL**: Acceso al fileserver via Azure AD
- **Estructura modular**: `src/dags/`, `src/config/`, `src/lib/`
- **Integracion con Claude Code**: AGENTS.md y directorio `.claude/`
- **rsync para deploy**: `.rsyncignore` para sincronizar DAGs al servidor

## Relacion con otros proyectos

- Precursor de [[Airflow ETL Bancos]] (version mas especializada)
- Consume datos del fileserver via [[JLV Airflow System]]
- Alimenta al [[ERP JLV - Sistema Empresarial]]
