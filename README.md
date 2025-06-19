# Tiermaker Anime Scraper

## Descripción

Este proyecto es un scraper web asíncrono diseñado para extraer información de animes desde una lista de Tiermaker específica. Utiliza Playwright para navegación web automatizada y BeautifulSoup para el parsing de HTML, con capacidades de reintentos, manejo de protecciones de Cloudflare y actualización inteligente de datos.

## Características

- ✨ **Scraping asíncrono** con Playwright
- 🔄 **Sistema de reintentos automáticos** (hasta 3 intentos)
- 🛡️ **Bypass de protecciones Cloudflare**
- 📊 **Interfaz visual con Rich** (barras de progreso y colores)
- 🔧 **Actualización inteligente de datos** (preserva datos existentes)
- 💾 **Respaldo automático** de archivos
- 🔀 **Sistema de intercambios personalizados**

## Instalación

### Prerrequisitos

Asegúrate de tener Python 3.7+ instalado en tu sistema.

### Dependencias

Instala las dependencias necesarias ejecutando:

```bash
pip install playwright beautifulsoup4 rich asyncio
```

### Configuración de Playwright

Después de instalar Playwright, ejecuta:

```bash
playwright install chromium
```

## Estructura del Proyecto

```
proyecto/
├── main.py              # Script principal
├── original.json        # Archivo de respaldo con datos originales
├── animes_updated.json  # Archivo de salida actualizado
├── README.md            # Este archivo
└── requirements.txt     # Archivo para instalar las dependencias directamente
```

## Uso

### Ejecución básica

```bash
python main.py
```

### Configuración

El script está configurado para scraper la siguiente URL por defecto:
```python
URL = "https://tiermaker.com/create/animes-random-saikomic-16203118"
```

Puedes modificar esta URL en la función `main()` si necesitas scraper una lista diferente.

## Funcionalidades Detalladas

### 1. Extracción de Datos (`fetch_page_content`)

- Lanza un navegador Chromium en modo headless
- Incluye headers personalizados para evitar detección
- Maneja protecciones de Cloudflare automáticamente
- Sistema de reintentos con delays progresivos

### 2. Procesamiento de Datos (`extract_data`)

Extrae la siguiente información de cada anime:
- **Nombre**: Extraído de la URL de la imagen usando expresiones regulares
- **ID**: Identificador único del elemento
- **URL**: Enlace de la imagen del anime

### 3. Comparación y Actualización (`compare_anime_data`)

- Preserva campos personalizados como 'nota' de datos existentes
- Mantiene URLs y nombres modificados manualmente
- Ejecuta intercambios automáticos predefinidos
- Añade nuevos animes sin sobrescribir existentes

### 4. Sistema de Intercambios

El script incluye un sistema para intercambiar posiciones de animes específicos:

```python
INTERCAMBIOS_SIMPLE = {
    "458": "225",  # Intercambia anime ID 458 con ID 225
    "469": "196",  # Intercambia anime ID 469 con ID 196
}
```

### 5. Guardado Seguro (`save_to_json`)

- Guarda datos en `animes_updated.json`
- Crea respaldo automático en `original.json`
- Manejo de errores durante el guardado

## Formato de Datos

Los datos se guardan en formato JSON con la siguiente estructura:

```json
[
    {
        "nombre": "NombreDelAnime",
        "id": "123",
        "url": "https://tiermaker.com/images/...",
        "nota": "Comentario opcional (si existe)"
    }
]
```

## Configuración Avanzada

### Modificar Timeouts

```python
# En fetch_page_content()
await page.goto(url, wait_until="load", timeout=30000)  # 30 segundos
await page.wait_for_timeout(12000)  # 12 segundos de espera adicional
```

### Personalizar User Agent

```python
'--user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36...'
```

### Agregar Nuevos Intercambios

Modifica el diccionario `INTERCAMBIOS_SIMPLE` en la función `compare_anime_data()`:

```python
INTERCAMBIOS_SIMPLE = {
    "ID_ORIGEN": "ID_DESTINO",
    "458": "225",
    "469": "196",
    # Agrega más intercambios aquí
}
```

## Manejo de Errores

El script incluye manejo robusto de errores:

- **Errores de conexión**: Reintentos automáticos con delays
- **Elementos no encontrados**: Mensajes claros de error
- **Protecciones web**: Detección y bypass automático
- **Errores de guardado**: Preservación de datos originales

## Logging y Monitoreo

El script utiliza Rich Console para proporcionar feedback visual:

- 🟡 **Amarillo**: Intentos de conexión
- 🔴 **Rojo**: Errores y problemas
- 🟢 **Verde**: Operaciones exitosas
- 🔵 **Azul**: Procesamiento de datos

## Solución de Problemas

### Error: "No se encontraron elementos de anime"

- Verifica que la URL sea correcta
- Asegúrate de que la página cargue completamente
- Revisa si hay cambios en la estructura HTML del sitio

### Error: "Detectada protección de Cloudflare"

- El script maneja automáticamente este caso
- Si persiste, aumenta los timeouts en la configuración

### Problemas de instalación de Playwright

```bash
# Reinstalar navegadores
playwright install --force

# Verificar instalación
playwright --version
```

## Contribución

Para contribuir al proyecto:

1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -am 'Agregar nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Crea un Pull Request

## Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.

## Contacto

Para preguntas o sugerencias, puedes crear un issue en el repositorio del proyecto.

---

**Nota**: Este scraper está diseñado para uso educativo y personal. Asegúrate de cumplir con los términos de servicio del sitio web objetivo.