---
aliases: [Secundarios, Utilidades, Otros Proyectos]
tags: [proyectos, secundarios, utilidades]
---

# Proyectos Secundarios y Utilidades

Proyectos menores que complementan el portfolio. Organizados por categoria.

---

## APIs & Backend

### mssql-jlv-api
- **Stack**: FastAPI, MSSQL, Docker, Gunicorn, OpenSSL
- **Complejidad**: Alta | **Horas**: ~60-80h
- **Descripcion**: API REST profesional para interactuar con bases de datos MSSQL. Incluye configuracion SSL con OpenSSL en Docker, Gunicorn como servidor de produccion, y documentacion API detallada (13KB). Endpoint de produccion para el ecosistema JLV.

### social-media-api
- **Stack**: FastAPI, Docker, PostgreSQL
- **Complejidad**: Alta | **Horas**: ~40-60h
- **Descripcion**: Backend completo para una aplicacion de red social. API REST con endpoints de posts, usuarios, autenticacion. README detallado (6KB), estructura profesional con `src/`, `.dockerignore`.

### project_api
- **Stack**: FastAPI (backend), Node.js (frontend), Docker Compose
- **Complejidad**: Alta | **Horas**: ~40-60h
- **Descripcion**: Aplicacion full-stack con backend FastAPI y frontend Node.js, orquestada con Docker Compose. Refactorizacion continua a lo largo de su vida util.

### crud-fastpAPI
- **Stack**: FastAPI, Docker Compose
- **Complejidad**: Media-Alta | **Horas**: ~30-40h
- **Descripcion**: CRUD full-stack con sistema de autenticacion progresivo (test_auth -> estable_autenticacion -> fronted_autenticacion). Backend + frontend dockerizado.

### postgresql-mssql
- **Stack**: Python, PostgreSQL, MSSQL, Docker Compose
- **Complejidad**: Alta | **Horas**: ~40-60h
- **Descripcion**: Puente de sincronizacion/migracion de datos entre PostgreSQL y MSSQL. Docker multi-contenedor con ambas bases de datos, app Python como middleware, init-scripts SQL para setup automatico.

### fastAPI-template-auth
- **Stack**: FastAPI, Docker
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Template reutilizable para crear APIs FastAPI con autenticacion integrada. Base para nuevos proyectos.

### BRCP-API
- **Stack**: Python, Jupyter, pandas
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Extraccion y procesamiento de datos de la API publica del Banco Central de Reserva del Peru. Notebooks para consultas simples y multiples tablas, exportacion a Excel.

---

## Web Scraping

### web-scrap-jlv-comercial
- **Stack**: Python, Selenium, BeautifulSoup, pandas, openpyxl
- **Complejidad**: Media | **Horas**: ~20-30h
- **Descripcion**: Scraper para el portal OSCE (Organismo Supervisor de las Contrataciones del Estado, Peru). Extrae datos de licitaciones/contrataciones publicas y exporta a Excel. Estructura organizada por fuente (`src/osce`, `src/otros`).

### web-manga-park
- **Stack**: FastAPI, Playwright, Docker
- **Complejidad**: Media | **Horas**: ~20-30h
- **Descripcion**: API REST para descarga automatizada de imagenes de MangaPark. Modo generico y modo manga. Scraping con Playwright para sitios con lazy-loading, tareas en background, imagenes numeradas. Docker con imagen oficial de Playwright.

### nexo-inmobiliario
- **Stack**: Python, Selenium/BS4, SQL
- **Complejidad**: Media | **Horas**: ~30-40h
- **Descripcion**: Scraper original de Nexo Inmobiliario. Modulos separados: scraper, send_sql, descargar_imagenes. Precursor de [[Nexo Scrapeo - Pipeline Inmobiliario]].

---

## Data & Analytics

### analysis_db_openai
- **Stack**: Python, OpenAI GPT-4o-mini, PostgreSQL, SQLAlchemy, pandas
- **Complejidad**: Media | **Horas**: ~20-30h
- **Descripcion**: Chatbot de consultas en lenguaje natural sobre base de datos PostgreSQL. Pipeline: pregunta natural -> GPT genera SQL -> ejecuta query -> GPT interpreta resultado en lenguaje natural. Usa esquema de tablas en JSON y diccionario de datos en Excel. Limita resultados a 10 registros por seguridad.

