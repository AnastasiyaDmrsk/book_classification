# Clasificación de Libros por Género

## Descripción del Proyecto

Este proyecto tiene como objetivo predecir automáticamente el género de un libro (como fantasía, romance, historia, etc.) utilizando únicamente su título y sinopsis. A diferencia de enfoques anteriores que dependían de datasets preconstruidos, este trabajo extrae datos directamente desde la web, lo que lo hace más dinámico y adaptable.

### Fuente de Datos

- Se extraen automáticamente los títulos de libros del sitio WorldCat Top 500: [Top 500 de WorldCat](https://www.oclc.org/en/worldcat/library100/top500.html)
- Posteriormente, se utiliza la [Open Library API](https://openlibrary.org/developers/api) para obtener las descripciones de los libros.
- Los títulos, descripciones y géneros inferidos se guardan en un archivo CSV: `classic_books_data.csv`.

## Tecnologías y Herramientas

- **Python** para scraping, procesamiento y modelado
- **BeautifulSoup** para extraer información del HTML
- **Requests** para interactuar con APIs y páginas web
- **Open Library API** para obtener sinopsis reales
- **Scikit-learn** y **Transformers (HuggingFace)** para entrenar y evaluar modelos de clasificación de texto

## Flujo del Proyecto

1. Extracción de títulos desde WorldCat
2. Obtención de descripciones usando Open Library API
3. Clasificación automática del género del libro utilizando modelos previamente entrenados (Naive Bayes, Logistic Regression, SVM, Transformers, etc.)
4. Evaluación de los resultados con métricas como F1 Score

## Estructura del CSV Final

El archivo `classic_books_data.csv` generado contiene las siguientes columnas:
- `title`: título del libro
- `description`: sinopsis del libro extraída de Open Library
- `categories`: categoria del libro de Open Library

## Resultados y Conclusiones

| Modelo                | Accuracy | F1 Score (ponderado) |
|------------------------|----------|----------------------|
| Naive Bayes           | 0.667    | 0.533                |
| Regresión Logística   | 0.667    | 0.533                |
| Random Forest         | 0.667    | 0.533                |
| SVM                   | 0.697    | 0.574                |
| **DistilBERT**        | 0.667    | 0.533                |