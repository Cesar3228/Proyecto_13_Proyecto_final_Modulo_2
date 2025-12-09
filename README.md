# Proyecto_13_Proyecto_final_Modulo_2
## Predicción de recuperación de oro  
## Gold Recovery Prediction

---

## 🧩 Descripción general / Overview

### 🇪🇸 Español

En este proyecto se trabaja con datos reales de un **proceso industrial de extracción de oro**, cuyo objetivo es **predecir la recuperación del metal** en diferentes etapas del proceso de purificación.

El proceso incluye etapas como *rougher*, *limpieza primaria* y *concentrado final*, donde las concentraciones de metales cambian progresivamente.  
Un reto clave del proyecto es que **algunas características no están disponibles en el conjunto de prueba**, ya que se calculan o miden mucho después del momento de la predicción.

El objetivo es construir un modelo de **Machine Learning** que prediga la recuperación del oro utilizando la métrica **sMAPE (Symmetric Mean Absolute Percentage Error)**.

Este proyecto corresponde al **Proyecto 13 – Machine Learning para procesos industriales** del programa de **Data Science de TripleTen**.

---

### 🇬🇧 English

This project uses real industrial data from a **gold extraction process**, with the goal of **predicting gold recovery** at different purification stages.

The process includes stages such as *rougher*, *primary cleaner*, and *final concentrate*, where metal concentrations evolve over time.  
A key challenge is that **some features are not available in the test set**, as they are measured or calculated much later in the process.

The goal is to build a **Machine Learning model** that predicts gold recovery using **sMAPE (Symmetric Mean Absolute Percentage Error)** as the primary metric.

This project corresponds to **Project 13 – Machine Learning for Industrial Processes** in the **TripleTen Data Science program**.

---

## 📂 Datos / Data

### Archivos / Files
- `gold_recovery_train.csv` — conjunto de entrenamiento  
- `gold_recovery_test.csv` — conjunto de prueba  
- `gold_recovery_full.csv` — dataset fuente  

Los datos están indexados por **fecha y hora (`date`)**, por lo que observaciones cercanas en el tiempo tienden a ser similares.

> **Nota / Note:**  
> Los datos no se incluyen en este repositorio debido a restricciones de la plataforma **TripleTen**.  
> The datasets are not included due to **TripleTen platform restrictions**.

---

## 🧪 Verificación de la recuperación / Recovery Verification

### 🇪🇸 Español

Se verificó la corrección del cálculo de la recuperación (`rougher.output.recovery`) utilizando la fórmula proporcionada en el proyecto.  
El **Error Absoluto Medio (MAE)** entre los valores calculados y los valores originales fue:

- **MAE = 9.30 × 10⁻¹⁵**

Este valor cercano a cero confirma que el cálculo de la recuperación es **correcto**.

---

### 🇬🇧 English

The recovery calculation (`rougher.output.recovery`) was validated using the formula provided in the project instructions.  
The **Mean Absolute Error (MAE)** between the calculated values and the original dataset values was:

- **MAE = 9.30 × 10⁻¹⁵**

This near-zero value confirms that the recovery calculation is **correct**.

---

## 🚫 Características no disponibles en el conjunto de prueba  
## Missing Features in the Test Set

Las siguientes características están presentes en el conjunto de entrenamiento pero **no están disponibles en el conjunto de prueba** porque se calculan en etapas posteriores del proceso:

- Características de salida (`output`) y recuperación de:
  - *rougher*
  - *primary_cleaner*
  - *secondary_cleaner*
  - *final*
- Variables de tipo:
  - concentrados
  - colas (tails)
  - métricas de recuperación
  - variables calculadas del proceso

Estas características **no pueden utilizarse para el entrenamiento del modelo**, ya que no estarían disponibles en un escenario real de predicción.

---

## 🔍 Metodología / Methodology

### 🇪🇸 Español

1. **Preparación de datos**
   - Eliminación de columnas no disponibles en el conjunto de prueba.
   - Manejo de valores faltantes.
   - Separación de variables objetivo:
     - `rougher.output.recovery`
     - `final.output.recovery`

2. **Análisis exploratorio**
   - Análisis de la evolución de las concentraciones de **Au, Ag y Pb** a lo largo de las etapas.
   - Comparación del tamaño de partículas entre entrenamiento y prueba.
   - Identificación y eliminación de valores anómalos en concentraciones totales.

3. **Construcción del modelo**
   - Implementación de una función personalizada para el cálculo de **sMAPE**.
   - Entrenamiento y evaluación de múltiples modelos mediante **validación cruzada**.

---

## 📐 Métrica de evaluación / Evaluation Metric

### sMAPE (Symmetric Mean Absolute Percentage Error)

Se utiliza una métrica personalizada que combina la sMAPE del proceso *rougher* y del concentrado final, conforme a las especificaciones del proyecto.

---

## 🤖 Modelos y Resultados / Models and Results

### Modelos evaluados
- **LinearRegression**
- **RandomForestRegressor**

### Resultados por validación cruzada

| Modelo | sMAPE (CV) |
|------|-----------|
| LinearRegression | 9.334% |
| RandomForestRegressor | **7.038%** ✅ |

🏆 **Mejor modelo:** `RandomForestRegressor`

---

### 📊 Resultados en el conjunto de prueba

El modelo final (`RandomForestRegressor`) fue evaluado en el conjunto de prueba, generando predicciones tanto para:

- `rougher.output.recovery`
- `final.output.recovery`

Ejemplo de predicciones en el conjunto de prueba:

| rougher.output.recovery | final.output.recovery |
|------------------------|-----------------------|
| 88.94 | 69.26 |
| 86.73 | 69.89 |
| 87.42 | 68.85 |
| 86.93 | 69.20 |
| 88.08 | 68.71 |

---

## 📁 Estructura del repositorio / Repository Structure

```text
.
├── Proyecto_13.ipynb
├── requirements.txt
└── README.md