### NLP-Codificacion-Presupuestos
- **Stack**: Python, NLP/ML, pandas, Jupyter
- **Complejidad**: Media | **Horas**: ~40-60h
- **Descripcion**: Modelo de Machine Learning para codificar automaticamente items de presupuestos de construccion. NLP para asignar codigos a descripciones presupuestarias. Incluye notebook del modelo, procesamiento de datos, concentrador de Excels, y lista de codigos de referencia.

### validador_datos_jlv
- **Stack**: Python, scikit-learn, pandas, Jupyter
- **Complejidad**: Media | **Horas**: ~30-40h
- **Descripcion**: Sistema de validacion de datos con 12+ reglas de negocio, analisis de reportabilidad, y analisis de tendencias con regresion lineal. Notebook principal de 49KB.

### Bancos-Data-Analytics-Experimental
- **Stack**: Python, Jupyter, pandas
- **Complejidad**: Baja | **Horas**: ~10-15h
- **Descripcion**: Analisis exploratorio de datos bancarios: calculo de ratios financieros, indicadores estadisticos basicos, exportacion a Excel.

### BBDD-bancos
- **Stack**: Python, SQL, pandas, Jupyter
- **Complejidad**: Media | **Horas**: ~20-30h
- **Descripcion**: Esquema de base de datos para sector bancario (create_table.sql, 5KB). Scripts de calculos financieros, modulos ejecutables, notebook de testing.

---

## Aplicaciones Web

### django-surf-new / new2 / panel-surf-new3
- **Stack**: Django, Docker Compose
- **Complejidad**: Media | **Horas**: ~30-40h (total 3 versiones)
- **Descripcion**: Sitio web de surf con 3 iteraciones. v1: basico, v2: perfiles de usuario, v3: panel administrativo/dashboard. La v3 tuvo 4 meses de desarrollo activo (Jun-Oct 2025).

### web-happy-kids
- **Stack**: Django, Docker Compose
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Sitio web para centro educativo/guarderia infantil "Happy Kids". Pagina "Nosotros" con features, Django dockerizado.

### web-portfolio-kurt
- **Stack**: Django, Docker
- **Complejidad**: Baja-Media | **Horas**: ~10-15h
- **Descripcion**: Portfolio personal con Django y Docker.

### django-Kurt-Project
- **Stack**: Django 5.1, PostgreSQL, pandas, NumPy
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Proyecto educativo para aprender Django. Multiples apps, archivos estaticos, conexion a PostgreSQL.

---

## Herramientas & Utilidades

### n8n_agent
- **Stack**: Node.js, MCP Protocol, Claude Desktop
- **Complejidad**: Media | **Horas**: ~20-30h
- **Descripcion**: Agente MCP (Model Context Protocol) que permite controlar n8n desde Claude Desktop/Claude Code. 7 skills: expression-syntax, workflow-patterns, validation, node-configuration, code JS/Python. 3,336 tests incluidos.

### n8n-local-kurt
- **Stack**: Docker, n8n, PostgreSQL 16, Cloudflare, Bash
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Setup de n8n self-hosted con PostgreSQL, backup/restore automatico, soporte Cloudflare tunnel. 3 variantes de compose (normal, backup, cloudflare).

### One-drive-API
- **Stack**: Python, Microsoft Graph API, MSAL
- **Complejidad**: Media | **Horas**: ~20-30h
- **Descripcion**: Scripts para interactuar con OneDrive, SharePoint y Outlook Email via Microsoft Graph API. Autenticacion publica MSAL, operaciones de drive, envio de emails.

### organizador-de-carpetas
- **Stack**: Python, SQLAlchemy, PostgreSQL, pandas, openpyxl
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Organizacion automatica de carpetas basada en datos de base de datos. Queries SQL para etapas/informes/servicios, validacion con notebooks, exportacion a Excel.

### heic-to-png
- **Stack**: Python, Pillow, pillow-heif
- **Complejidad**: Baja | **Horas**: ~3-5h
- **Descripcion**: Conversor batch de imagenes HEIC/HEIF a PNG. CLI con argumentos, barra de progreso, soporte multiple extensiones. Repo publico.

### clonador-hojas-excel
- **Stack**: Python, openpyxl, Jupyter
- **Complejidad**: Baja | **Horas**: ~3-5h
- **Descripcion**: Script para clonar/duplicar hojas dentro de archivos Excel usando plantillas.

### CV-Generator-kurt → ver [[CV Generator]]

---

