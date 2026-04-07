---
aliases: [Stack, Tecnologias]
tags: [stack, tecnologias]
---

# Stack Tecnico

## Lenguajes

### Python — Nivel avanzado
Lenguaje principal durante los primeros 2 anos. Usado en backend (Django, FastAPI), data engineering (Airflow, pandas), scraping (Playwright, Selenium, BeautifulSoup) y machine learning (scikit-learn, Sentence-Transformers).

**Patrones y librerias dominadas:**
- Web frameworks: Django (MTV, ORM, Admin, DRF), FastAPI (async, Pydantic, dependency injection)
- Data: pandas, geopandas, openpyxl, pyarrow, XlsxWriter, numpy
- DB drivers: psycopg2, asyncpg, SQLAlchemy (sync + async), pymssql, pyodbc, pymongo, Motor
- Scraping: Playwright (async), Selenium, BeautifulSoup, lxml, httpx
- ML/NLP: scikit-learn (regresion lineal), Sentence-Transformers (embeddings), OpenAI API
- Auth: PyJWT, bcrypt, MSAL (Microsoft Azure AD), python-decouple
- Testing: pytest
- Templating: Jinja2, WeasyPrint (PDF), python-docx

### TypeScript — Nivel intermedio-avanzado (adopcion rapida 2025-2026)
Adoptado progresivamente para frontend (React) y luego para full-stack con Elysia + tRPC. En 2026 es el lenguaje principal del proyecto mas complejo.

**Ecosistema dominado:**
- Runtime: Bun (package manager + runtime)
- Frontend: React 18/19, TanStack Router, TanStack Start (SSR), TanStack Table, Vite
- Backend: Elysia (Bun-native), NestJS (experimentado y descartado)
- Type-safe API: tRPC (end-to-end type safety)
- ORM: Prisma 7.4, Drizzle ORM
- UI: TailwindCSS, shadcn/ui, Lucide React
- Graficos/Mapas: Recharts, Leaflet, Apache ECharts
- Auth: Better Auth
- Monorepo: Turborepo
- Linting: Biome
- Testing: Playwright (E2E)

### SQL — Nivel intermedio
Usado directamente en scripts de migracion, esquemas versionados y queries complejas.

- DDL/DML para PostgreSQL y MSSQL
- Esquemas versionados (01_meta -> 06_migrations)
- Queries de agregacion, joins complejos, CTEs
- Init-scripts para Docker

---

## Backend Frameworks

### Django + Django REST Framework
> Usado en: [[ERP JLV - Sistema Empresarial]] (versiones 1-6), [[Geo Photos Demo]], web-happy-kids, django-surf, django-folders-postgresql

- Django ORM con modelos complejos (Proyecto, Servicio, Entidad, Informe, Promotor, Funcionario, Ubigeo)
- Django Admin personalizado con panel avanzado
- DRF con SimpleJWT para APIs REST con autenticacion
- Autenticacion por email con verificacion de correo y aprobacion por admin
- Sistema de roles granular (Visitante/Supervisor/Jefe/Administrador)
- Middleware personalizado, signals, management commands
- Static files, templates con TailwindCSS

### FastAPI
> Usado en: [[JLV Airflow System]], [[CV Generator]], [[Nexo Scrapeo - Pipeline Inmobiliario]], [[Page Report Validaciones]], mssql-jlv-api, social-media-api, urbania-scraper, web-manga-park, BRCP-API

- Async handlers con asyncpg y Motor
- Dependency injection para DB sessions y auth
- Pydantic models para validacion de request/response
- Background tasks para jobs largos (scraping, generacion de CV)
- Middleware CORS, rate limiting
- Gunicorn como servidor de produccion
- Documentacion OpenAPI automatica

### Elysia (Bun)
> Usado en: [[ERP JLV - Sistema Empresarial]] (v7 actual), [[Biblioteca Digital]]

- Runtime nativo de Bun — rendimiento superior a Node.js
- Integracion con tRPC para APIs type-safe
- Better Auth para autenticacion
- Prisma/Drizzle como ORM
- Estructura de monorepo con Turborepo

---

## Frontend

### React + TypeScript
> Usado en: [[ERP JLV - Sistema Empresarial]] (v6-v7), [[Page Report Validaciones]], [[Biblioteca Digital]], erp-jlv-django-react

- React 18/19 con hooks, context, suspense
- TanStack Router para routing type-safe con file-based routes
- TanStack Start para SSR (Server-Side Rendering)
- TanStack Table para tablas paginadas con sorting/filtering
- React Query (TanStack Query) para server state management
- Zustand para client state management
- Vite como bundler
- Bun como package manager
- TailwindCSS + shadcn/ui para UI components
- Apache ECharts para visualizaciones (diagramas Sankey)
- Recharts para graficos
- Leaflet para mapas interactivos
- react-pdf-viewer para visualizacion de PDFs

---

## Bases de Datos

### PostgreSQL — Base de datos principal
Usada en practicamente todos los proyectos desde 2024. Conocimiento profundo de:
- Modelado relacional complejo (ERP con 15+ tablas interrelacionadas)
- Extensiones: PostGIS (geoespacial, inferido por uso de geopandas)
- Drivers: psycopg2 (sync), asyncpg (async), SQLAlchemy (ORM)
- Migraciones: Alembic, Django migrations, Prisma migrations
- Docker: PostgreSQL 13/15/16 containerizado con init-scripts y volumenes persistentes

