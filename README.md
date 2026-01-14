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

## Práctica 2: Clasificación de imágenes

### Dataset

**Oxford-IIIT Pet Dataset**
[https://www.kaggle.com/datasets/tanlikesmath/the-oxfordiiit-pet-dataset](https://www.kaggle.com/datasets/tanlikesmath/the-oxfordiiit-pet-dataset)

* Imágenes RGB de perros y gatos
* Alta variabilidad visual
* Problema: **Clasificación de imágenes**

### Modelos aplicados

* **SVM (LinearSVC)**
* **CNN (Convolutional Neural Network)**

### Flujo del proceso

1. Carga de imágenes
2. Conversión a escala de grises
3. Redimensionamiento (64×64)
4. Vectorización (SVM)
5. Entrenamiento de modelos
6. Visualización XAI

### Enfoque XAI

* **SVM**: visualización de pesos como mapas de calor
* **CNN**: análisis de regiones activadas (conceptual)

### Resultados clave

* SVM genera mapas ruidosos
* Falta de alineación espacial en imágenes
* Los píxeles no representan semántica fija

### Limitaciones detectadas

* El SVM busca correlaciones espaciales rígidas
* No captura jerarquías visuales
* Explicabilidad matemática ≠ explicabilidad semántica

### Conclusión práctica 2

Aunque el SVM es explicable matemáticamente, **no es adecuado para visión por computador compleja**. Las CNN son superiores, pero requieren técnicas XAI adicionales.

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
 ┃ ┣ SMV_Uzhca.ipynb
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