## Infraestructura & Self-hosting

### mssql-dockerfile
- **Stack**: Docker, MSSQL, SQL
- **Complejidad**: Baja | **Horas**: ~3-5h
- **Descripcion**: Dockerfile y Docker Compose para MSSQL con init-scripts. Repo publico.

### mcp-postgres
- **Stack**: Docker, PostgreSQL
- **Complejidad**: Baja | **Horas**: ~2-3h
- **Descripcion**: Docker Compose minimalista para PostgreSQL, para uso con MCP.

### nextcloud-local-kurt
- **Stack**: Docker, Nextcloud, PHP
- **Complejidad**: Baja | **Horas**: ~3-5h
- **Descripcion**: Nextcloud self-hosted con Docker y configuracion PHP personalizada.

### obsidian-cloudflare
- **Stack**: Docker, Obsidian (linuxserver), Cloudflare Tunnels
- **Complejidad**: Baja | **Horas**: ~3-5h
- **Descripcion**: Obsidian web accesible remotamente via Cloudflare Tunnel. Volumenes persistentes para vaults y configuracion.

### airflow-postgres-docker
- **Stack**: Docker, Airflow, PostgreSQL
- **Complejidad**: Media | **Horas**: ~10-15h
- **Descripcion**: Template base para Airflow + PostgreSQL con Docker. Directorio de DAGs, init-scripts.

---

## Academico & Aprendizaje

### tesis-COR
- **Stack**: Python, Jupyter, pandas, Power BI, Excel
- **Complejidad**: Media | **Horas**: ~40-60h
- **Descripcion**: Proyecto de tesis con analisis de datos financieros/operativos (utilidad, margen). Scripts de procesamiento, archivo Power BI para visualizacion, datasets en Excel.

### Solve-Truss-example-OpenSeesPy
- **Stack**: Python, OpenSeesPy, opsvis, matplotlib
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Analisis estructural de armaduras y vigas con OpenSeesPy. Verificacion de ejercicios de ingenieria comparando calculos manuales con simulacion. Repo publico.

### django-crud-first-project
- **Stack**: Django, SQLite
- **Complejidad**: Baja | **Horas**: ~5-8h
- **Descripcion**: Primer proyecto Django. CRUD basico con REST, app de tareas, app hello. Proyecto de 2 dias.

---

## Datos Empresariales (Incoin)

### postgres_incoin
- **Stack**: Python, PostgreSQL, pandas, Jupyter, Excel
- **Complejidad**: Media-Alta | **Horas**: ~30-40h
- **Descripcion**: Migracion de datos empresariales de Excel a PostgreSQL para Incoin. ETL de proyectos, stock, consultas automatizadas. Integracion con sistema Nexo. Libreria de funciones reutilizables.

### Bases-Distritos-Incoin
- **Stack**: Python, Jupyter, pandas, Excel
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Procesamiento de bases de datos distritales por trimestre. Compilador/separador de bases, generacion trimestral automatica, plantillas reutilizables.

### Pe_incoin
- **Stack**: Python, Jupyter, pandas, Excel
- **Complejidad**: Media | **Horas**: ~15-20h
- **Descripcion**: Procesamiento de datos del Plan Estrategico de Incoin. Notebook de 57KB, renombramiento de columnas, manejo de historicos, corroboracion con cabeceras.

---

## Repos minimos / placeholders

| Repo | Descripcion |
|------|-------------|
| airflow-opt-kurt | Placeholder vacio para config optimizada de Airflow |
| kurt-landpage | Landing page sin desarrollar (solo initial commit) |
| claude-app-test | Scaffold basico `bun create vite` de prueba |
| testing-kurt | Scripts experimentales de testing y markmap |
| django-fast | Django + Docker + PostgreSQL (setup rapido) |
| WE-urbania | Notebook basico de scraping Urbania (reemplazado por [[Urbania Scraper]]) |
| nexo-pruebas | Notebooks de experimentacion para scrapers Nexo |
| Calculador-BBDD-JLV | Notebook unico de calculo (2.4MB) |
| System-Folder-Windows | Explorador de carpetas con markmap |
| python-postgre-SQL | Notebooks de conexion Python-PostgreSQL-SQLServer |
| PostgreSQL-Python | Laboratorio de SQLAlchemy |
| django-folders-postgresql | Django multi-app para gestion de datos |
| django-crud-first-project | Primer proyecto Django de aprendizaje |
