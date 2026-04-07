---
aliases: [Resumen, About]
tags: [perfil, resumen]
---

# Resumen Profesional

## Quien soy

Ingeniero con formacion en **ingenieria civil y estructural** que transiciono hacia el desarrollo de software, especializandose en **desarrollo full-stack** e **ingenieria de datos**. Con mas de 2.5 anos de experiencia construyendo sistemas en produccion para el sector financiero, bancario e inmobiliario en Peru.

## Perfil tecnico

Desarrollador que abarca todo el ciclo de vida del software: desde el **diseno de pipelines ETL** que procesan cientos de reportes financieros, hasta **aplicaciones web full-stack** con arquitectura de monorepo y type-safety end-to-end. Experiencia demostrada en llevar proyectos desde prototipo hasta produccion con Docker, CI/CD y despliegue con Cloudflare.

## Sectores de experiencia

### Sector Financiero / Bancario
- Diseno e implementacion de pipelines ETL para procesamiento de **20+ tipos de reportes** con **458+ columnas** de datos
- Maquinas de estado de **10 pasos** para validacion de documentos financieros
- Replica automatizada de datos entre PostgreSQL y MSSQL para alimentar dashboards Power BI
- Calculos financieros: conversion monetaria PEN/USD, indicadores derivados, codigos mensuales

### Sector Inmobiliario
- Scraping automatizado de portales inmobiliarios peruanos (Nexo Inmobiliario, Urbania, OSCE)
- Busqueda semantica vectorial sobre proyectos inmobiliarios con embeddings y Qdrant
- Geolocalizacion y mapas interactivos con Leaflet para visualizacion de proyectos
- Extraccion y procesamiento de datos para analisis de mercado

### Ingenieria Civil (background)
- Analisis estructural con OpenSeesPy (armaduras y vigas)
- Codificacion automatica de presupuestos de construccion con NLP/ML
- Georreferenciacion de planos sobre mapas interactivos

## Enfoque de desarrollo

- **Iteracion constante**: El proyecto principal (ERP JLV) tiene 7+ versiones, cada una con mejoras arquitecturales significativas — ver [[03 - Trayectoria de Desarrollo]]
- **Produccion real**: No solo prototipos — los sistemas estan desplegados con Docker Compose, Nginx como reverse proxy, Redis para caching, GitHub Actions para CI/CD y Cloudflare Tunnels para acceso seguro
- **Type-safety end-to-end**: Migracion progresiva hacia TypeScript con tRPC, Prisma y Zod para eliminar errores en runtime
- **Automatizacion**: Uso de Apache Airflow para orquestar pipelines, n8n para workflows de negocio, y scripts Python para tareas repetitivas

## Links

- GitHub: [Gneomar](https://github.com/Gneomar)
- Stack detallado: [[02 - Stack Tecnico]]
- Evolucion: [[03 - Trayectoria de Desarrollo]]
