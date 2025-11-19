# Proyecto Final de Machine Learning - Database II
## Análisis de Clasificación del Dataset Yeast

Este proyecto implementa un análisis completo de **clasificación multiclase** sobre el dataset Yeast (Protein Localization Sites), aplicando técnicas avanzadas de manejo de desbalanceo, selección de características y optimización de modelos.

## 📁 Estructura del Proyecto

```
ML_ProyectoFinalDB2/
├── DATABASE/
│   ├── yeast.data          # Dataset principal
│   └── yeast.names         # Descripción del dataset
├── yeast_ml_analysis.ipynb # Notebook principal con todo el análisis
├── requirements.txt        # Dependencias del proyecto
└── README.md              # Este archivo
```

## 📊 Dataset

**Yeast Protein Localization Sites**
- **Instancias**: 1,484
- **Características**: 8 numéricas + 1 nombre
- **Clases**: 10 (sitios de localización de proteínas)
- **Fuente**: UCI Machine Learning Repository

### Características del Dataset:
1. `mcg`: McGeoch's method for signal sequence recognition
2. `gvh`: von Heijne's method for signal sequence recognition  
3. `alm`: Score of ALOM membrane spanning region prediction
4. `mit`: Discriminant analysis of mitochondrial proteins
5. `erl`: Presence of "HDEL" substring
6. `pox`: Peroxisomal targeting signal
7. `vac`: Discriminant analysis of vacuolar proteins
8. `nuc`: Discriminant analysis of nuclear proteins

### Clases:
- CYT (cytosolic/cytoskeletal): 463
- NUC (nuclear): 429
- MIT (mitochondrial): 244
- ME3 (membrane protein, no signal): 163
- ME2 (membrane protein, uncleaved): 51
- ME1 (membrane protein, cleaved): 44
- EXC (extracellular): 37
- VAC (vacuolar): 30
- POX (peroxisomal): 20
- ERL (endoplasmic reticulum): 5

## 🛠️ Métodos Implementados

### 1. Carga de Datos
- **Fuente Oficial**: UCI ML Repository mediante `ucimlrepo` (ID: 110)
- **Sin valores faltantes**: Dataset confirmado completo
- **Análisis de desbalanceo**: Identificación de clases minoritarias

### 2. Evaluación de Escalamiento
- Comparación de rendimiento con/sin escalamiento
- **StandardScaler**: Para modelos sensibles a la escala

### 3. Detección de Outliers (PyOD) con Protección de Clases Minoritarias
- **KNN**: K-Nearest Neighbors para detección de anomalías
- **Isolation Forest**: Aislamiento aleatorio de observaciones
- **LOF**: Local Outlier Factor
- **CRÍTICO**: Protección de outliers en clases minoritarias (< 5%)

### 4. Selección de Características
- **RFE (Recursive Feature Elimination)**: Con RandomForestClassifier
- **Lasso (L1)**: Logistic Regression con regularización L1
- **Stepwise (Forward Selection)**: Búsqueda secuencial hacia adelante

### 5. Manejo de Desbalanceo
- **SMOTE**: Synthetic Minority Over-sampling Technique
- **Random Oversampling**: Sobremuestreo aleatorio
- Mejora de Balanced Accuracy

### 6. Modelos de Clasificación con Regularización
- **Ridge (L2)**: Logistic Regression con penalización L2
- **Lasso (L1)**: Logistic Regression con penalización L1
- **Elastic Net**: Logistic Regression con L1 + L2
- **GridSearchCV**: Optimización de hiperparámetros

### 7. Modelos Ensemble y Avanzados
- **Árbol de Decisión**: Clasificador optimizado
- **Random Forest**: Ensemble de árboles
- **Gradient Boosting**: Boosting secuencial
- **SVM**: Support Vector Machine con kernel RBF

### 8. Métricas de Clasificación
- **Accuracy**: Tasa de acierto global
- **Balanced Accuracy**: Ajustada por desbalanceo
- **F1-Score (weighted)**: Balance precision/recall ponderado
- **Classification Report**: Métricas por clase

## 📦 Instalación

### Requisitos Previos
- Python 3.8 o superior
- pip

