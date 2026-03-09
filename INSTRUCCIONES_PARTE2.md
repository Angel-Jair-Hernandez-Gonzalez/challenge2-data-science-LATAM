# Parte 2: Modelado Predictivo de Evasión de Clientes

## 🎯 Misión

Tu nueva misión es desarrollar modelos predictivos capaces de prever qué clientes tienen mayor probabilidad de cancelar sus servicios.

La empresa quiere anticiparse al problema de la cancelación, y te corresponde a ti construir un pipeline robusto para esta etapa inicial de modelado.

## 🧠 Objetivos del Desafío

- Preparar los datos para el modelado (tratamiento, codificación, normalización)
- Realizar análisis de correlación y selección de variables
- Entrenar dos o más modelos de clasificación
- Evaluar el rendimiento de los modelos con métricas
- Interpretar los resultados, incluyendo la importancia de las variables
- Crear una conclusión estratégica señalando los principales factores que influyen en la cancelación

## 🧰 Lo que vas a practicar

- ✅ Preprocesamiento de datos para Machine Learning
- ✅ Construcción y evaluación de modelos predictivos
- ✅ Interpretación de resultados y entrega de insights
- ✅ Comunicación técnica con enfoque estratégico

---

## 📋 Etapas de Implementación

### 1. Extracción del Archivo Tratado

Carga el archivo CSV que contiene los datos tratados anteriormente.

**📂 Atención:** Utiliza el mismo archivo que limpiaste y organizaste en la Parte 1 del desafío Telecom X. Debe contener solo las columnas relevantes, ya con los datos corregidos y estandarizados.

- Archivo: `data/processed/telecom_cleaned.csv`

### 2. Eliminación de Columnas Irrelevantes

Elimina columnas que no aportan valor al análisis o a los modelos predictivos, como identificadores únicos (por ejemplo, el ID del cliente). Estas columnas no ayudan en la predicción de la cancelación y pueden incluso perjudicar el desempeño de los modelos.

### 3. Encoding

Transforma las variables categóricas a formato numérico para hacerlas compatibles con los algoritmos de machine learning. Utiliza un método de codificación adecuado, como **one-hot encoding**.

**🔎 Sugerencia:**
Consulta los siguientes temas para entender mejor cuándo usar `get_dummies()` o `OneHotEncoder`:
- Variables con pocas categorías → `pd.get_dummies()`
- Mayor flexibilidad → `sklearn.preprocessing.OneHotEncoder`

### 4. Verificación de la Proporción de Cancelación (Churn)

Calcula la proporción de clientes que cancelaron en relación con los que permanecieron activos. Evalúa si existe un desbalance entre las clases, ya que esto puede impactar en los modelos predictivos y en el análisis de los resultados.

```python
df['Churn'].value_counts()
df['Churn'].value_counts(normalize=True)
```

### 5. Balanceo de Clases (Opcional)

Si deseas profundizar en el análisis, aplica técnicas de balanceo como:
- **Undersampling:** Reducir la clase mayoritaria
- **Oversampling:** Aumentar la clase minoritaria
- **SMOTE:** Generar ejemplos sintéticos de la clase minoritaria

En situaciones de fuerte desbalanceo, herramientas como SMOTE pueden ser útiles.

### 6. Normalización o Estandarización (si es necesario)

Evalúa la necesidad de normalizar o estandarizar los datos, según los modelos que se aplicarán:

- **Modelos sensibles a la escala:** KNN, SVM, Regresión Logística, Redes Neuronales
  - Utiliza `StandardScaler` o `MinMaxScaler`
  
- **Modelos insensibles a la escala:** Decision Tree, Random Forest, XGBoost
  - No requieren normalización

---

## 🔍 Siguiente Etapa: Análisis de Correlación

### Análisis de Correlación

Visualiza la matriz de correlación para identificar relaciones entre las variables numéricas. Presta especial atención a las variables que muestran una mayor correlación con la cancelación, ya que estas pueden ser fuertes candidatas para el modelo predictivo.

### Análisis Dirigido

Investiga cómo variables específicas se relacionan con la cancelación, tales como:

- **Tiempo de contrato × Cancelación**
- **Gasto total × Cancelación**
- Otras variables relevantes identificadas en Parte 1

Utiliza gráficos como:
- **Boxplots** para comparar distribuciones
- **Scatter plots** para visualizar patrones
- **Heatmaps** para correlación

---

## 🤖 Modelos Predictivos a Entrenar

Se requiere entrenar **mínimo dos modelos** de clasificación. Opciones sugeridas:

1. **Regresión Logística** - Baseline simple y interpretable
2. **Random Forest** - Ensemble robusto con importancia de variables
3. **XGBoost** - Gradient boosting de alto rendimiento
4. **SVM** - Support Vector Machine (requiere normalización)
5. **KNN** - K-Nearest Neighbors (requiere normalización)

### Evaluación de Modelos

Utiliza las siguientes métricas:
- **Accuracy:** Proporción de predicciones correctas
- **Precision:** Proporción de predicciones positivas correctas
- **Recall:** Proporción de casos positivos identificados
- **F1-Score:** Media armónica de Precision y Recall
- **ROC-AUC:** Área bajo la curva ROC
- **Matriz de Confusión:** Análisis detallado de predicciones

---

## 📊 Entregables

1. Notebook completo con:
   - Preprocesamiento de datos
   - Análisis exploratorio y de correlación
   - Entrenamiento de modelos
   - Evaluación comparativa
   - Interpretación de resultados

2. Conclusiones estratégicas:
   - Principales factores que influyen en la cancelación
   - Recomendaciones basadas en el modelado
   - Limitaciones y posibles mejoras

---

**Siguiente paso:** Abre el notebook `notebooks/02_Predictive_Modeling.ipynb` y comienza a implementar estas etapas.
