---
aliases: [Airflow ETL, ETL Bancos, Pipeline Bancos]
tags: [proyecto, data-engineering, airflow, etl, destacado]
categoria: Data Engineering
complejidad: Muy Alta
estado: En desarrollo activo
horas_estimadas: "250-350h"
---

# Airflow ETL Bancos

> [!tip] Pipeline de produccion
> El pipeline ETL mas complejo del portfolio. Procesa reportes financieros bancarios con 20+ tipos de tablas y 458+ columnas codificadas.

## Contexto del negocio

Pipeline automatizado que procesa **informes financieros bancarios** recibidos como archivos Excel en un fileserver. El sistema escanea carpetas, valida formatos, calcula indicadores derivados, y carga los datos en PostgreSQL (base primaria) y MSSQL (replica para Power BI).

**Problema que resuelve:** Antes de este sistema, el procesamiento de cientos de reportes Excel era manual, propenso a errores y consumia horas de trabajo. El pipeline automatiza todo el ciclo: deteccion de archivos -> validacion -> transformacion -> carga -> replicacion.

## Repositorio

`Gneomar/Airflow-ETL-Bancos` (privado)
**Ultima actualizacion:** 7 Abril 2026 (hoy — activamente desarrollado)

## Arquitectura del pipeline

```
Fileserver (Excel)
       │
       ▼
┌──────────────────────────────────────────────────┐
│              Apache Airflow 2.10.4                │
│                                                    │
│  DAG 1: extract_validate_formato                   │
│    └─ Escanea carpetas, extrae Excel, valida       │
│       formato contra diccionario maestro           │
│                    │                               │
│  DAG 2: informes_rev                               │
│    └─ 7 pasos de validacion:                       │
│       1. Convertir a Parquet                       │
│       2. Ajustar columnas                          │
│       3. Limpiar datos                             │
│       4. Convertir tipos                           │
│       5. Asignar IDs                               │
│       6. Validar reglas de negocio                 │
│       7. Exportar CSV + JSON                       │
│                    │                               │
│  DAG 3: directory_explorer_v2                      │
│    └─ Procesamiento geoespacial, calculos          │
│       derivados, carga a PostgreSQL (upsert)       │
│                    │                               │
│  DAG 4: replicate_mssql                            │
│    └─ Replica de PostgreSQL a MSSQL para Power BI  │
└──────────────────────────────────────────────────┘
       │                              │
       ▼                              ▼
  PostgreSQL                     MSSQL (replica)
  (primaria)                     (Power BI)
       │
       ▼
    MongoDB
    (logs de
    validacion)
```

## Stack tecnico

| Componente | Tecnologia | Detalle |
|-----------|-----------|---------|
| **Orquestador** | Apache Airflow 2.10.4 | DAGs Python, scheduler, web UI |
| **Contenedores** | Docker Compose | Airflow + PostgreSQL + workers |
| **DB primaria** | PostgreSQL | Almacenamiento principal de datos procesados |
| **DB replica** | MSSQL | Replica para consumo desde Power BI |
| **DB logs** | MongoDB | Registro de validaciones y errores |
| **Procesamiento** | pandas, geopandas | Transformaciones de datos, geoespacial |
| **Archivos** | openpyxl, xlrd, pyarrow | Lectura Excel, conversion Parquet |
| **Auth Microsoft** | MSAL | Autenticacion Azure AD para fileserver |
| **DB drivers** | psycopg2, pymssql, pyodbc, pymongo | Conexion a las 3 bases de datos |
| **Config** | python-dotenv | Variables de entorno |
| **Deploy** | rsync | Sincronizacion de DAGs al servidor |

## Detalles tecnicos

### Escala de datos
- **20+ tipos de tablas** con esquemas diferentes
- **458+ columnas** codificadas en un diccionario maestro Excel
- **Procesamiento batch**: lotes de 10/30/8 archivos con 5/3 hilos paralelos
- **10 pasos de maquina de estados** para el ciclo de vida de cada documento

### Esquema SQL versionado
```
sql/
├── 01_meta.sql          # Tablas de metadatos
├── 02_core.sql          # Tablas de negocio principales
├── 03_indexes.sql       # Indices de rendimiento
├── 04_views.sql         # Vistas de consulta
├── 05_functions.sql     # Funciones SQL
└── 06_migrations.sql    # Migraciones incrementales
```

### Calculos implementados
- Conversion monetaria PEN/USD con tipo de cambio dinamico
- Codigos mensuales para series temporales
- Indicadores derivados de datos bancarios
- Calculos geoespaciales (geopandas) para ubicacion de proyectos

### Variantes de despliegue
- `docker-compose.yml` — Standard con LocalExecutor
- `docker-compose-celery.yml` — Distribuido con CeleryExecutor + workers
- `docker-compose-test.yml` — Entorno de testing

### Integracion con IA
- `CLAUDE.md` detallado para desarrollo asistido con Claude Code
- Documentacion del dominio de negocio para contexto de IA

## Relacion con otros proyectos

- Alimenta de datos al [[ERP JLV - Sistema Empresarial]]
- Comparte infraestructura con [[JLV Airflow System]]
- Replica datos a MSSQL que se consumen desde Power BI
- Evolucion de [[Data Pipelines JLV]] (versiones anteriores)