### Pasos de Instalación

1. Clonar o descargar el repositorio

2. Instalar las dependencias:
```bash
pip install -r requirements.txt
```

### Dependencias Principales
```
pandas==2.0.3
numpy==1.24.3
scikit-learn==1.3.0
matplotlib==3.7.2
seaborn==0.12.2
pyod==1.1.0
mlxtend==0.22.0
jupyter==1.0.0
imbalanced-learn==0.11.0
ucimlrepo
```

## 🚀 Uso

### Ejecutar el Análisis Completo

1. Abrir Jupyter Notebook:
```bash
jupyter notebook yeast_ml_analysis.ipynb
```

2. Ejecutar todas las celdas secuencialmente (Cell → Run All)

### Estructura del Notebook

El notebook está organizado en las siguientes secciones:

1. **Importar Librerías**: Carga de todas las dependencias necesarias
2. **Carga y Exploración de Datos**: Desde UCI ML Repository oficial
3. **Preparación de Datos**: Análisis de desbalanceo y codificación
4. **Evaluación de Escalamiento**: Comparación con/sin scaling
5. **Detección de Outliers**: PyOD con protección de clases minoritarias
6. **Selección de Características**: RFE, Lasso, Stepwise
7. **Manejo de Desbalanceo**: SMOTE y Random Oversampling
8. **Modelos de Clasificación**: Regularización y optimización
9. **Árboles de Decisión y Ensemble**: RF, GB, SVM
10. **Comparativa Final**: Evaluación con métricas de clasificación
11. **Conclusiones**: Resumen y recomendaciones

## 📈 Resultados Esperados

El notebook genera:

- **Visualizaciones**:
  - Distribución de clases y desbalanceo
  - Matriz de correlación
  - Análisis de outliers por clase
  - Comparación de métodos de selección de características
  - Árboles de decisión visualizados
  - Matriz de confusión
  - Gráficas comparativas de modelos

- **Métricas de Clasificación**:
  - **Accuracy**: Tasa de acierto
  - **Balanced Accuracy**: Ajustada por desbalanceo
  - **F1-Score (weighted)**: Balance precision/recall
  - **Classification Report**: Precision, Recall, F1 por clase
  - Importancia de características

- **Comparativa Final**:
  - Tabla resumen con todos los modelos
  - Recomendaciones sobre qué modelo usar

## 📝 Análisis Realizados

### Preprocesamiento
- Introducción artificial de valores faltantes (5%)
- Comparación de técnicas de imputación
- Detección y remoción de outliers por consenso

### Feature Engineering
- Selección mediante 3 métodos diferentes
- Identificación de características más relevantes
- Análisis de importancia

### Modelado
- Optimización de hiperparámetros con GridSearch
- Validación cruzada de 5 folds
- Comparación exhaustiva de modelos

## 🎯 Conclusiones Principales

1. **Imputación**: KNNImputer demostró ser más robusto que Forward/Backward Fill
2. **Outliers**: El consenso de múltiples métodos mejora la calidad del dataset
3. **Selección de Features**: Los 3 métodos identificaron características comunes relevantes
4. **Regularización**: Elastic Net ofrece un buen balance entre Ridge y Lasso
5. **Árboles**: La optimización de hiperparámetros mejora significativamente el desempeño

## 👥 Autores

Proyecto Final - Base de Datos II  
Universidad de Lima - Ciclo VIII  
Machine Learning

## 📄 Licencia

Este proyecto es parte de un trabajo académico.

## 🔗 Referencias

- Dataset: [UCI Machine Learning Repository - Yeast](https://archive.ics.uci.edu/ml/datasets/Yeast)
- Nakai, K., & Kanehisa, M. (1991). Expert system for predicting protein localization sites in gram-negative bacteria
- Horton, P., & Nakai, K. (1996). A probabilistic classification system for predicting the cellular localization sites of proteins

## 📧 Contacto

Para preguntas o sugerencias sobre este proyecto, contactar al equipo de desarrollo.

---

**Nota**: Este es un proyecto académico que demuestra la aplicación práctica de técnicas de Machine Learning vistas en el curso.
