# Script de Actualización de Lista de Animes

## Descripción General
Este script `app.py` es una herramienta automatizada diseñada para extraer y actualizar información de animes desde Tiermaker. El script mantiene una lista actualizada de animes mientras preserva datos personalizados como notas y URLs específicas.

## Características Principales
- Extracción automática de datos de Tiermaker
- Preservación de datos personalizados existentes
- Manejo asíncrono de operaciones web
- Sistema robusto de extracción de datos mediante expresiones regulares
- Actualización inteligente de registros existentes

## Requisitos
```
playwright
beautifulsoup4
asyncio
```

## Funciones Principales

### `fetch_page_content(url)`
- Función asíncrona que obtiene el contenido de la página
- Utiliza Playwright para la navegación web automatizada
- Implementa esperas inteligentes para asegurar la carga completa
- Configuración anti-detección de bots

### `extract_data(content)`
- Procesa el HTML para extraer información de animes
- Utiliza BeautifulSoup para el parsing
- Extrae URLs de imágenes y nombres mediante regex
- Limpia y formatea los nombres de animes

### `compare_anime_data(anime_data_list, filename)`
- Compara y actualiza datos con el archivo original
- Preserva notas existentes
- Mantiene URLs personalizadas
- Maneja casos especiales de reordenamiento

### `save_to_json(anime_data_list, filename)`
- Guarda los datos actualizados en formato JSON
- Preserva el formato UTF-8 para caracteres especiales

## Estructura de Datos

### Formato del Archivo JSON
```json
[
    {
        "id": "string",       // Identificador único del anime
        "nombre": "string",   // Nombre del anime
        "url": "string",      // URL de la imagen
        "nota": "string"      // Nota opcional personalizada
    }
]
```

## Uso
1. Asegúrate de tener los requisitos instalados
2. Ejecuta el script:
   ```bash
   python app.py
   ```
3. El script generará/actualizará `animes_updated.json`

## Notas Importantes
- El script requiere conexión a internet
- Mantén un archivo `original.json` con la estructura correcta
- Las notas y URLs personalizadas se preservarán durante la actualización
- El script incluye un manejo especial para reordenar ciertos animes específicos (IDs: 458 y 225)

### 4. Procesamiento de Datos
Implementa un sistema de actualización que:
- Mantiene datos existentes de `original.json`
- Actualiza entradas modificadas
- Agrega nuevos personajes
- Preserva notas y URLs personalizadas

### 5. Sistema de Logging
Utiliza la biblioteca `rich` para proporcionar:
- Barras de progreso interactivas
- Tablas de resumen
- Paneles informativos
- Logging con colores

## Flujo de Ejecución
1. Inicialización del navegador con configuraciones anti-detección
2. Navegación a la URL de Tiermaker
3. Manejo de protección Cloudflare
4. Extracción de datos de personajes
5. Carga y procesamiento de datos existentes
6. Actualización y fusión de información
7. Generación de reportes
8. Guardado de datos actualizados

## Estructura de Datos

### Formato de Entrada (original.json)
```json
[
    {
        "id": "string",
        "nombre": "string",
        "url": "string",
        "nota": "string (opcional)"
    }
]
```

### Formato de Salida (anime_list.json)
```json
[
    {
        "id": "string",
        "nombre": "string",
        "url": "string",
        "nota": "string (si existe en original)"
    }
]
```

## Manejo de Errores
- Captura de errores de navegación
- Generación de screenshots en caso de error
- Logging detallado de problemas
- Fallbacks para patrones de extracción

## Métricas y Reportes
Genera reportes detallados incluyendo:
- Total de personajes encontrados
- Número de actualizaciones
- Nuevas adiciones
- Cambios en URLs y nombres

## Requisitos del Sistema
- Python 3.7+
- Playwright
- BeautifulSoup4
- Rich
- Conexión a Internet estable
- Memoria suficiente para procesamiento de datos

## Limitaciones Conocidas
- Dependencia de la estructura HTML de Tiermaker
- Sensibilidad a cambios en la protección anti-bot
- Necesidad de conexión estable a Internet
- Tiempo de espera para bypass de Cloudflare
        