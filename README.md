# XAI – Interpretación de Modelos de Machine Learning y Deep Learning

## Descripción general del proyecto

Este proyecto presenta un **estudio técnico y experimental sobre Explainable Artificial Intelligence (XAI)**, aplicando y comparando modelos de *Machine Learning clásico* y *Deep Learning* sobre **datos estructurados** e **imágenes**, con el objetivo de **interpretar, analizar y explicar las predicciones** de cada modelo.

El trabajo se centra en responder una pregunta clave:

> ¿Cómo y por qué un modelo toma una decisión, más allá de su precisión?

Para ello, se desarrollaron **dos prácticas complementarias**, integradas bajo un mismo marco conceptual de explicabilidad.

---

## Objetivos

### Objetivo general

Analizar y comparar modelos predictivos desde la perspectiva de **XAI**, evaluando su desempeño y su capacidad de explicación.

### Objetivos específicos

* Aplicar modelos interpretables y no interpretables en distintos tipos de datos.
* Identificar **características importantes** y **factores clave** en las predicciones.
* Visualizar y analizar explicaciones globales y locales.
* Evidenciar las limitaciones de la interpretabilidad en modelos complejos.

---

## Marco conceptual: XAI

**Explainable Artificial Intelligence (XAI)** busca hacer transparentes los modelos de IA, permitiendo:

* Comprender decisiones del modelo
* Generar confianza
* Detectar sesgos
* Facilitar la toma de decisiones humanas

Este proyecto contrasta:

* **Modelos inherentemente interpretables** (Árboles, Random Forest, SVM)
* **Modelos de alta complejidad** (Redes Neuronales, CNN)

---

## Práctica 1: Datos estructurados

### Dataset

**Online Shoppers Purchasing Intention Dataset**
[https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset](https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset)

* Variables numéricas y categóricas
* Variable objetivo: `Revenue` (0 = No compra, 1 = Compra)
* Problema: **Clasificación binaria**

### Modelos aplicados

* **Random Forest / Árbol de Decisión**
* **Red Neuronal Artificial (MLP)**

### Flujo del proceso

1. Carga de datos y análisis exploratorio (EDA)
2. Preprocesamiento:

   * Variables dummy
   * Escalado con `StandardScaler`
3. Entrenamiento de modelos
4. Evaluación de métricas
5. Análisis XAI

### Características importantes (XAI)

* `PageValue` → Variable más influyente
* `ExitRates` y `BounceRates`
* `ProductRelated` y duración
* `VisitorType`

### Resultados clave

* Ambos modelos identifican **PageValue** como factor determinante
* El **Árbol de Decisión** reduce falsos negativos
* Mejor interpretación de patrones lógicos de compra

### Ventajas y desventajas

**Random Forest / Árbol**

* ✔ Alta interpretabilidad
* ✔ Explicación directa de decisiones
* ✖ Menor capacidad para relaciones muy complejas

**Red Neuronal**

* ✔ Mayor capacidad de representación
* ✖ Modelo tipo *caja negra*

### Conclusión práctica 1

Los modelos basados en árboles resultan más adecuados cuando la **explicabilidad es prioritaria**, especialmente en contextos de negocio.

---

## Práctica 2: Clasificación de imágenes (Perros vs Gatos)

### Dataset

