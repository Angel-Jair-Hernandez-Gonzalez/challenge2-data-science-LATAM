# Analysis of Customer Churn in Telecom X

**Análisis de Evasión de Clientes en Telecom X**

## Descripción del Proyecto

Este proyecto realiza un análisis exhaustivo del problema de evasión de clientes (Churn) en la empresa Telecom X. Mediante técnicas de análisis exploratorio de datos (EDA), se identifican los factores clave que influyen en la cancelación de servicios, proporcionando insights estratégicos para mejorar la retención de clientes.

## Contexto y Problemática

Telecom X enfrenta una **tasa de evasión del 26.58%**, lo que significa que aproximadamente 1 de cada 4 clientes cancela sus servicios. Este proyecto busca:

- Comprender los patrones de comportamiento de clientes evadidos
- Identificar variables categóricas y numéricas asociadas a la evasión
- Proporcionar recomendaciones estratégicas basadas en datos

## Estructura del Proyecto

```
challenge2-data-science-LATAM/
├── README.md                          # Este archivo (documentación del proyecto)
├── data/
│   ├── TelecomX_Data.json            # Dataset completo con estructura JSON anidada
│   └── TelecomX_diccionario.md       # Diccionario de datos y variable descriptions
└── notebooks/
    └── TelecomX_LATAM.ipynb          # Notebook principal con análisis completo
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

### 2. Iniciar Jupyter Notebook

```bash
# Navegar a la carpeta de notebooks
cd notebooks

# Iniciar el servidor Jupyter
jupyter notebook TelecomX_LATAM.ipynb
```

### 3. Ejecutar el Análisis

El notebook contiene celdas ejecutables en orden secuencial. Simplemente:
- Ejecutar todas las celdas: `Cell → Run All`
- O ejecutar celda por celda: `Shift + Enter`

## Contenido del Análisis

### 1. Extracción y Carga de Datos
- Carga de datos desde archivo JSON con estructura anidada
- Conversión a DataFrame de Pandas
- Dataset: 7,267 registros iniciales

### 2. Transformación y Limpieza
- Desanidación de 6 columnas originales en 21 variables
- Identificación y eliminación de 224 registros inválidos
- Corrección de tipos de datos
- Dataset limpio: 7,043 registros

### 3. Análisis Descriptivo
- Estadísticas descriptivas (media, mediana, desviación estándar)
- Análisis de correlación entre variables
- Distribución de variables numéricas

### 4. Distribución de Evasión
- Conteo y porcentaje de clientes evadidos vs activos
- Visualizaciones: gráficos de barras y pastel
- **Resultado: 26.58% de evasión (1,869 de 7,032 clientes)**

### 5. Análisis por Variables Categóricas
Análisis de 6 variables categóricas con las tasas de evasión más altas:

| Variable | Categoría | Tasa de Evasión |
|----------|-----------|-----------------|
| Método de Pago | Electronic check | 45.29% |
| Tipo de Contrato | Mes a mes | 42.71% |
| Tipo de Internet | Fibra óptica | 41.89% |
| Senior Citizen | Sí (≥65 años) | 41.68% |
| Pareja | No | 32.98% |
| Género | Mujer | 26.96% |

### 6. Análisis por Variables Numéricas
Comparación de distribuciones entre clientes evadidos y activos:

| Variable | Evadidos | Activos | Diferencia |
|----------|----------|---------|------------|
| Tenure (meses) | 17.98 | 37.65 | -19.67 |
| Charges.Total ($) | 1,531.80 | 2,555.34 | -1,023.55 |
| Charges.Monthly ($) | 74.44 | 61.31 | +13.13 |
| Cuentas_Diarias ($) | 2.48 | 2.04 | +0.44 |

## Resultados Principales

### Insights Clave

1. **Antigüedad del Cliente**: Clientes con menos de 18 meses de contrato tienen 2.4x más probabilidad de evasión
2. **Tipo de Contrato**: Los contratos mes a mes presentan 42.71% de evasión vs 10% para contratos de 2 años
3. **Tipo de Internet**: Servicio de fibra óptica tiene 41.89% de evasión (posibles problemas de calidad)
4. **Método de Pago**: Transferencia electrónica correlaciona con 45.29% de evasión
5. **Seniores**: Clientes de 65+ años tienen 41.68% de evasión
6. **Relaciones**: Clientes sin pareja tienen 32.98% de evasión

### Visualizaciones Generadas

- Gráficos de distribución de evasión (barras y pastel)
- Análisis de contingencia por 6 variables categóricas (6 gráficos)
- Boxplots de 4 variables numéricas (4 gráficos)
- Tablas cruzadas con porcentajes

## Conclusiones y Recomendaciones

### Recomendaciones Estratégicas

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

4. **Optimización de Métodos de Pago**
   - Investigar problemas con transferencias electrónicas
   - Ofrecer opciones de pago alternativas

5. **Segmentación por Perfil**
   - Crear programas específicos para seniores
   - Desarrollar estrategias para clientes sin pareja

## Tecnologías Utilizadas

- **Python 3.13**: Lenguaje de programación
- **Jupyter Notebook**: Entorno interactivo de análisis
- **Pandas**: Manipulación de datos
- **Matplotlib & Seaborn**: Visualización de datos
- **Git**: Control de versiones

## Autor

**Angel Jair Hernández González**

- GitHub: [Angel-Jair-Hernandez-Gonzalez](https://github.com/Angel-Jair-Hernandez-Gonzalez)
- Repositorio: [challenge2-data-science-LATAM](https://github.com/Angel-Jair-Hernandez-Gonzalez/challenge2-data-science-LATAM)

## Licencia

Este proyecto es de código abierto y disponible bajo la licencia MIT.

## Notas Importantes

- El análisis completo se ejecuta en aproximadamente 2-3 segundos
- Los gráficos se generan automáticamente durante la ejecución
- El informe final contiene conclusiones detalladas y recomendaciones basadas en datos
- Todos los datos están limpios y validados antes del análisis 