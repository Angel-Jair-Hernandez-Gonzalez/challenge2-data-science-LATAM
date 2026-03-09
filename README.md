# Analysis of Customer Churn in Telecom X

**Análisis de Evasión de Clientes en Telecom X**

## Descripción del Proyecto

Este proyecto realiza un análisis exhaustivo del problema de evasión de clientes (Churn) en Telecom X en dos fases:

**Parte 1 (Análisis Exploratorio):** Desanidalización de datos JSON, limpieza, transformación y análisis descriptivo detallado de variables categóricas y numéricas.

**Parte 2 (Modelado Predictivo):** Construcción de modelos de Machine Learning para predecir cancelaciones, análisis de correlación, evaluación de rendimiento e identificación de factores clave que influyen en la evasión de clientes.

## Contexto y Problemática

Telecom X enfrenta una **tasa de evasión del 26.58%**, lo que significa que aproximadamente 1 de cada 4 clientes cancela sus servicios. Este proyecto busca:

- Comprender los patrones de comportamiento de clientes evadidos
- Identificar variables categóricas y numéricas asociadas a la evasión
- Proporcionar recomendaciones estratégicas basadas en datos

## Estructura del Proyecto

```
challenge2-data-science-LATAM/
├── README.md                               # Este archivo (documentación del proyecto)
├── INSTRUCCIONES_PARTE2.md                # Instrucciones detalladas de Parte 2
├── requirements.txt                        # Dependencias Python
├── data/
│   ├── TelecomX_Data.json                 # Dataset original con estructura JSON
│   ├── TelecomX_diccionario.md            # Diccionario de datos
│   └── processed/
│       └── telecom_cleaned.csv            # Datos limpios exportados de Parte 1 (7,032 registros)
└── notebooks/
    ├── 01_TelecomX_LATAM_EDA.ipynb        # Análisis Exploratorio (desanidalización, limpieza)
    └── 02_Predictive_Modeling.ipynb       # Modelado Predictivo (classification, evaluation)
```

## Requisitos y Dependencias

El proyecto utiliza las siguientes librerías Python:

- **pandas** (2.2.3) - Manipulación y análisis de datos
- **numpy** (2.2.5) - Cálculos numéricos
- **matplotlib** (3.10.1) - Visualización de datos
- **seaborn** (0.13.2) - Gráficos estadísticos avanzados
- **python** (3.13.3) - Intérprete Python

## Instalación

### Opción 1: Con Anaconda/Conda

```bash
# Crear entorno virtual
conda create -n telecom-churn python=3.13

# Activar entorno
conda activate telecom-churn

# Instalar dependencias
conda install pandas numpy matplotlib seaborn jupyter
```

### Opción 2: Con pip

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno (Windows)
venv\Scripts\activate

# Activar entorno (macOS/Linux)
source venv/bin/activate

