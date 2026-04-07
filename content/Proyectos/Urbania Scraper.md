---
aliases: [Urbania Scraper, urbania-scraper]
tags: [proyecto, scraping, ai, fastapi, destacado]
categoria: Scraping / AI
complejidad: Alta
estado: Completado
horas_estimadas: "80-100h"
---

# Urbania Scraper

> [!tip] Scraping profesional
> Extractor de datos inmobiliarios de Urbania.pe con API REST, CLI, busqueda semantica y descarga de imagenes.

## Contexto

Urbania.pe es otro de los principales portales inmobiliarios de Peru. Este scraper extrae listados y detalles de proyectos inmobiliarios con una API REST y un CLI para uso directo.

Proyecto hermano de [[Nexo Scrapeo - Pipeline Inmobiliario]], aplicando el mismo patron arquitectural a un portal diferente.

## Repositorio

`Gneomar/urbania-scraper` (publico)
**Fecha:** Octubre 2025

## Stack tecnico

| Componente | Tecnologia |
|-----------|-----------|
| **API** | FastAPI |
| **Scraping** | Playwright (headless browser) |
| **Parsing** | BeautifulSoup + lxml |
| **Embeddings** | Sentence-Transformers + PyTorch |
| **Vector DB** | Qdrant |
| **Document DB** | MongoDB (PyMongo) |
| **Archivos** | aiofiles (async file I/O) |
| **Deploy** | Docker Compose (imagen oficial Playwright) |

## Funcionalidades

### API REST
- Endpoints para iniciar scraping de listados y detalles
- Jobs asincronos en background
- Healthcheck endpoint

### CLI
- Uso directo desde terminal sin levantar el servidor
- Parametros para filtrar por zona, tipo de propiedad, rango de precios

### Scraping de detalle
- Extrae: precio, ubicacion, metros cuadrados, dormitorios, banos, descripcion, amenities
- Maneja paginacion automatica
- Soporte para sitios con lazy-loading (Playwright)

### Descarga de imagenes
- Dos modos: alta calidad y baja calidad
- Estructura de salida organizada por proyecto
- Imagenes numeradas secuencialmente

### Busqueda semantica
- Genera embeddings del texto descriptivo con Sentence-Transformers
- Almacena en Qdrant para busqueda por similitud
- Busqueda en lenguaje natural: "casa con jardin en Miraflores"

## Evolucion desde WE-urbania

| Version | Repo | Tecnologia | Nivel |
|---------|------|-----------|-------|
| v1 (2023) | WE-urbania | Jupyter Notebook basico | Prototipo |
| **v2 (2025)** | **urbania-scraper** | **FastAPI + Playwright + Qdrant** | **Profesional** |

## Que lo hace destacable

- **Repo publico**: Codigo disponible para revision en GitHub
- **Dual interface**: API REST para integraciones + CLI para uso directo
- **Async-first**: aiofiles, Playwright async, background tasks
- **Mismo patron que nexo-scrapeo**: Demuestra capacidad de aplicar arquitecturas a diferentes dominios
