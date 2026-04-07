---
aliases: [Trayectoria, Evolucion, Timeline]
tags: [trayectoria, evolucion]
---

# Trayectoria de Desarrollo

## Timeline de evolucion tecnica

### 2024 Q1-Q2 — Fundamentos: Python + Data
> Scripts ETL, Jupyter Notebooks, primeros contactos con SQL

**Tecnologias incorporadas:** Python, pandas, openpyxl, SQLAlchemy, psycopg2, PostgreSQL, Jupyter Notebooks

**Proyectos clave:**
- `Sistema-modelo-JLV` / `Sistema-bbdd-JLV` — Scripts Python para extraer datos de archivos Excel en un fileserver y cargar a PostgreSQL. Pipeline ETL lineal: leer carpetas -> extraer informes -> calcular indicadores bancarios -> enviar a SQL
- `Solve-Truss-example-OpenSeesPy` — Analisis estructural, demostrando el background de ingenieria civil
- `Bases-Distritos-Incoin` / `Pe_incoin` / `postgres_incoin` — Procesamiento de datos empresariales para cliente Incoin: bases distritales trimestrales, planes estrategicos, migracion Excel->PostgreSQL
- `Calculador-BBDD-JLV` — Calculadora de datos con notebook pesado (2.4MB)
- `validador_datos_jlv` — 12+ reglas de validacion de datos con regresion lineal para tendencias

**Lo que se aprendio:** Manipulacion de datos con pandas, conexion Python-PostgreSQL, logica de validacion, procesamiento batch de archivos Excel.

---

### 2024 Q3 — Transicion a Web: Django
> Primeros pasos en desarrollo web, CRUD basico, HTML/CSS

**Tecnologias incorporadas:** Django 5.x, HTML, CSS, Django ORM, manage.py

**Proyectos clave:**
- `django-crud-first-project` — Primer proyecto Django de aprendizaje. CRUD basico con REST, app de tareas. Duracion: ~2 dias
- `django-Kurt-Project` — Proyecto educativo con multiples apps Django, archivos estaticos, conexion a PostgreSQL, aprendiendo HTML
- `django-folders-postgresql` — Aplicacion con 6 apps Django (folders, home, library, myapp, submits, apptest). Primera integracion real Django + PostgreSQL
- `nexo-inmobiliario` — Primer scraper serio: Selenium/BS4 para extraer datos de portal inmobiliario, modulos separados (scraper, send_sql, descargar_imagenes)

**Lo que se aprendio:** Patron MTV de Django, ORM, routing, templates, admin, static files. Web scraping con Selenium.

---

### 2024 Q4 — Consolidacion: Django en produccion + primeros Docker
> Django como framework principal, Docker como herramienta de despliegue

**Tecnologias incorporadas:** Docker, Docker Compose, Apache Airflow (basico)

**Proyectos clave:**
- `Django-proyect-jlv` — Primera version web del ERP: modelos de tablas SQL, queries para servicios/informes/etapas. Transicion real de scripts a web app
- `airflow-postgres-docker` — Primer contacto con Airflow: setup basico con Docker Compose + PostgreSQL + directorio de DAGs
- `PostgreSQL-Python` — Laboratorio de SQLAlchemy: metadata, scripts SQL para etapas/informes/servicios, estructura JSON de tablas
- `BRCP-API` — Extraccion de datos del Banco Central de Reserva del Peru via API publica
- `fast-api-interact-sql` — Primera incursion en FastAPI: API para interactuar con SQL

**Lo que se aprendio:** Docker Compose para orquestar servicios, Airflow como concepto, FastAPI como alternativa a Django para APIs.

---

### 2025 Q1-Q2 — APIs profesionales: FastAPI + Docker
> FastAPI como framework API principal, Docker en todos los proyectos, primeras integraciones con Microsoft

**Tecnologias incorporadas:** FastAPI (avanzado), Gunicorn, MSAL (Microsoft Auth), One-drive API, Microsoft Graph, NLP/ML