### Microsoft SQL Server (MSSQL)
Usado como base de datos secundaria/replica para integracion con Power BI:
- Drivers: pymssql, pyodbc
- Configuracion SSL con OpenSSL en Docker
- Replica automatica desde PostgreSQL via DAGs de Airflow
- MSSQL Express containerizado

### MongoDB
Usado para almacenamiento de documentos y logs:
- Motor (async driver) en FastAPI
- PyMongo en scripts y Airflow
- Mongo Express como UI de administracion
- Logs de validacion de pipelines ETL

### Qdrant (Vector Database)
Usado para busqueda semantica en proyectos de scraping inmobiliario:
- Almacenamiento de embeddings generados con Sentence-Transformers
- Busqueda por similitud coseno
- Docker Compose con servicio dedicado

---

## Data Engineering & ETL

### Apache Airflow
> Usado en: [[Airflow ETL Bancos]], [[Data Pipelines JLV]], airflow-postgres-docker

- Airflow 2.10.4 con Docker Compose
- DAGs encadenados con dependencias (4 DAGs en secuencia)
- Executor: LocalExecutor y CeleryExecutor (distribuido)
- Conexiones a PostgreSQL, MSSQL, MongoDB
- Variables y connections via Airflow UI
- Custom operators y hooks
- rsync para despliegue de DAGs

### pandas / geopandas
- Procesamiento de Excel con openpyxl y xlrd
- Transformaciones complejas: 458+ columnas, 20+ tipos de tabla
- Conversion a Parquet con pyarrow
- Procesamiento geoespacial con geopandas
- Export a CSV, JSON, Excel (XlsxWriter)

### Pipeline patterns implementados
1. **Extract**: Scan de fileserver buscando reportes Excel por patron de nombre
2. **Validate**: 7 pasos (parquet -> ajustar -> limpiar -> convertir tipos -> asignar ID -> validar -> exportar)
3. **Transform**: Calculos derivados (conversion monetaria, codigos mensuales, indicadores)
4. **Load**: Upsert en PostgreSQL (primaria) + replica en MSSQL (Power BI)
5. **Log**: Registro de validaciones en MongoDB

---

## Infraestructura & DevOps

### Docker & Docker Compose
Presente en el **90%+ de los proyectos** desde mediados de 2025:
- Multi-stage Dockerfiles
- Compose con 7+ servicios orquestados (PostgreSQL, MSSQL, MongoDB, FastAPI, React/Nginx, Redis, Scheduler)
- Redes Docker externas compartidas
- Volumenes persistentes para datos y configuracion
- Fileserver montado en solo lectura
- Healthchecks

### Nginx
- Reverse proxy para frontend React
- Configuracion de static files
- Proxy pass a backend API

### Redis
- Usado como broker/cache en produccion del ERP
- Integracion con Celery para tareas distribuidas

### Cloudflare Tunnels
- Exposicion segura de servicios locales a internet sin abrir puertos
- Usado en produccion para el ERP y servicios internos

### GitHub Actions (CI/CD)
- Pipeline de build y deploy para el ERP en produccion
- Automatizacion de tests y deployment

### Self-hosting
- n8n con PostgreSQL y backup/restore automatico
- Nextcloud para almacenamiento en la nube
- Obsidian web accesible remotamente via Cloudflare

---

## AI & Machine Learning

### Integraciones con LLMs
- **OpenAI API** (GPT-4o-mini): Generacion de SQL desde lenguaje natural, interpretacion de resultados — ver analysis_db_openai
- **OpenRouter API** (multi-modelo): Generacion de CVs con Mistral, Claude, GPT-4o, Gemini — ver [[CV Generator]]
- **Claude Code**: Desarrollo asistido por IA con CLAUDE.md y AGENTS.md en proyectos recientes

### NLP / Machine Learning
- **Sentence-Transformers**: Generacion de embeddings para busqueda semantica de proyectos inmobiliarios
- **scikit-learn**: Regresion lineal para analisis de tendencias en datos financieros
- **NLP para clasificacion**: Codificacion automatica de partidas presupuestarias de construccion

### MCP (Model Context Protocol)
- Agente MCP para n8n con 7 skills (expression-syntax, workflow-patterns, validation, node-configuration, code JS/Python)
- mcp-postgres para acceso a bases de datos desde Claude

---

## Herramientas de desarrollo

| Herramienta | Uso |
|-------------|-----|
| Bun | Package manager y runtime para TypeScript |
| Turborepo | Monorepo management |
| Biome | Linting y formatting (reemplazo de ESLint + Prettier) |
| Playwright | Testing E2E |
| pytest | Testing Python |
| Alembic | Migraciones de DB (SQLAlchemy) |
| Prisma | ORM + migraciones (TypeScript) |
| Drizzle | ORM alternativo a Prisma (mas ligero) |
| Power BI | Dashboards de negocio (consumo de MSSQL) |
| Jupyter Notebooks | Prototipado y analisis exploratorio |