# Instalar dependencias
pip install pandas numpy matplotlib seaborn jupyter
```

## Cómo Ejecutar el Proyecto

### 1. Clonar el repositorio

```bash
git clone https://github.com/Angel-Jair-Hernandez-Gonzalez/challenge2-data-science-LATAM.git
cd challenge2-data-science-LATAM
```

### 2. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 3. Ejecutar los Notebooks en orden

**Parte 1: Análisis Exploratorio**
```bash
cd notebooks
jupyter notebook 01_TelecomX_LATAM_EDA.ipynb
```

**Parte 2: Modelado Predictivo**
```bash
jupyter notebook 02_Predictive_Modeling.ipynb
```

### 4. Ejecución de Celdas

- Ejecutar todas las celdas: `Cell → Run All` (o Ctrl+Shift+Enter)
- O ejecutar celda por celda: `Shift + Enter`

**Nota:** Parte 2 depende de los datos limpios generados en Parte 1 (`data/processed/telecom_cleaned.csv`)

## Contenido del Análisis

### Parte 1: Análisis Exploratorio (01_TelecomX_LATAM_EDA.ipynb)

1. **Extracción y Carga de Datos**
   - Carga desde JSON con estructura anidada
   - Dataset inicial: 7,267 registros

2. **Transformación y Limpieza**
   - Desanidación de 6 columnas originales → 21 variables
   - Eliminación de 224 registros inválidos
   - Dataset limpio: 7,032 registros

3. **Análisis Descriptivo y Visualizaciones**
   - Estadísticas descriptivas, correlación
   - Distribución de variables numéricas
   - Análisis de 6 variables categóricas con tasas de evasión

4. **Resultados**
   - Identificación de 5 principales factores de churn
   - Recomendaciones estratégicas de retención

### Parte 2: Modelado Predictivo (02_Predictive_Modeling.ipynb)

1. **Preparación de Datos**
   - Codificación de variables categóricas (one-hot encoding)
   - Normalización/estandarización de features
   - Split train/test (80/20 con stratificación)

2. **Análisis de Correlación**
   - Matriz de correlación completa
   - Top 10 variables correlacionadas con churn
   - Análisis dirigido de variables clave

3. **Entrenamiento de Modelos**
   - Logistic Regression (baseline)
   - Random Forest (interpretabilidad)
   - XGBoost (rendimiento)

4. **Evaluación Comparativa**
   - Accuracy, Precision, Recall, F1-Score
   - ROC-AUC curve analysis
   - Confusion Matrix por modelo

5. **Interpretación de Resultados**
   - Feature Importance de cada modelo
   - Factores más influyentes en cancelación
   - Conclusiones estratégicas y recomendaciones

## Resultados Principales

### Parte 1: Insights del EDA

1. **Antigüedad del Cliente**: Clientes con <18 meses tienen 2.4x más probabilidad de evasión
2. **Tipo de Contrato**: Mes a mes: 42.71% evasión vs 10% para contratos de 2 años
3. **Tipo de Internet**: Fibra óptica: 41.89% evasión (posibles problemas de calidad)
4. **Método de Pago**: Transferencia electrónica: 45.29% evasión
5. **Demographic Factors**: Seniores (65+) tienen 41.68% de evasión

### Parte 2: Rendimiento Predictivo

**Modelos Entrenados:**
- Regresion Logística (baseline escalable)
- Random Forest (interpretar importancia de variables)
- XGBoost (máximo rendimiento predictivo)

**Métricas de Evaluación:**
- Accuracy, Precision, Recall, F1-Score
- ROC-AUC para comparación de modelos
- Análisis de confusion matrix por modelo

**Variables Más Predictivas:**
Identificadas según importancia relativa en cada modelo para soportar decisiones de negocio.

## Conclusiones y Recomendaciones

### Estrategia de Retención (de Parte 1 EDA)

1. **Mejorar Contratos a Corto Plazo**
   - Implementar programas de retención para nuevos clientes
   - Ofrecer incentivos para pasar a contratos más largos

2. **Evaluación de Servicio Fibra Óptica**
   - Investigar causas de insatisfacción
   - Mejorar calidad de servicio
   - Crear planes de fidelización específicos

3. **Enfoque en Nuevos Clientes**
   - Mejorar programa de onboarding
   - Asignar gerentes de cuenta en primeros 6 meses
   - Seguimiento proactivo de satisfacción

### Aplicación del Modelado Predictivo (Parte 2)

1. **Identificación Proactiva de Riesgo**
   - Usar modelos para scoring de riesgo de churn en tiempo real
   - Priorizar clientes de alto riesgo para intervención

2. **Intervención Personalizada**
   - Diseñar estrategias de retención basadas en factores predictivos
   - A/B testing de tácticas de retención

3. **Monitoreo Continuo**
   - Re-entrenar modelos regularmente con datos nuevos
   - Medir ROI de acciones de retención
   - Optimizar thresholds según disponibilidad de recursos

## Tecnologías Utilizadas

- **Python 3.13**: Lenguaje de programación
- **Jupyter Notebook**: Entorno interactivo de análisis
- **Pandas**: Manipulación de datos
- **Matplotlib & Seaborn**: Visualización de datos
- **Git**: Control de versiones

## Proyecto de Dos Fases

Este repositorio contiene la **Parte 2: Modelado Predictivo** de un proyecto completo de análisis de evasión de clientes.

- **Parte 1:** Análisis Exploratorio de Datos (EDA)
- **Parte 2 (Este Repositorio):** Modelado Predictivo de Evasión de Clientes

Los datos limpios y procesados en Parte 1 se cargan desde `data/processed/telecom_cleaned.csv` para entrenar modelos de Machine Learning que predicen cancelaciones de clientes.

👉 **[Parte 1: Análisis Exploratorio →](https://github.com/Angel-Jair-Hernandez-Gonzalez/challenge1-data-science-latam-)**

---

## Autor

**Angel Jair Hernández González**

- GitHub: [Angel-Jair-Hernandez-Gonzalez](https://github.com/Angel-Jair-Hernandez-Gonzalez)
- Repositorio Parte 1 (EDA): [challenge1-data-science-latam-](https://github.com/Angel-Jair-Hernandez-Gonzalez/challenge1-data-science-latam-)
- Repositorio Parte 2 (Modelado): [challenge2-data-science-LATAM](https://github.com/Angel-Jair-Hernandez-Gonzalez/challenge2-data-science-LATAM)

## Licencia

Este proyecto es de código abierto y disponible bajo la licencia MIT. 