**Proyectos clave:**
- `django-web-erp2` — ERP v2: primer Django dockerizado con dashboard
- `django-surf-new/new2` — Proyectos web de surf con Docker, perfiles de usuario
- `fastAPI-template-auth` — Template reutilizable para APIs FastAPI con auth
- `One-drive-API` — Integracion con Microsoft Graph: OneDrive, SharePoint, Email con autenticacion MSAL
- `analysis_db_openai` — Chatbot que genera SQL desde lenguaje natural con GPT-4o-mini. Pipeline: pregunta natural -> GPT genera SQL -> ejecuta query -> GPT interpreta resultado
- `crud-fastpAPI` — CRUD full-stack con autenticacion (backend + frontend)
- `tesis-COR` — Tesis academica con analisis de datos y Power BI

**Lo que se aprendio:** FastAPI con async, integracion con APIs de Microsoft, primeros usos de IA generativa (OpenAI), patrones de autenticacion JWT.

---

### 2025 Q3 — Expansion: React + TypeScript + microservicios
> Adopcion de frontend moderno, experimentacion con diferentes stacks

**Tecnologias incorporadas:** React 18, TypeScript, NestJS, TailwindCSS, Zustand, JWT/Passport.js, Vite, Redis, Celery

**Proyectos clave:**
- `django-erp-jlv-v2` — ERP v4 con Docker, detalle de informes bancarios
- `erp-spa` — **Experimento con NestJS + React**: SPA completa con TypeORM, Zustand, RBAC con 4 roles, JWT auth. Fue abandonado tras evaluar que NestJS no aportaba suficiente valor sobre Django/FastAPI
- `django-erp-v3` — ERP v5 con TailwindCSS, autenticacion por email con verificacion, aprobacion por admin, 4 roles, Cloudflare Tunnels. Documentacion de migracion de 73KB
- `web-scrap-jlv-comercial` — Scraping de licitaciones publicas de OSCE con Selenium
- `web-happy-kids` — Sitio web para centro educativo con Django + Docker
- `social-media-api` — API de red social con FastAPI + Docker
- `django-panel-surf-new3` — Tercera iteracion del proyecto surf con panel admin
- `web-portfolio-kurt` — Portfolio personal con Django
- `web-manga-park` — API FastAPI + Playwright para descarga de manga
- `urbania-scraper` — Scraper profesional de Urbania con FastAPI, Playwright, busqueda vectorial con Qdrant + Sentence-Transformers

**Lo que se aprendio:** React + TypeScript, state management, CSS-in-utility (Tailwind), deployment con Cloudflare, bases de datos vectoriales, embeddings para busqueda semantica.

---

### 2025 Q4 — Produccion: Airflow + multi-DB + CI/CD
> Sistemas en produccion real, pipelines de datos robustos, infraestructura multi-servicio

**Tecnologias incorporadas:** Apache Airflow 2.x (avanzado), CeleryExecutor, MSSQL, MongoDB, Nginx, GitHub Actions, Gunicorn, OpenSSL

**Proyectos clave:**
- `JLV-Airflow-System` — Hub central: 7 contenedores Docker (PostgreSQL, MSSQL, MongoDB, FastAPI, React/Nginx, Mongo Express, postgres-api). Redes Docker externas, fileserver montado, autenticacion JWT
- `django-react-erp` — ERP v6: DRF + React 19 + TypeScript. Dashboard con KPIs, mapa interactivo con geolocalizacion, workflow de estados (borrador-pendiente-revision-emitido), importacion CSV
- `airflow-ETL-JLV` — Pipeline ETL con Airflow: 3 variantes Docker (standard, Celery, test), procesamiento geoespacial con geopandas, autenticacion MSAL
- `postgresql-mssql` — Puente de sincronizacion entre PostgreSQL y MSSQL con Docker multi-contenedor
- `mssql-jlv-api` — API FastAPI profesional para MSSQL con SSL, Gunicorn, documentacion API completa (13KB)
- `geo-photos-demo` — Fotos geolocalizadas: mapa Leaflet, extraccion EXIF, georreferenciacion de planos