**Oxford-IIIT Pet Dataset**  
[https://www.kaggle.com/datasets/tanlikesmath/the-oxfordiiit-pet-dataset](https://www.kaggle.com/datasets/tanlikesmath/the-oxfordiiit-pet-dataset)

- Imágenes RGB de 37 razas de gatos y perros (en esta práctica: subconjunto binario **Gato vs Perro**)
- Alta variabilidad visual (posturas, iluminación, fondo, raza)
- **Tarea**: Clasificación binaria de imágenes

### Modelos aplicados

- **SVM** (LinearSVC) – baseline clásico
- **CNN** (Convolutional Neural Network) – enfoque deep learning

### Flujo del proceso

1. Carga y preprocesamiento de imágenes
2. Conversión a escala de grises + redimensionamiento (64×64)
3. Vectorización de imágenes (para SVM)
4. División train / validation / test
5. Entrenamiento de ambos modelos
6. Evaluación + visualización de explicabilidad (XAI)

### Enfoque XAI

- **SVM**: Visualización de los pesos del clasificador como mapa de calor
- **CNN**: Análisis conceptual de regiones activadas (enfoque cualitativo en esta práctica)

### Resultados clave

#### SVM
- Genera mapas de pesos **ruidosos** y poco interpretables
- Busca patrones espaciales rígidos → no captura bien la variabilidad natural de las imágenes
- Rendimiento inferior al de la CNN (no se detalla aquí la métrica exacta, pero visiblemente peor)

#### CNN
- **Accuracy final en conjunto de test**: **80.58%**
- Comportamiento durante el entrenamiento:
  - Accuracy en entrenamiento → sube de forma sostenida hasta ~98%
  - Accuracy en validación → se estabiliza alrededor de **~80–82%** (evidencia clara de **sobreajuste**)
  - Pérdida (loss) en entrenamiento → disminuye correctamente
  - Pérdida en validación → **aumenta** significativamente después de varias épocas → confirma sobreajuste

**Matriz de confusión (test)**

| True \ Predicted | Gato       | Perro      |
|------------------|------------|------------|
| **Gato**         | 288        | 192        |
| **Perro**        | 95         | 903        |

- Total de ejemplos de gatos: 288 + 192 = **480**
- Total de ejemplos de perros: 95 + 903 = **998**
- **Fuerte sesgo hacia la clase "Perro"** (el modelo predice "Perro" en la mayoría de los casos)
- Recall para "Gato" ≈ 60% (288/480) → muchos gatos clasificados erróneamente como perros
- Recall para "Perro" ≈ 90.5% (903/998) → muy buen desempeño en la clase mayoritaria

### Limitaciones detectadas

- **Sobreajuste evidente** en la CNN (divergencia train/val loss)
- Desbalance de clases en el conjunto de evaluación (~2:1 perros:gatos) → sesgo hacia la clase mayoritaria
- Preprocesamiento simple (grises + 64×64) → pérdida importante de información (color y resolución)
- El SVM, aunque matemáticamente interpretable, **no captura jerarquías visuales** → mapas de pesos poco semánticos
- Explicabilidad matemática (SVM) ≠ explicabilidad semántica/humanamente comprensible

### Conclusión práctica 2

Aunque el **SVM** ofrece explicabilidad directa a nivel de píxeles, **no es adecuado** para tareas de visión por computador con alta variabilidad como esta.  
Las **CNN** logran un rendimiento significativamente superior (**80.58%** en test), pero muestran **sobreajuste** 

---

## Relación global con XAI

Este proyecto demuestra que:

* La precisión no es suficiente
* La interpretabilidad depende del tipo de dato
* XAI actúa como puente entre modelos y usuarios

| Tipo de modelo | Precisión | Explicabilidad |
| -------------- | --------- | -------------- |
| Árboles        | Media     | Alta           |
| Random Forest  | Alta      | Media-Alta     |
| SVM            | Media     | Media          |
| CNN            | Muy alta  | Baja (sin XAI) |

---

## 📁 Estructura del proyecto

```
Proyecto-XAI
 ┣ 📂 data
 ┣ 📂 notebooks
 ┃ ┣ DecisionTree.ipynb
 ┃ ┣ SMV.ipynb
 ┃ ┣ CNN.ipynb
 ┣ 📄 README.md
 ┗ 📄 X-ai.pdf
```

---

## Autores

* **David Uzhca**
* **Domenika Delgado**
* **Irar Nankamai**

---

## Conclusión general

La **Explainable AI** es esencial para una adopción responsable de modelos de IA. Este proyecto evidencia que **comprender el porqué de una predicción es tan importante como el resultado mismo**, especialmente en contextos reales donde la confianza y la transparencia son fundamentales.
Depende mucho del conte
