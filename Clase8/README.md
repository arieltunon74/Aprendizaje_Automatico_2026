# Segmentación de Clientes - Aprendizaje No Supervisado

## Descripción General
Este repositorio contiene el análisis e implementación de un modelo de **Segmentación de Clientes** desarrollado en el marco de la **Clase 8: Aprendizaje No Supervisado**.

El objetivo principal de este proyecto fue validar experimentalmente la hipótesis inicial planteada por el equipo directivo/ventas: **determinar si los datos de los clientes se agrupan de forma natural en 3 segmentos latentes ($K = 3$)**. Mediante técnicas de Machine Learning, transformamos datos de comportamiento en perfiles comerciales accionables.

---

## Metodología y Flujo de Trabajo

El proyecto sigue el flujo estándar de un proyecto de Aprendizaje No Supervisado:

1. **Análisis Exploratorio de Datos (EDA) y Selección de Variables:**
   * Eliminación de variables de ruido o sin valor discriminativo.
   * Selección de métricas clave: `purchase_freq_month`, `avg_basket_usd`, `time_on_site_min`, `discount_sensitivity` y `returns_rate`.

2. **Preprocesamiento de Datos:**
   * Escalado de características con `StandardScaler` para corregir la varianza de escala, garantizando cálculos equitativos de distancia euclidiana entre variables.

3. **Optimización de Hiperparámetros y Validación de Clústeres:**
   * Evaluación de configuraciones para $K$ entre 2 y 6.
   * Aplicación del **Método del Codo (Inercia/WCSS)** y el **Coeficiente de Silhouette**.
   * **Resultado:** $K = 3$ obtuvo el Coeficiente de Silhouette más alto ($0.4305$), validando empíricamente la hipótesis del gerente.

4. **Entrenamiento del Modelo e Interpretación de Centroides:**
   * Entrenamiento del modelo `KMeans` definitivo con $n\_clusters = 3$.
   * Cálculo de los centroides en la escala original de los datos para caracterizar los grupos.

5. **Reducción de Dimensionalidad y Visualización:**
   * Aplicación de **Análisis de Componentes Principales (PCA)** para comprimir las 5 variables en un espacio 2D.
   * Visualización gráfica de la separación entre clústeres y la posición de los centroides ($\mathbf{X}$).

---

## Perfiles de los Segmentos Identificados

A partir del análisis de centroides des-estandarizados, se identificaron 3 perfiles comerciales:

* **Clúster 0 — Clientes Frecuentes Sensibles a Promociones:** Alta permanencia en plataforma y frecuencia de compra mensual, acompañadas por una marcada respuesta a descuentos.
* **Clúster 1 — Clientes Premium de Alto Valor:** Menor frecuencia de visita, pero con montos de ticket promedio (`avg_basket_usd`) significativamente elevados y baja tasa de devolución.
* **Clúster 2 — Compradores Ocasionales de Bajo Ticket:** Baja interacción en la plataforma, menor gasto por transacción y sensibilidad moderada.

---

## Cómo Ejecutar el Proyecto

### Requisitos Previos
* Python 3.8+
* Jupyter Notebook / Google Colab

### Dependencias
Instalar las librerías necesarias ejecutando:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

### Ejecución
Ejecutar el cuaderno Jupyter de manera secuencial:
1. Carga y limpieza del conjunto de datos.
2. Estandarización de variables con `StandardScaler`.
3. Entrenamiento del algoritmo K-Means ($K=3$).
4. Generación del gráfico PCA en 2D y mapas de calor (heatmaps).

---

## Limitaciones del Modelo

* **Sesgo Cuantitativo:** El análisis utiliza únicamente 5 variables continuas; no se incluyeron datos demográficos o cualitativos.
* **Sensibilidad a Outliers:** Al basarse en distancias euclidianas, K-Means es sensible a valores extremadamente atípicos.
* **Naturaleza Dinámica:** El comportamiento del consumidor cambia con el tiempo, por lo que los clústeres deben re-evaluarse periódicamente.

---

## Conclusión
El enfoque de aprendizaje no supervisado validó de forma empírica la hipótesis del negocio sin requerir etiquetas previas, proporcionando al equipo de marketing una estructura clara para el diseño de campañas personalizadas.