**Lo que se aprendio:** Orquestacion de pipelines complejos, multi-database architecture, reverse proxy con Nginx, CI/CD con GitHub Actions, seguridad SSL.

---

### 2026 Q1-Q2 — Modernizacion: TypeScript full-stack + monorepo
> Migracion a stack completamente type-safe, monorepo, runtime moderno con Bun

**Tecnologias incorporadas:** Bun, Turborepo, Elysia, tRPC, TanStack Router/Start, Prisma 7.4, Drizzle ORM, Better Auth, Biome, shadcn/ui, Recharts, react-pdf-viewer, Leaflet (TS), Playwright E2E, n8n, MCP Protocol

**Proyectos clave:**
- `erp-jlv-django-react` — ERP v6.5 en produccion: Docker multi-servicio (Redis + Backend + Scheduler + Frontend/Nginx), GitHub Actions CI/CD, documentacion de deployment
- `typescript-erp-jlv` — **ERP v7 (actual)**: Monorepo TypeScript con Turborepo, Elysia + tRPC + React + Prisma + Better Auth. Type-safety E2E, mapas con Leaflet, PDFs, graficos con Recharts
- `Airflow-ETL-Bancos` — Pipeline ETL mas complejo: 4 DAGs encadenados, 458+ columnas, 10 pasos de validacion, replica MSSQL, batch multihilo
- `nexo-scrapeo` — Pipeline de scraping con microservicios: FastAPI + Playwright + MongoDB + PostgreSQL + Qdrant (5 servicios Docker)
- `page-report-validaciones` — Dashboard full-stack: React + ECharts (Sankey) + FastAPI + PostgreSQL + Docker
- `CV-Generator-kurt` — Generador de CV con IA multi-modelo (Mistral, Claude, GPT-4o, Gemini) via OpenRouter
- `biblioteca` / `biblioteca-HK` — Monorepos de practica con Elysia + tRPC + Prisma/Drizzle + Better Auth + Playwright
- `n8n_agent` — Agente MCP para n8n con 7 skills y 3,336 tests
- `mssql-dockerfile` / `mssql-jlv-api` — Infraestructura MSSQL containerizada

**Lo que se aprendio:** Monorepo architecture, type-safety E2E con tRPC, runtime Bun, ORMs modernos (Prisma/Drizzle), SSR con TanStack Start, testing E2E con Playwright, MCP Protocol.

---

## Patron de crecimiento

```
Complejidad
    ^
    |                                          * typescript-erp-jlv
    |                                     * Airflow-ETL-Bancos
    |                                * erp-jlv-django-react
    |                           * JLV-Airflow-System
    |                      * django-erp-v3
    |                 * django-react-erp
    |            * Django-proyect-jlv
    |       * nexo-inmobiliario
    |  * Sistema-bbdd-JLV
    +-------------------------------------------------> Tiempo
    2024              2025              2026
```

## Decisiones arquitecturales clave

1. **Django -> FastAPI para APIs**: Django se mantiene para apps con admin/templates, pero FastAPI es la eleccion para APIs puras por rendimiento async y tipado con Pydantic
2. **NestJS descartado**: Se probo en `erp-spa` pero se considero demasiado ceremonioso. La eleccion final fue Elysia (Bun-native, mas ligero)
3. **Prisma sobre Drizzle**: Ambos probados en repos `biblioteca` vs `biblioteca-HK`. Prisma elegido para el ERP principal por madurez del ecosistema
4. **PostgreSQL como base principal**: MSSQL solo se usa como replica para Power BI, MongoDB solo para logs/documentos
5. **Turborepo para monorepo**: Elegido sobre Nx por simplicidad y compatibilidad nativa con Bun
6. **Cloudflare Tunnels sobre VPN**: Para exponer servicios internos sin configurar firewalls
