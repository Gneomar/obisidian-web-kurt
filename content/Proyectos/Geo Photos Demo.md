---
aliases: [Geo Photos, Fotos Geolocalizadas]
tags: [proyecto, fullstack, django, gis, mapas, destacado]
categoria: Full-Stack / GIS
complejidad: Alta
estado: Completado
horas_estimadas: "60-80h"
---

# Geo Photos Demo

> [!tip] GIS + Fotografia
> Aplicacion web para gestion de fotos geolocalizadas con mapa interactivo y georreferenciacion de planos.

## Contexto

Aplicacion Django para visualizar fotografias en un mapa segun sus coordenadas GPS, extraidas automaticamente de los metadatos EXIF. Ademas permite georreferenciar planos arquitectonicos sobre el mapa.

**Problema que resuelve:** En proyectos de ingenieria civil/inmobiliaria, se toman cientos de fotos en campo. Esta herramienta las organiza automaticamente en un mapa segun donde fueron tomadas, sin intervencion manual.

## Repositorio

`Gneomar/geo-photos-demo` (publico)
**Fecha:** Diciembre 2025

## Stack tecnico

| Componente | Tecnologia |
|-----------|-----------|
| **Backend** | Django 5.0.3 |
| **Mapa** | Leaflet.js + OpenStreetMap |
| **EXIF** | exifread (extraccion de metadatos GPS) |
| **Imagenes** | Pillow (procesamiento) |
| **UI** | Bootstrap 5 |
| **DB** | SQLite |

## Funcionalidades

### Mapa interactivo
- Leaflet.js con tiles de OpenStreetMap
- Marcadores en las coordenadas GPS de cada foto
- Popup con preview de la foto al hacer click
- Control de capas para mostrar/ocultar diferentes tipos de contenido

### Extraccion automatica de GPS
- Lee metadatos EXIF de archivos JPG/PNG
- Extrae latitud, longitud y altitud si estan disponibles
- Calcula coordenadas decimales desde formato DMS (grados/minutos/segundos)

### Georreferenciacion de planos
- Permite subir un plano arquitectonico (imagen)
- Se definen 4 vertices con coordenadas GPS
- El plano se superpone sobre el mapa con la transformacion correcta
- Util para ver planos de obra sobre el terreno real

### Dashboard
- Estadisticas: total de fotos, fotos con GPS, fotos sin GPS
- Galeria de fotos con thumbnails
- Subida multiple de archivos

### Admin Django
- Panel de administracion completo para gestionar fotos y planos
- CRUD de todos los modelos

## Que lo hace destacable

- **Automatizacion EXIF**: No requiere input manual — las fotos se geolocalizan solas
- **Georreferenciacion**: Feature avanzado de GIS que permite superponer planos sobre mapas
- **Background de ingenieria civil**: Demuestra conocimiento de dominio que no tiene un developer comun
- **Repo publico**: Uno de los pocos proyectos publicos, disponible para revision
