# roldyoran

Este proyecto utiliza `selenium`, `BeautifulSoup`, `re` y `colorama` para extraer información de un sitio web de clasificación de animes y guarda los datos en un archivo JSON mediante la libreria `json`.

## Requisitos

- Python 3.12+
- Selenium
- BeautifulSoup
- Colorama
- Un navegador web (Chrome)

## Instalación

1. Clona este repositorio en tu máquina local.
2. Dirigete a la carpeta:
```sh
cd scrap-tiermaker
```
* Crea un entorno virtual (opcional)
```sh
python -m venv venv
```
* Activa el entorno Virtual
```sh
# Para LINUX
./venv/Scripts/activate

# Para WINDOWS
.\venv\Scripts\activate
```

3. Instala las dependencias necesarias ejecutando:
```sh
pip install selenium beautifulsoup4 colorama
```
4. Ejecuta el Script:
```sh
python app.py
```