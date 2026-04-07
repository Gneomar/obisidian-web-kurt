---
aliases: [Nexo Scrapeo, Scraper Inmobiliario]
tags: [proyecto, scraping, ai, fastapi, destacado]
categoria: Scraping / AI
complejidad: Alta
estado: Reciente
horas_estimadas: "120-160h"
---

# Nexo Scrapeo - Pipeline Inmobiliario

> [!tip] Scraping + Busqueda Semantica
> Pipeline profesional que combina web scraping con busqueda vectorial usando embeddings de Sentence-Transformers y Qdrant.

## Contexto

Nexo Inmobiliario es uno de los principales portales inmobiliarios de Peru. Este proyecto extrae datos de proyectos inmobiliarios (precios, ubicaciones, tipologias, imagenes) y los almacena de forma estructurada, habilitando **busqueda semantica** sobre los datos extraidos.

**Problema que resuelve:** El analisis de mercado inmobiliario requiere datos actualizados de multiples fuentes. Este pipeline automatiza la extraccion, almacenamiento y busqueda inteligente sobre miles de proyectos inmobiliarios.

## Repositorio

`Gneomar/nexo-scrapeo` (privado)
**Fecha:** Marzo 2026

## Arquitectura

```
Docker Compose (5 servicios):

┌─────────────────────────────────────────┐
│              FastAPI App                 │
│  ┌──────────┐  ┌───────────────────┐   │
│  │ Scraper   │  │ Search Engine     │   │
│  │ Playwright│  │ Sentence-         │   │
│  │ + BS4     │  │ Transformers      │   │
│  └─────┬─────┘  └────────┬──────────┘   │
│        │                 │               │
└────────┼─────────────────┼───────────────┘
         │                 │
    ┌────┴────┐      ┌────┴────┐
    │ MongoDB │      │ Qdrant  │
    │ (datos) │      │(vectors)│
    └─────────┘      └─────────┘
         │
    ┌────┴──────────┐
    │ Mongo Express  │
    │ (admin UI)     │
    └────────────────┘
         │
    ┌────┴──────────┐
    │  PostgreSQL    │
    │ (relacional)   │
    └────────────────┘
```

## Stack tecnico

| Componente | Tecnologia | Uso |
|-----------|-----------|-----|
| **API** | FastAPI | Endpoints REST para scraping y busqueda |
| **Scraping** | Playwright | Navegador headless para sitios con JS dinámico |
| **Parsing** | BeautifulSoup + lxml | Extraccion de datos del HTML |
| **HTTP** | httpx | Requests async para APIs |
| **Embeddings** | Sentence-Transformers | Generacion de vectores semanticos de texto |
| **Vector DB** | Qdrant | Almacenamiento y busqueda por similitud coseno |
| **Document DB** | MongoDB (Motor) | Almacenamiento de datos scrapeados (async) |
| **Relational DB** | PostgreSQL (asyncpg + SQLAlchemy async) | Datos estructurados |
| **Migraciones** | Alembic | Versionado de esquema PostgreSQL |
| **Validacion** | Pydantic | Modelos tipados para request/response |
| **Testing** | pytest | Tests automatizados |
| **Deploy** | Docker Compose | 5 servicios orquestados |

## Flujo de scraping

1. **Request** -> Endpoint FastAPI recibe URL o criterios de busqueda
2. **Scrape** -> Playwright navega el sitio, maneja paginacion y lazy-loading
3. **Parse** -> BeautifulSoup + lxml extraen datos estructurados (precio, ubicacion, tipologia, m2, imagenes)
4. **Store** -> Datos crudos a MongoDB, datos relacionales a PostgreSQL
5. **Embed** -> Sentence-Transformers genera embedding del texto descriptivo del proyecto
6. **Index** -> Embedding almacenado en Qdrant con metadata
7. **Search** -> Endpoint de busqueda semantica: "departamento 3 dormitorios cerca al mar" -> Qdrant retorna proyectos similares por vector

## Que lo hace destacable

- **Busqueda semantica real**: No es keyword matching — entiende el significado de las consultas usando embeddings
- **Triple almacenamiento**: MongoDB (documentos), PostgreSQL (relacional), Qdrant (vectores) — cada motor para lo que mejor hace
- **Async-first**: Motor (MongoDB async) + asyncpg (PostgreSQL async) + httpx (HTTP async) — maxima concurrencia
- **Microservicios Docker**: 5 servicios aislados, escalables independientemente

## Evolucion del scraping inmobiliario

| Periodo | Repo | Nivel |
|---------|------|-------|
| Nov 2023 | WE-urbania | Notebook basico, Selenium |
| Jun 2024 | nexo-inmobiliario | Script modular, Selenium + BS4 + SQL |
| Dic 2024 | nexo-pruebas | Notebooks de experimentacion |
| Oct 2025 | urbania-scraper | FastAPI + Playwright + Qdrant (profesional) |
| **Mar 2026** | **nexo-scrapeo** | **Microservicios + triple DB + embeddings** |

Proyecto hermano: [[Urbania Scraper]] (mismo stack aplicado al portal Urbania.pe)
