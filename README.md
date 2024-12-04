# Descripción del Proyecto

**Film Junky Union**, una nueva comunidad vanguardista para los aficionados de las películas clásicas, está desarrollando un sistema para filtrar y categorizar reseñas de películas. Tu objetivo es entrenar un modelo para detectar las críticas negativas de forma automática. Para lograrlo, utilizarás un conjunto de datos de reseñas de películas de IMDB con etiquetado para construir un modelo que clasifique las reseñas como positivas y negativas. Este deberá alcanzar un valor F1 de al menos 0.85.

## Descripción de los Datos

Los datos se almacenan en el archivo `imdb_reviews.tsv`.

Los datos fueron proporcionados por Andrew L. Maas, Raymond E. Daly, Peter T. Pham, Dan Huang, Andrew Y. Ng, y Christopher Potts. (2011). Learning Word Vectors for Sentiment Analysis. La Reunión Anual 49 de la Asociación de Lingüística Computacional (ACL 2011).

### Campos seleccionados:
- `review`: el texto de la reseña
- `pos`: el objetivo, '0' para negativo y '1' para positivo
- `ds_part`: 'entrenamiento'/'prueba' para la parte de entrenamiento/prueba del conjunto de datos, respectivamente

Hay otros campos en el conjunto de datos, puedes explorarlos si lo deseas.

## Comentarios

- No se encontraron valores duplicados en el conjunto de datos, lo que indica que no es necesario realizar acciones adicionales para tratar duplicados.
- Identificamos valores NaN en dos columnas, pero estas no son relevantes para el análisis ni para el objetivo principal del proyecto, por lo que no afectarán los resultados.
- La columna `pos` presenta una distribución equilibrada de sus categorías, lo que confirma que no hay un problema de desequilibrio de clases en los datos.
- El conjunto de datos contiene la información esencial requerida para el análisis, lo que permite proceder con confianza hacia las siguientes etapas del proyecto.

## Entrenamiento de Modelos

Entrenamos al menos tres modelos diferentes para el conjunto de datos de entrenamiento y los probamos para el conjunto de datos de prueba.

### Modelos entrenados:

#### Modelo de Regresión Logística
Este modelo se entrenó usando un valor de `C=0.01` y el solver `liblinear`.

#### Modelo de Árbol de Decisión
Este modelo se entrenó con una profundidad máxima de 15.

#### Modelo Random Forest
Este modelo se entrenó con 200 estimadores y una profundidad máxima de 20.

### F1 Scores de los Modelos

- **Regresión Logística**: 0.88
- **Árbol de Decisión**: 0.77
- **Random Forest**: 0.85

#### Predicciones de Modelos para Nuevas Reseñas

- **Regresión Logística**: [1, 0, 0]
- **Árbol de Decisión**: [1, 0, 1]
- **Random Forest**: [1, 1, 1]

## Comparaciones

Los resultados muestran que la **Regresión Logística** obtuvo el mejor desempeño con una puntuación de 0.88, seguida de **RandomForestClassifier** con 0.85 y finalmente **DecisionTreeClassifier** con 0.77.

- La **Regresión Logística** destaca por su simplicidad y es especialmente efectiva cuando los datos no presentan relaciones complejas, lo que explica su buen desempeño en este caso.
- El modelo **RandomForestClassifier** demostró ser más robusto frente al sobreajuste en comparación con **DecisionTreeClassifier**, capturando mejor las relaciones presentes en los datos gracias a su enfoque basado en múltiples árboles.
- Aunque es posible optimizar los hiperparámetros de los modelos, los resultados actuales son suficientes para realizar un análisis preliminar y tomar decisiones fundamentadas.

## Comparación Adicional con TF-IDF

- **TF-IDF Logistic Regression F1**: 0.8955974842767296

### Probamos las reseñas anteriormente usadas con los modelos anteriores.

- **TF-IDF Logistic Regression Predictions**: [1, 0, 0]

## Conclusiones Finales

Los proyectos de clasificación con **Regresión Logística** en lenguaje natural destacan por su simplicidad y efectividad. La parte más desafiante del proceso radica en la preparación de los datos de texto, específicamente en las etapas de tokenización y lemmatización, aunque hoy en día existen herramientas y modelos preentrenados que simplifican estas tareas.

Las técnicas de procesamiento de texto varían desde las más simples, como **CountVectorizer** y **TF-IDF**, hasta modelos más avanzados como **BERT**. Este último sobresale por su capacidad para entender el contexto semántico de los textos, aunque requiere mayor tiempo y recursos computacionales debido a su complejidad. En este proyecto, logramos identificar que la **Regresión Logística** es el algoritmo más adecuado para problemas de esta naturaleza, destacando su balance entre simplicidad y desempeño.

Usando **TF-IDF** como técnica de vectorización, alcanzamos un **F1-Score** de 0.89 con **Regresión Logística**, lo que representa una mejora significativa frente a otras técnicas más simples.

Aunque intentamos implementar **BERT**, el procesamiento en lotes de 100 reseñas resultó extremadamente lento (más de 40 minutos sin resultados finales), lo que refuerza la necesidad de recursos especializados para su uso efectivo.

Notamos que con **TF-IDF**, el **F1-Score** se incrementó hasta un 89.6%, mostrando su capacidad para capturar características relevantes del texto.

Es importante destacar que los modelos con **F1-Scores** de 88% o superiores lograron clasificar correctamente todas las reseñas evaluadas, lo que refuerza su confiabilidad para este tipo de tareas.
