# 1. Introducción

## 1.1. El dengue como problema de salud pública

El dengue es una **enfermedad febril aguda de etiología viral**,  transmitida por vectores del género _Aedes (A. aegypti y A. albopictus)_. Según la Organización mundial de la salud (OMS), esta patología representa una de las mayores cargas sanitarias en regiones tropicales y subtropicales, con un estimado de **390 millones de infecciones anuales** a nivel global (OMS, 2023). Su espectro clínico varía desde formas asintomáticas hasta cuadros graves que requieren intervención médica urgente. 

En Colombia, el dengue constituye un **reto epidemiológico prioritario** debido a su patrón endemo-epidémico y la amplia distribución del vector en el territorio nacional (73.3% según el INS, 2024). El  Instituto Nacional de Salud (INS) reporta ciclos epidémicos cada 3 a 5 años, asociados a factores climáticos y sociodemográficos. Desde 2013, el país ha fortalecido sus estrategias de vigilancia reforzada a través del Sistema Nacional de Vigilancia en Salud pública (SIVIGILA), que exige la notificación obligatoria de casos sospechosos y confirmados.

### 1.1.1. Clasificación de casos
Los registros epidemiológicos distinguen dos categorías principales:

| Tipo de caso | Criterios de clasificación |
| ---- |----|
| No confirmado |Pacientes con cuadro febril agudo (2 a 7 días) y signos de alarma compatibles con dengue, sin confirmación diagnóstica.|
| Confirmado | Diagnóstico corroborado mediante pruebas de laboratorio (PCR, ELISA) o nexo epidemiológico. | 

La detección temprana de casos resulta fundamental para:
* Reducir la mortalidad mediante el tratamiento oportuno.
* Contener brotes a través del control vectorial.
* Optimizar recursos en sistemas de salud, especialmente en contextos con capacidad limitada.


## 1.2. Objetivo del estudio

El objetivo principal de este estudio es **desarrollar un modelo de aprendizaje automático para la clasificación precisa de casos confirmados de dengue**, utilizando variables clínicas, demográficas y epidemiológicas extraídas de SIVIGILA. Dada la naturaleza de alto riesgo de los falsos negativos en este contexto, el modelo busca **maximizar la sensibilidad (recall)**, es decir, la capacidad de identificar el mayor número posible de casos positivos, sin comprometer la estabilidad predictiva.

## 1.3. Hipótesis técnica
> _Un enfoque basado en modelos ensamblados (stacking) puede superar el rendimiento de clasificadores individuales al combinar sus fortalezas para detectar patrones complejos en datos heterogéneos y desbalanceados._

## 1.4. Enfoque metodológico
Para validar esta hipótesis, se implementó un flujo de trabajo estructurado en dos etapas: 

1. Evaluación de modelos base y optimización:

Se evaluaron 10 algoritmos clásicos y de ensamble, agrupados según su naturaleza:

|Categoría| Modelos Evaluados |
| ---- | ----|
| Modelos lineales| Regresión logística con penalización Ridge y Lasso |
| Métodos basados en distancias | K-Nearest Neighbors |
| Algoritmos probabilísticos | Naive Bayes |
| Árboles de decisión | Decision Tree |
| Métodos de ensamble | Random Forest y XGBoost |
| Métodos de margen | Support Vector Machine, Linear Support Vector Regression | 

**Proceso de optimización**
* Búsqueda de hiperparámetros mediante validación cruzada.
* Métricas prioritarias: Recall (sensibilidad), F1-Score y ROC-AUC
* Balanceo de clases mediante el ajuste de pesos.
* En los casos necesarios, se aplicaron estandarización y reducción de dimensionalidad.


2. Selección y combinación óptima:

Tras la evaluación inicial, se identificaron los dos mejores modelo base según el mayor recall, estabilidad en las curvas ROC, y mejor interpretabilidad. Luego se exploraron diferentes enfoques de ensamblado, incluyendo:
* Voting Classifier,
* Stacking simple
* Stacking con passthrough


## 1.5. Propuesta del modelo
Como resultado de este análisis comparativo, se propone una solución final denominada **SD-GBClassifier** _(Stacked Dengue - Gradient Boosting Classifier)_. Este modelo integra predicciones provenientes de Random Forest y XGBoost dentro de una arquitectura de stacking, con un meta-modelo Gradient Boosting, optimizado para la detección de casos confirmados de dengue en Colombia.

**Proyecto de clase Machine Learning**\
**Universidad del Norte**\
**2025-10**