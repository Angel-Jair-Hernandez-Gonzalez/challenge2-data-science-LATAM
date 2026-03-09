# Challenge 2 – Data Science LATAM: Análisis de Evasión de Clientes (Telecom X)

## Tabla de Contenidos

1. [Contexto del Challenge](#contexto-del-challenge)
2. [Objetivos](#objetivos)
3. [Prerrequisitos](#prerrequisitos)
4. [Estructura del Proyecto](#estructura-del-proyecto)
5. [Instrucciones Paso a Paso](#instrucciones-paso-a-paso)
   - [Paso 1 – Extracción de Datos](#paso-1--extracción-de-datos)
   - [Paso 2 – Transformación de Datos](#paso-2--transformación-de-datos)
   - [Paso 3 – Comprobación de Incoherencias](#paso-3--comprobación-de-incoherencias)
   - [Paso 4 – Manejo de Inconsistencias](#paso-4--manejo-de-inconsistencias)
   - [Paso 5 – Columna de Cuentas Diarias (Opcional)](#paso-5--columna-de-cuentas-diarias-opcional)
   - [Paso 6 – Estandarización y Transformación (Opcional)](#paso-6--estandarización-y-transformación-opcional)
   - [Paso 7 – Análisis Exploratorio de Datos (EDA)](#paso-7--análisis-exploratorio-de-datos-eda)
   - [Paso 8 – Visualizaciones](#paso-8--visualizaciones)
   - [Paso 9 – Informe de Insights](#paso-9--informe-de-insights)
6. [Diccionario de Datos](#diccionario-de-datos)
7. [Entregables Esperados](#entregables-esperados)
8. [Criterios de Evaluación](#criterios-de-evaluación)

---

## Contexto del Challenge

Has sido contratado como asistente de análisis de datos en **Telecom X** y formarás parte del proyecto **"Churn de Clientes"**. La empresa enfrenta una alta tasa de cancelaciones y necesita comprender los factores que llevan a la pérdida de clientes.

Tu desafío es recopilar, procesar y analizar los datos utilizando **Python** y sus principales bibliotecas para extraer información valiosa. A partir de tu análisis, el equipo de Data Science podrá avanzar en modelos predictivos y desarrollar estrategias para reducir la evasión.

---

## Objetivos

Al finalizar este challenge habrás demostrado tu capacidad para:

- ✅ Importar y manipular datos desde una API de manera eficiente.
- ✅ Aplicar los conceptos de **ETL** (Extracción, Transformación y Carga) en la preparación de los datos.
- ✅ Crear **visualizaciones estratégicas** para identificar patrones y tendencias.
- ✅ Realizar un **Análisis Exploratorio de Datos (EDA)** y generar un informe con insights relevantes.

---

## Prerrequisitos

Antes de comenzar, asegúrate de contar con lo siguiente:

### Software y herramientas

| Herramienta | Versión recomendada |
|-------------|---------------------|
| Python | 3.8 o superior |
| Jupyter Notebook / JupyterLab | Última versión estable |
| Git | Cualquier versión reciente |

### Bibliotecas de Python

Instala las dependencias necesarias ejecutando el siguiente comando en tu terminal:

```bash
pip install pandas numpy matplotlib seaborn requests
```

> 💡 **Tip:** Se recomienda usar un entorno virtual para mantener las dependencias aisladas:
> ```bash
> python -m venv venv
> source venv/bin/activate      # Linux / macOS
> venv\Scripts\activate         # Windows
> pip install pandas numpy matplotlib seaborn requests
> ```

---

## Estructura del Proyecto

```
challenge2-data-science-LATAM/
├── data/
│   ├── TelecomX_Data.json          # Datos de clientes en formato JSON
│   └── TelecomX_diccionario.md     # Diccionario de variables del dataset
├── notebooks/
│   └── TelecomX_LATAM.ipynb        # Notebook principal del análisis
└── README.md                        # Este archivo
```

---

## Instrucciones Paso a Paso

### Paso 1 – Extracción de Datos

Los datos de Telecom X están disponibles en formato **JSON** y contienen información esencial sobre los clientes: datos demográficos, tipo de servicio contratado y estado de evasión.

**¿Qué debes hacer?**

1. Abre el notebook `notebooks/TelecomX_LATAM.ipynb`.
2. Carga los datos directamente desde la API usando la biblioteca `requests`:

```python
import requests
import pandas as pd

url = "https://raw.githubusercontent.com/ingridcristh/challenge2-data-science-LATAM/main/TelecomX_Data.json"
response = requests.get(url)
data = response.json()
df = pd.DataFrame(data)
```

3. Como alternativa, puedes cargar el archivo local disponible en `data/TelecomX_Data.json`:

```python
import pandas as pd
import json

with open("../data/TelecomX_Data.json", "r") as f:
    data = json.load(f)
df = pd.DataFrame(data)
```

4. Verifica que los datos se cargaron correctamente mostrando las primeras filas: `df.head()`.

---

### Paso 2 – Transformación de Datos

Es fundamental comprender la estructura del dataset y el significado de sus columnas. Esta etapa te ayudará a identificar qué variables son más relevantes para el análisis de evasión.

**¿Qué debes hacer?**

1. Explora la estructura del DataFrame:

```python
print(df.shape)       # Dimensiones del dataset
print(df.dtypes)      # Tipos de datos por columna
df.info()             # Resumen general
df.describe()         # Estadísticas descriptivas
```

2. Consulta el [Diccionario de Datos](#diccionario-de-datos) disponible en `data/TelecomX_diccionario.md` para comprender el significado de cada columna.
3. Identifica las columnas más relevantes para el análisis de evasión (columna `Churn`).
4. Normaliza columnas anidadas si es necesario (el dataset JSON puede tener columnas como `customer`, `phone`, `internet`, `account` con sub-campos).

---

### Paso 3 – Comprobación de Incoherencias

Verifica si hay problemas en los datos que puedan afectar el análisis. Presta atención a:

- **Valores ausentes (NaN / nulos)**
- **Registros duplicados**
- **Errores de formato** (por ejemplo, números almacenados como texto)
- **Inconsistencias en categorías** (por ejemplo, `"Yes"` y `"yes"` como valores distintos)

```python
# Valores nulos por columna
print(df.isnull().sum())

# Porcentaje de nulos
print(df.isnull().mean() * 100)

# Registros duplicados
print(df.duplicated().sum())

# Valores únicos en columnas categóricas
for col in df.select_dtypes(include="object").columns:
    print(f"{col}: {df[col].unique()}")
```

---

### Paso 4 – Manejo de Inconsistencias

Ahora que has identificado las inconsistencias, aplica las correcciones necesarias para que los datos estén completos y coherentes.

**Acciones sugeridas:**

- Eliminar o imputar valores nulos según corresponda.
- Eliminar registros duplicados.
- Convertir columnas numéricas que están como texto (por ejemplo, `TotalCharges`).
- Normalizar valores categóricos a un formato consistente.

```python
# Ejemplo: eliminar duplicados
df = df.drop_duplicates()

# Ejemplo: convertir TotalCharges a numérico
df["Charges.Total"] = pd.to_numeric(df["Charges.Total"], errors="coerce")

# Ejemplo: rellenar nulos en columnas numéricas con la mediana
df["Charges.Total"].fillna(df["Charges.Total"].median(), inplace=True)
```

---

### Paso 5 – Columna de Cuentas Diarias (Opcional)

Crea la columna **`Cuentas_Diarias`** dividiendo la facturación mensual entre 30, para obtener el costo diario estimado por cliente.

```python
df["Cuentas_Diarias"] = df["Charges.Monthly"] / 30
```

Esta nueva columna proporciona una visión más detallada del comportamiento financiero de los clientes a lo largo del tiempo.

---

### Paso 6 – Estandarización y Transformación (Opcional)

Esta etapa mejora la consistencia y legibilidad del dataset, especialmente al compartir resultados con stakeholders no técnicos.

**Acciones sugeridas:**

1. **Convertir variables binarias** de texto a números:

```python
binary_cols = ["Churn", "Partner", "Dependents", "PhoneService", "PaperlessBilling"]
for col in binary_cols:
    df[col] = df[col].map({"Yes": 1, "No": 0})
```

2. **Renombrar columnas** al español para mayor claridad:

```python
df.rename(columns={
    "customerID": "ID_Cliente",
    "gender": "Genero",
    "SeniorCitizen": "Adulto_Mayor",
    "tenure": "Meses_Contrato",
    "Churn": "Evasion"
}, inplace=True)
```

---

### Paso 7 – Análisis Exploratorio de Datos (EDA)

Realiza un análisis profundo del dataset para identificar patrones y relaciones entre variables.

**Análisis sugeridos:**

1. **Tasa de evasión general:**

```python
print(df["Churn"].value_counts(normalize=True) * 100)
```

2. **Evasión por variables categóricas** (género, tipo de contrato, método de pago, etc.):

```python
print(df.groupby("Contract")["Churn"].mean() * 100)
```

3. **Estadísticas de variables numéricas** por grupo de evasión:

```python
print(df.groupby("Churn")[["tenure", "Charges.Monthly", "Charges.Total"]].mean())
```

4. **Matriz de correlación** entre variables numéricas:

```python
import seaborn as sns
import matplotlib.pyplot as plt

corr = df.select_dtypes(include="number").corr()
sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("Matriz de Correlación")
plt.show()
```

---

### Paso 8 – Visualizaciones

Crea visualizaciones estratégicas para comunicar los hallazgos del análisis.

**Visualizaciones sugeridas:**

1. **Distribución de la evasión:**

```python
df["Churn"].value_counts().plot(kind="bar", color=["steelblue", "salmon"])
plt.title("Distribución de Evasión de Clientes")
plt.xlabel("Evasión")
plt.ylabel("Cantidad de Clientes")
plt.xticks(ticks=[0, 1], labels=["No", "Sí"], rotation=0)
plt.show()
```

2. **Tasa de evasión por tipo de contrato:**

```python
df.groupby("Contract")["Churn"].mean().plot(kind="bar", color="coral")
plt.title("Tasa de Evasión por Tipo de Contrato")
plt.ylabel("Tasa de Evasión")
plt.xticks(rotation=45)
plt.show()
```

3. **Distribución de antigüedad (tenure) por grupo de evasión:**

```python
df.groupby("Churn")["tenure"].plot(kind="hist", alpha=0.5, bins=30)
plt.title("Distribución de Antigüedad por Evasión")
plt.xlabel("Meses de Contrato")
plt.legend(["No Evasión", "Evasión"])
plt.show()
```

4. **Facturación mensual promedio por evasión:**

```python
df.groupby("Churn")["Charges.Monthly"].mean().plot(kind="bar", color=["steelblue", "salmon"])
plt.title("Facturación Mensual Promedio por Evasión")
plt.ylabel("Promedio (USD)")
plt.xticks(ticks=[0, 1], labels=["No", "Sí"], rotation=0)
plt.show()
```

---

### Paso 9 – Informe de Insights

Al final del notebook, redacta un informe en celdas Markdown con los principales hallazgos. El informe debe responder, como mínimo, las siguientes preguntas:

1. **¿Cuál es la tasa general de evasión?**
2. **¿Qué perfil tiene un cliente con mayor probabilidad de evadir?** (antigüedad baja, contrato mensual, facturación alta, etc.)
3. **¿Qué tipo de contrato presenta mayor tasa de evasión?**
4. **¿Qué método de pago está asociado a mayor evasión?**
5. **¿Qué servicios adicionales (seguridad en línea, soporte técnico, etc.) reducen la probabilidad de evasión?**
6. **Recomendaciones accionables** para que el equipo de negocio reduzca la tasa de cancelación.

---

## Diccionario de Datos

| Columna | Descripción |
|---------|-------------|
| `customerID` | Número de identificación único de cada cliente |
| `Churn` | Si el cliente dejó o no la empresa |
| `gender` | Género del cliente (masculino / femenino) |
| `SeniorCitizen` | Si el cliente tiene 65 años o más (1 = Sí, 0 = No) |
| `Partner` | Si el cliente tiene pareja (Yes / No) |
| `Dependents` | Si el cliente tiene dependientes (Yes / No) |
| `tenure` | Meses de contrato del cliente |
| `PhoneService` | Suscripción al servicio telefónico (Yes / No) |
| `MultipleLines` | Suscripción a más de una línea telefónica |
| `InternetService` | Proveedor de internet contratado |
| `OnlineSecurity` | Suscripción adicional de seguridad en línea |
| `OnlineBackup` | Suscripción adicional de respaldo en línea |
| `DeviceProtection` | Suscripción adicional de protección del dispositivo |
| `TechSupport` | Suscripción adicional de soporte técnico |
| `StreamingTV` | Suscripción de televisión por cable |
| `StreamingMovies` | Suscripción de streaming de películas |
| `Contract` | Tipo de contrato (Month-to-month / One year / Two year) |
| `PaperlessBilling` | Si el cliente prefiere factura en línea (Yes / No) |
| `PaymentMethod` | Forma de pago |
| `Charges.Monthly` | Total de todos los servicios del cliente por mes |
| `Charges.Total` | Total gastado por el cliente durante toda su relación con la empresa |

> 📄 El diccionario completo también está disponible en `data/TelecomX_diccionario.md`.

---

## Entregables Esperados

Al finalizar el challenge, debes entregar:

1. **Notebook completo** (`notebooks/TelecomX_LATAM.ipynb`) con:
   - Código limpio, comentado y organizado por secciones.
   - Todas las etapas del ETL ejecutadas sin errores.
   - Al menos **4 visualizaciones** relevantes.
2. **Informe de insights** redactado en celdas Markdown dentro del notebook.
3. **Repositorio actualizado** en GitHub con todos los archivos del proyecto.

---

## Criterios de Evaluación

| Criterio | Descripción |
|----------|-------------|
| **Extracción de datos** | Los datos se cargan correctamente desde la API o el archivo local |
| **Limpieza de datos** | Se identifican y tratan valores nulos, duplicados e inconsistencias |
| **Transformaciones** | Las columnas tienen los tipos de datos correctos y los valores son coherentes |
| **Visualizaciones** | Los gráficos son claros, están bien etiquetados e interpretan correctamente los datos |
| **Análisis (EDA)** | Se responden las preguntas clave sobre evasión con evidencia en los datos |
| **Informe** | El informe es claro, estructurado y presenta recomendaciones accionables |
| **Código** | El código es legible, está comentado y sigue buenas prácticas |

---

> 🚀 ¡Buena suerte con el challenge! Recuerda que el objetivo es no solo obtener resultados, sino también contar una historia con los datos que ayude a Telecom X a tomar mejores decisiones.

