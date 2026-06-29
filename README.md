# Talleres de Aprendizaje No Supervisado 🤖🍄💳

Este repositorio contiene dos talleres prácticos enfocados en la implementación, evaluación y visualización de algoritmos de **Aprendizaje No Supervisado** utilizando Python y la librería `scikit-learn`. 

Los proyectos abordan dos problemáticas de negocio y análisis muy comunes: la **clasificación biológica/validación mediante clustering** (datos categóricos) y la **segmentación de clientes para estrategias de marketing** (datos numéricos), además de técnicas para **detección de anomalías**.

---

## 📁 Estructura del Repositorio

* `workshop-clustering-Mushrooms.ipynb`: Notebook de la **Parte 1** enfocado en datos categóricos (Mushroom Dataset).
* `workshop-clustering-creditcard.ipynb`: Notebook de la **Parte 2** enfocado en datos numéricos de comportamiento financiero (Credit Card Dataset).
* `data/`: Carpeta sugerida para almacenar los conjuntos de datos en formato `.csv` (`mushrooms.csv` y `ccdata.csv`).

---

## 🍄 Parte 1: Dataset de Setas (Variables Categóricas)

### 📝 Descripción del Problema
El objetivo es analizar el comportamiento de algoritmos de clustering sobre un conjunto de datos que contiene características morfológicas de **8,124 setas**, donde todas las variables son categóricas. Aunque el dataset original incluye la etiqueta de clase (`e` = comestible, `p` = venenosa), esta **solo se utiliza al final para validar** la estructura descubierta por los modelos.

### 🛠️ Flujo de Trabajo y Técnicas
1.  **Limpieza e Imputación**: 
    * Identificación de valores nulos ocultos (`'?'` en la variable `stalk-root`) e imputación con la moda.
    * Eliminación de variables con varianza cero (`veil-type`) que no aportan información.
2.  **Codificación**: Transformación de variables categóricas mediante *One-Hot Encoding* (`pd.get_dummies`).
3.  **Reducción de Dimensionalidad**: Uso de **PCA** (lineal) y **t-SNE** (no lineal) para proyectar y visualizar un espacio de más de 100 dimensiones en 2D.
4.  **Modelos de Clustering**: 
    * *K-Means*, *Clustering Jerárquico Aglomerativo*, *Gaussian Mixture Models (GMM)* y *DBSCAN*.
5.  **Evaluación**: 
    * Métricas internas: Método del codo, *Silhouette*, *Davies-Bouldin*, *Calinski-Harabasz*.
    * Métricas con etiqueta de referencia: *Adjusted Rand Index (ARI)* y *Normalized Mutual Information (NMI)*.
6.  **Detección de Anomalías**: Uso de **Isolation Forest** para localizar los ejemplares morfológicamente más atípicos.

---

## 💳 Parte 2: Segmentación de Clientes de Tarjeta de Crédito (Variables Numéricas)

### 📝 Descripción del Problema
A diferencia del primer taller, este caso representa un escenario de aprendizaje no supervisado puro. Consiste en analizar el comportamiento de aproximadamente **9,000 titulares de tarjetas de crédito** durante 6 meses utilizando 17 variables numéricas (saldos, compras, adelantos de efectivo, límite de crédito, pagos, etc.). El objetivo es **descubrir segmentos de clientes reales** para personalizar estrategias de marketing y productos financieros.

### 🛠️ Flujo de Trabajo y Técnicas
1.  **Preprocesamiento Crítico**:
    * Imputación de valores faltantes (por ejemplo, en `MINIMUM_PAYMENTS` y `CREDIT_LIMIT`).
    * **Escalado de Datos**: Al trabajar con variables numéricas en escalas masivamente distintas, se vuelve indispensable la estandarización/escalado.
2.  **Ingeniería de Características (KPIs)**: Creación de variables de negocio como el *ratio de uso del límite* (`BALANCE / CREDIT_LIMIT`) o la *compra media por transacción*.
3.  **Modelado**: Aplicación y tuning de *K-Means*, *GMM*, *Clustering Aglomerativo* y *DBSCAN*. 
4.  **Análisis de Perfiles**: Creación de un **Heatmap de perfiles por Cluster** para convertir las métricas matemáticas en segmentos interpretables por el equipo de negocio.
5.  **Detección de Outliers**: Implementación de **Isolation Forest** combinado con **PCA(2)** para marcar y mapear visualmente a los clientes con comportamientos financieros atípicos.

---

## 🚀 Tecnologías y Librerías Utilizadas

El proyecto está desarrollado completamente en **Python 3** empleando las siguientes librerías:
* **Manipulación de datos**: `pandas`, `numpy`
* **Visualización**: `matplotlib`, `seaborn`
* **Machine Learning**: `scikit-learn` (módulos de `cluster`, `decomposition`, `ensemble`, `mixture`, `manifold` y `metrics`)
* **Análisis Jerárquico**: `scipy.cluster.hierarchy` (Dendrogramas y Linkage)

---

## 📊 Principales Conclusiones de los Talleres
* **La importancia de la métrica**: Con datos categóricos (Setas), *DBSCAN* demuestra que la elección de la métrica de distancia es crítica.
* **Validación interna vs. externa**: En escenarios reales sin etiquetas (Tarjetas de Crédito), la validación se guía por coeficientes como *Silhouette* y, por encima de todo, por la **interpretabilidad comercial** de los clústeres.
* **Tratamiento de Datos**: El escalado e imputación transforman drásticamente el rendimiento en variables numéricas, un paso que no es crítico en variables puramente categóricas.
