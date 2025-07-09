
# Pulsar Detection with MLP (HTRU2 Dataset)

Proyecto final del curso **Big Data en Astrofísica**. Se implementa una red neuronal tipo *Multilayer Perceptron (MLP)* para la clasificación automática de señales como **púlsares reales** o **interferencias**, utilizando el conjunto de datos **HTRU2**.

---

##  Estructura del Repositorio

```
 pulsar-mlp
├── PULSAR1.ipynb           # Notebook principal (análisis + entrenamiento + evaluación)
├── /models                 # Scripts de modelos alternativos (SVM, GMM, LogReg)
├── /utils                  # Scripts de preprocesamiento, normalización, PCA
├── /data                   # Dataset original y/o procesado
├── /figures                # Gráficos generados (PCA, ROC, curvas de pérdida, etc.)
└── README.md               # Este archivo
```

---

##  Objetivos del proyecto

- Explorar y visualizar el dataset HTRU2.
- Aplicar normalización y PCA para análisis exploratorio.
- Entrenar un MLP usando PyTorch para clasificación binaria.
- Ajustar umbral de decisión para mejorar F1-score.
- Calibrar scores y evaluar con datos simulados.

---

##  Dataset HTRU2

- 17.898 ejemplos
- 8 características estadísticas por muestra:
  - Media, desviación, skewness y curtosis del perfil integrado
  - Media, desviación, skewness y curtosis de la curva DM-SNR
- Etiqueta binaria: `1` = púlsar, `0` = interferencia
- Fuertemente desbalanceado (~9% púlsares reales)

Fuente: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/HTRU2)

---

## Arquitectura del MLP

```text
Input (8)
→ Linear(8, 16) → ReLU
→ Linear(16, 8) → ReLU
→ Linear(8, 1) → Sigmoid
```

- Optimización con Adam
- Pérdida: Binary Cross-Entropy
- 50 épocas
- Umbral ajustado para maximizar F1-score

---

## Resultados

| Métrica            | Valor     |
|--------------------|-----------|
| Accuracy           | 91.4%     |
| Precision          | 0.5588    |
| Recall             | 0.5460    |
| F1-score           | **0.5523** |
| AUC ROC            | 0.85      |

---

## Validación Adicional

- Simulación de datos gaussianos por clase
- Evaluación con datos nuevos
- Verificación de generalización

---

## Herramientas utilizadas

- `PyTorch` – entrenamiento del modelo
- `scikit-learn` – métricas, PCA y validación
- `matplotlib` / `seaborn` – visualizaciones
- `numpy`, `pandas` – manipulación de datos

---

## Informe final

El notebook `PULSAR1.ipynb` contiene:

- Análisis exploratorio
- Entrenamiento y visualización de curvas
- Métricas y gráficas de evaluación
- Comparación con datos simulados
- Conclusiones y sugerencias futuras

---

## Autores

- **Nicolás Campos**
- **Ángel Paisano**
- **Irma Pizarro**
- **Marcelo Andrade**

Estudiantes de Astrofísica con mención en Ciencia de Datos, Departamento de Física, Universidad de Santiago de Chile  
Julio 2025

---

## Ideas futuras

- Aplicar penalización por clase (weighted loss)
- Probar arquitecturas más profundas o RNN
- Automatizar búsqueda de hiperparámetros
- Implementar pipeline en entorno real de observatorio
