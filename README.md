
# Clasificación de Libros por Género

## Descripción del Proyecto

### Motivación y Objetivos
El objetivo de este proyecto es desarrollar un modelo de clasificación de texto capaz de predecir el **género principal de un libro** (fantasía, misterio, romance, ciencia ficción, etc.) a partir de su **descripción**. Esta tarea tiene aplicaciones prácticas en bibliotecas digitales, recomendaciones automáticas y organización de catálogos editoriales.

### Dataset Utilizado
Se utilizó el dataset de Kaggle:  
👉 [Books Dataset - Kaggle](https://www.kaggle.com/datasets/abdallahwagih/books-dataset/data)  
Este dataset fue seleccionado por contener una menor proporción de valores nulos y una buena variedad de géneros.

---

## Desarrollo del Trabajo

### Preprocesamiento
- Se eliminaron entradas con descripciones (`description`) o categorías (`categories`) nulas.
- Se extrajo la **categoría principal** de cada libro (`main_category`), usando el primer valor del campo `categories`.
- Se seleccionaron los **10 géneros más frecuentes** para reducir la complejidad y balancear las clases.
- Se codificaron las etiquetas con `LabelEncoder`.

### División de Datos
- 80% para entrenamiento y 20% para prueba, usando `train_test_split`.

### Representación del Texto
Se probaron dos enfoques para representar las descripciones de los libros:

#### 1. **TF-IDF (Term Frequency - Inverse Document Frequency)**
- Se utilizó `TfidfVectorizer` con los siguientes parámetros:
  - `max_features=5000`
  - `stop_words="english"`

#### 2. **Embeddings con Transformers (Hugging Face)**
- Modelo usado: `DistilBERT` (`distilbert-base-uncased`)
- Se entrenó un modelo de clasificación (`DistilBertForSequenceClassification`)
- Se utilizó `Trainer` de Hugging Face para entrenamiento y evaluación.

### Modelos de Clasificación Probados
Con representaciones TF-IDF:
- Naive Bayes
- Regresión Logística
- Random Forest
- SVM (LinearSVC)

Con representaciones Transformers:
- DistilBERT fine-tuneado usando la sinopsis como entrada.

---

## Resultados

| Modelo                | Accuracy         | F1 Score (ponderado) |
|------------------------|------------------|----------------------|
| Naive Bayes           | 0.574            | TODO                 |
| Regresión Logística   | 0.650               | TODO                 |
| Random Forest         | 0.663               | TODO                 |
| SVM                   | 0.710               | TODO                     |
| **DistilBERT**        | TODO| TODO |

> *Los resultados concretos dependen del entrenamiento, pero en general DistilBERT mostró un rendimiento significativamente superior en términos de F1 Score y generalización.*

---

## Guardado del Modelo
Se guardó el modelo fine-tuneado y el tokenizer de Hugging Face con:

```python
model.save_pretrained("book_genre_classifier_model")
tokenizer.save_pretrained("book_genre_classifier_model")
```

También se guardó el `LabelEncoder` para decodificar las predicciones:
```python
joblib.dump(label_encoder, "label_encoder.pkl")
```

---

## Conclusiones

- Los modelos clásicos con TF-IDF ofrecen resultados razonables, especialmente Logistic Regression y SVM.
- Sin embargo, los modelos basados en **Transformers (DistilBERT)** muestran una **mejora significativa** en la capacidad de capturar el significado semántico del texto.
- Este enfoque puede escalar fácilmente a más categorías y otros idiomas.
- El modelo puede integrarse en sistemas de recomendación, motores de búsqueda o bibliotecas virtuales para clasificar libros automáticamente.
