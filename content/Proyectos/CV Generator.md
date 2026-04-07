---
aliases: [CV Generator, Generador CV, CV-Generator-kurt]
tags: [proyecto, ai, fastapi, llm, destacado]
categoria: AI / Backend
complejidad: Alta
estado: Completado
horas_estimadas: "60-80h"
---

# CV Generator

> [!tip] IA multi-modelo
> Generador de CVs optimizados para ATS que soporta multiples LLMs (Mistral, Claude, GPT-4o, Gemini) via OpenRouter.

## Contexto

Herramienta que genera CVs personalizados y optimizados para sistemas ATS (Applicant Tracking Systems) usando inteligencia artificial. El usuario proporciona su CV base y una descripcion de puesto, y el sistema genera una version optimizada con scoring de compatibilidad.

**Problema que resuelve:** Adaptar un CV para cada oferta laboral es tedioso y requiere conocimiento de como funcionan los ATS. Esta herramienta automatiza la personalizacion y optimizacion.

## Repositorio

`Gneomar/CV-Generator-kurt` (privado)
**Fecha:** Marzo 2026

## Arquitectura

```
Cliente (HTTP)
     │
     ▼
┌─────────────────────────────────┐
│          FastAPI Backend         │
│                                  │
│  POST /generate-cv               │
│    └─ CV base + job description  │
│    └─ LLM genera CV optimizado   │
│                                  │
│  POST /analyze-match             │
│    └─ Scoring ATS (0-100)        │
│    └─ Sugerencias de mejora      │
│                                  │
│  POST /export                    │
│    └─ PDF (WeasyPrint)           │
│    └─ DOCX (python-docx)        │
│                                  │
│  ┌────────────────────────────┐  │
│  │     OpenRouter API          │  │
│  │  ┌─────────┐ ┌──────────┐ │  │
│  │  │ Mistral │ │ Claude   │ │  │
│  │  ├─────────┤ ├──────────┤ │  │
│  │  │ GPT-4o  │ │ Gemini   │ │  │
│  │  └─────────┘ └──────────┘ │  │
│  └────────────────────────────┘  │
│                                  │
│  ┌────────────────────────────┐  │
│  │     Templates (Jinja2)     │  │
│  │  CV format → PDF/DOCX      │  │
│  └────────────────────────────┘  │
└─────────────────────────────────┘
```

## Stack tecnico

| Componente | Tecnologia | Uso |
|-----------|-----------|-----|
| **Framework** | FastAPI + Uvicorn | API REST async |
| **Validacion** | Pydantic | Modelos tipados de request/response |
| **HTTP Client** | httpx | Llamadas async a OpenRouter API |
| **LLM Gateway** | OpenRouter API | Acceso unificado a Mistral, Claude, GPT-4o, Gemini |
| **PDF** | WeasyPrint + Jinja2 | Generacion de CV en PDF con templates HTML/CSS |
| **DOCX** | python-docx | Generacion de CV en formato Word |
| **Data** | pandas, numpy | Procesamiento de datos del CV |
| **Testing** | pytest | Tests automatizados de endpoints |

## Flujo de generacion

1. **Input**: Usuario envia su CV (texto/JSON) + descripcion del puesto objetivo
2. **Analisis**: LLM analiza la compatibilidad entre CV y puesto
3. **Generacion JSON-first**: El LLM genera el CV optimizado en formato JSON estructurado (no texto libre) para permitir revision manual antes de exportar
4. **Scoring**: Calcula un puntaje ATS (0-100) basado en coincidencia de keywords, skills y experiencia
5. **Carta de presentacion**: Opcionalmente genera una cover letter personalizada
6. **Export**: El JSON se renderiza con templates Jinja2 y se exporta a PDF (WeasyPrint) o DOCX (python-docx)

## API Endpoints

```
POST /generate-cv          # Genera CV optimizado (JSON)
POST /analyze-match        # Scoring ATS + sugerencias
POST /export               # Exporta a PDF/DOCX
GET  /models               # Lista modelos LLM disponibles
```

Tambien incluye endpoints "rapidos" con CV pre-cargado para demo sin necesidad de subir archivos.

## Que lo hace destacable

- **Multi-modelo**: No depende de un solo proveedor de IA — puede usar el modelo mas adecuado para cada tarea
- **JSON-first**: Genera datos estructurados, no texto libre — permite revision y edicion antes del export final
- **Doble formato de exportacion**: PDF (profesional) y DOCX (editable)
- **Scoring ATS cuantitativo**: No solo genera el CV, mide que tan compatible es con el puesto
