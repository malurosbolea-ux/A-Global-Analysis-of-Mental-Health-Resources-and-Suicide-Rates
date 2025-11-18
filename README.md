# 🧠 Análisis global de recursos de salud mental y tasas de suicidio

**Un estudio data-driven sobre la relación entre inversión en salud mental e impacto en tasas de suicidio a nivel mundial**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Latest-red.svg)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-blue.svg)](https://pandas.pydata.org/)

---

## 📖 Sobre el proyecto

Este proyecto presenta un análisis exhaustivo de la relación entre los recursos de salud mental disponibles en un país y sus tasas de suicidio. A través de técnicas avanzadas de ciencia de datos, machine learning y análisis estadístico, se investiga una pregunta fundamental:

> **¿Demuestran los países con recursos más extensos de salud mental (mayor densidad de psiquiatras, psicólogos e instalaciones especializadas) tasas de suicidio más bajas?**

El análisis unifica y procesa cuatro datasets distintos de la Organización Mundial de la Salud (WHO) para crear una visión 360º que combina recursos humanos, infraestructura sanitaria y estadísticas de mortalidad por país.

**Desarrollado por:** María Luisa Ros Bolea  
**Fecha:** Noviembre 2025  
**Fuente de datos:** World Health Organization (WHO)

---

## 🎯 Objetivos del análisis

1. **Integrar datos globales dispersos** en un único marco analítico cohesivo que permita investigar patrones a escala mundial
2. **Limpiar y preparar datos robustos** mediante técnicas avanzadas de imputación y transformación para manejar valores nulos y outliers
3. **Explorar relaciones complejas** entre variables a través de visualizaciones avanzadas (heatmaps, scatter plots, mapas coropléticos interactivos)
4. **Desarrollar modelos predictivos** que cuantifiquen el impacto de los recursos de salud mental en las tasas de suicidio
5. **Generar insights accionables** para informar políticas públicas de salud mental basadas en evidencia

---

## 📊 Datasets utilizados

El análisis integra cuatro datasets oficiales de la WHO:

| Dataset | Descripción | Variables clave |
|---------|-------------|-----------------|
| **Human Resources** | Cuantifica la disponibilidad de profesionales de salud mental | Psiquiatras, psicólogos, enfermeras, trabajadores sociales (por 100,000 hab.) |
| **Facilities** | Detalla la infraestructura de atención en salud mental | Hospitales psiquiátricos, unidades de salud, instalaciones ambulatorias |
| **Age-standardized suicide rates** | Tasas de suicidio estandarizadas por edad | Tasas ajustadas por grupos etarios (10-19, 20-29, ..., 80+) |
| **Crude suicide rates** | Tasas brutas de suicidio sin ajuste | Tasas generales por país y sexo |

**Fuente:** [Mental Health and Suicide Rates - Kaggle](https://www.kaggle.com/datasets/twinkle0705/mental-health-and-suicide-rates)

---

## 🛠️ Stack tecnológico

### Lenguajes y entornos
- **Python 3.8+**: Lenguaje principal del análisis
- **Jupyter Notebook**: Entorno de desarrollo interactivo
- **Google Colab**: Plataforma de ejecución en la nube (opcional)

### Librerías de análisis y manipulación de datos
```python
pandas>=1.3.0           # Manipulación y análisis de datos
numpy>=1.21.0           # Operaciones numéricas y álgebra lineal
```

### Visualización de datos
```python
matplotlib>=3.4.0       # Visualizaciones estáticas base
seaborn>=0.11.0         # Visualizaciones estadísticas avanzadas
plotly>=5.0.0           # Mapas interactivos y choropleth maps
```

### Machine Learning
```python
scikit-learn>=0.24.0    # Modelos de ML, métricas y validación
# Modelos utilizados:
# - LinearRegression
# - Lasso (con GridSearchCV)
# - RandomForestRegressor
# - StandardScaler
# - train_test_split, cross_val_score
```

---

## 📁 Estructura del proyecto

```
├── Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb
├── A_Global_Analysis_of_Mental_Health_Resources_and_Suicide_Rates_by_Maria_Luisa_Ros_Bolea.pdf
├── data/
│   ├── Age-standardized suicide rates.csv
│   ├── Crude suicide rates.csv
│   ├── Facilities.csv
│   └── Human Resources.csv
└── README.md
```

---

## 🔬 Metodología del análisis

### 1. Unificación de datos

**Estrategia de fusión por etapas:**
1. **Merge de recursos**: `Human Resources` + `Facilities` → unificados por `Country`
2. **Merge de tasas**: `Age-standardized rates` + `Crude rates` → unificados por `Country` y `Sex`
3. **Fusión final**: Recursos + Tasas → DataFrame maestro consolidado

**Resultado:** Un único DataFrame con información completa de recursos, infraestructura y tasas de suicidio por país y sexo.

### 2. Limpieza de datos

#### Manejo de valores nulos - Imputación por mediana
**Desafío:** Presencia significativa de valores nulos en columnas de recursos (hasta 50% en algunas variables)

**Solución adoptada:**
- **Técnica:** Imputación por mediana (en lugar de media)
- **Justificación:** Los datos presentan alta asimetría (skewness). La mediana es robusta a outliers y proporciona un estimado conservador y realista del "país típico"
- **Resultado:** Dataset completo sin pérdida de países en el análisis

**Columnas imputadas:**
- `Psychiatrists` (308/552 valores originales)
- `Psychologists`
- `Social_workers` (200/552 valores originales)
- `Nurses`
- `Mental_hospitals`
- `health_units`
- `outpatient_facilities` (149/552 valores originales)
- `day_treatment`
- `residential_facilities`

### 3. Manejo de outliers - Transformación logarítmica

**Problema identificado:** Distribuciones extremadamente sesgadas hacia la derecha con numerosos outliers (países con recursos excepcionales)

**Solución:** Transformación logarítmica `np.log1p()`

**Beneficios:**
- Comprime la escala de datos, acercando outliers al resto sin eliminarlos
- Normaliza distribuciones para cumplir supuestos de modelos lineales
- Mejora el rendimiento y estabilidad de los modelos predictivos

**Variables transformadas:**
- `Psychiatrists_log`
- `Psychologists_log`
- `Nurses_log`
- `Social_workers_log`
- `Mental_hospitals_log`
- `health_units_log`
- `outpatient_facilities_log`
- `day_treatment_log`
- `residential_facilities_log`
- `2000_log` (tasa de suicidio año 2000)
- `2015_log` (tasa de suicidio año 2015)
- `2016_log` (tasa de suicidio año 2016 - variable objetivo)

### 4. Preparación para modelado predictivo

#### Selección de variables

**Variable objetivo (y):**
- `2016_log`: Tasa de suicidio estandarizada por edad más reciente (transformada logarítmicamente)

**Características predictoras (X):**
- `Psychiatrists_log`: Densidad de psiquiatras
- `health_units_log`: Número de unidades de salud mental
- `outpatient_facilities_log`: Instalaciones ambulatorias
- `Sex`: Variable categórica (Female/Male) → One-Hot Encoded

#### Preprocesamiento final
- **One-Hot Encoding** de la variable `Sex` con `drop_first=True` para evitar multicolinealidad
- **Train-Test Split**: 80% entrenamiento / 20% prueba
- **Random state fijado** para reproducibilidad

---

## 🤖 Modelado predictivo y resultados

### Modelo 1: Linear Regression (baseline)

**Configuración:**
- Modelo: Regresión Lineal estándar
- Features: 4 variables (Psychiatrists_log, health_units_log, outpatient_facilities_log, Sex_Male)
- Target: 2016_log

**Resultados:**
- **RMSE (Root Mean Squared Error):** 0.5701
- **R² (R-squared):** 0.3420 (34.2%)

**Interpretación:**
- El modelo explica **34.2% de la variación** en las tasas de suicidio globales
- Para un fenómeno complejo de salud pública, explicar más de un tercio de la varianza con solo recursos de salud mental es un hallazgo altamente significativo
- Valida estadísticamente que existe una relación sustancial entre inversión en salud mental y tasas de suicidio

### Modelo 2: Cross-Validation (5-fold)

**Objetivo:** Validar la robustez del modelo y evitar overfitting

**Modelos comparados:**
1. **Linear Regression:** RMSE promedio = 0.573
2. **Random Forest Regressor:** RMSE promedio = 0.579

**Conclusión:** La regresión lineal supera ligeramente al Random Forest, indicando que la relación subyacente es predominantemente lineal (no requiere modelos complejos no lineales).

### Modelo 3: Lasso Regression con GridSearchCV

**Objetivo:** Realizar selección automática de características mediante regularización L1

**Proceso:**
- GridSearchCV para optimizar hiperparámetro `alpha`
- Lasso reduce coeficientes de características menos importantes (potencialmente a cero)

**Resultados:**
- **RMSE:** 0.570
- **R²:** 0.341
- **Hallazgo crítico:** NINGÚN coeficiente fue reducido a cero

**Conclusión:** El modelo Lasso **valida que todas las características seleccionadas son relevantes**. Esto confirma que la selección inicial de variables fue óptima y que cada recurso de salud mental contribuye información predictiva valiosa.

---

## 📈 Análisis de coeficientes del modelo

### Coeficientes del modelo de regresión lineal

| Variable | Coeficiente | Interpretación |
|----------|------------|----------------|
| **Psychiatrists_log** | +0.076 | ⚠️ Relación positiva (paradoja de causalidad inversa) |
| **health_units_log** | +0.110 | ⚠️ Relación positiva (paradoja de causalidad inversa) |
| **outpatient_facilities_log** | **-0.093** | ✅ Asociado con REDUCCIÓN de tasas de suicidio |
| **Sex_Female** | -0.572 | ✅ Tasas significativamente menores en mujeres |
| **Sex_Male** | +0.349 | ⚠️ Tasas significativamente mayores en hombres |

**Intercepto del modelo:** 2.191

### Interpretación de la "paradoja" de coeficientes positivos

**¿Por qué más psiquiatras correlaciona con MÁS suicidios?**

Este resultado NO implica que los psiquiatras "causen" suicidios. La interpretación correcta es:

🔄 **Causalidad inversa (reverse causality):**
- Los países con tasas de suicidio históricamente altas **invierten más recursos especializados en respuesta al problema**
- Los recursos se concentran reactivamente donde la crisis ya es severa
- Ejemplo: Un país con alta incidencia de suicidios contrata más psiquiatras para abordar la emergencia de salud pública

### Hallazgo clave: Instalaciones ambulatorias

✅ **Única variable con coeficiente negativo** → asociada directamente con reducción de tasas de suicidio

**Implicación estratégica:**
- La atención comunitaria y ambulatoria (más accesible, menos estigmatizada) es más efectiva para prevención que recursos altamente especializados
- Sugiere que la prevención de suicidio se beneficia más de servicios **accesibles y descentralizados** que de infraestructura hospitalaria especializada

---

## 🗺️ Visualizaciones y análisis exploratorio

### 1. Heatmap de correlaciones

**Hallazgos principales:**
- Correlación moderada (+0.52) entre `Psychiatrists_log` y `health_units_log` → las estrategias nacionales tienden a combinar personal especializado con infraestructura hospitalaria
- Correlación positiva débil-moderada entre recursos y tasas de suicidio (confirma paradoja)
- Variables de recursos están interconectadas (no actúan de forma independiente)

### 2. Scatter plot: Psychiatrists vs Suicide Rate

**Observaciones:**
- Tendencia general positiva (línea de regresión ascendente)
- Alta dispersión de puntos → múltiples factores en juego
- Visualización directa del fenómeno de "reverse causality"

### 3. Choropleth maps (mapas coropléticos interactivos)

#### Mapa A: Densidad de psiquiatras por país

**Patrones geográficos identificados:**
- **Alta concentración:** Europa, Norteamérica, Australia (>10-20 psiquiatras/100k hab.)
- **Escasez crítica:** África, Asia, Sudamérica (<1 psiquiatra/100k hab.)
- **Datos faltantes:** Regiones grises (África subsahariana, Asia Central)

**Conclusión:** Desigualdad masiva en acceso a profesionales de salud mental especializados

#### Mapa B: Densidad de instalaciones ambulatorias

**Diferencias respecto al mapa de psiquiatras:**
- Algunos países de Sudamérica (Chile, Brasil, Uruguay) y Europa del Este muestran mayor densidad relativa
- Sugiere **estrategias diferenciadas**: algunos países priorizan atención comunitaria sobre especialistas
- Refuerza hallazgo del modelo: las instalaciones ambulatorias son una estrategia efectiva

**Insight estratégico:** No todos los países invierten de la misma manera. Hay modelos de atención mental distintos, y el análisis sugiere que el modelo comunitario puede ser más protector.

---

## 🔮 Predicciones y escenarios hipotéticos

### Escenario A: Impacto de aumentar instalaciones ambulatorias en 20%

**Metodología:**
1. Crear perfil de "país típico" (medianas de todos los recursos)
2. Generar escenario hipotético con +20% en `outpatient_facilities_log`
3. Predecir tasas de suicidio con el modelo entrenado

**Resultado:**
- **Reducción predicha:** 0.60% en la tasa nacional de suicidio

**Interpretación:**
- Aunque 0.60% parece modesto, a escala nacional/global representa **miles de vidas salvadas**
- Proporciona una estimación cuantitativa del ROI (Return on Investment) de políticas públicas en salud mental comunitaria

### Escenario B: Diferencia por género en país con recursos típicos

**Metodología:**
1. Perfil de país típico (medianas de recursos)
2. Predecir tasa para población masculina
3. Predecir tasa para población femenina

**Resultados:**
- **Tasa predicha (hombres):** ~12.0 por 100,000 habitantes
- **Tasa predicha (mujeres):** ~4.2 por 100,000 habitantes
- **Diferencia:** Los hombres tienen una tasa **casi 3 veces mayor** que las mujeres

**Conclusión:** El género es el predictor individual más poderoso del modelo, confirmando vulnerabilidad desproporcionada de la población masculina.

---

## 💡 Hallazgos principales

### 1. Evidencia estadística sólida de la relación recursos-suicidio

✅ **34.2% de la variación** en tasas de suicidio globales se explica por disponibilidad de recursos de salud mental y género  
✅ Este es un hallazgo **altamente significativo** para un fenómeno de salud pública tan complejo y multifactorial  
✅ Valida la hipótesis central: la inversión en salud mental es un factor crítico y medible

### 2. El género como factor dominante

⚠️ **Hallazgo crítico:** El sexo es el predictor individual más fuerte del modelo  
📊 **Tasas en hombres:** ~3x mayores que en mujeres en países con recursos equivalentes  
🎯 **Implicación:** Las políticas de prevención deben ser **específicas por género**, con énfasis en destigmatizar la búsqueda de ayuda en población masculina

### 3. La eficacia de la atención comunitaria

✅ **Único recurso con asociación protectora directa:** Instalaciones ambulatorias  
✅ **Coeficiente negativo:** A mayor densidad de centros comunitarios, menor tasa de suicidio  
🏥 **Implicación estratégica:** Priorizar servicios accesibles, descentralizados y menos estigmatizados sobre hospitales psiquiátricos tradicionales

### 4. La paradoja de los recursos especializados

🔄 **Causalidad inversa:** Más psiquiatras correlacionan con MÁS suicidios  
🧠 **Interpretación correcta:** Los recursos especializados se concentran **reactivamente** en países donde el problema ya es grave  
📍 **Implicación:** Necesidad de cambiar de un enfoque reactivo a uno **proactivo y preventivo**

### 5. Desigualdad global masiva en salud mental

🌍 **Brecha crítica:** Diferencia de >20x en densidad de profesionales entre países desarrollados y en desarrollo  
📉 **Regiones más afectadas:** África subsahariana, Asia Central y Sur, partes de Latinoamérica  
🚨 **Problema adicional:** Falta de datos fiables en países más vulnerables

---

## 📋 Recomendaciones basadas en evidencia

### 1. Invertir en atención comunitaria accesible

**Evidencia del modelo:**
- Instalaciones ambulatorias son el único recurso con asociación protectora directa
- Coeficiente: -0.093 (reducción de tasas)

**Acción recomendada:**
- Priorizar creación de **clínicas de salud mental comunitarias**
- Expandir **centros de día** y **servicios ambulatorios**
- Reducir dependencia de hospitales psiquiátricos centralizados
- Aumentar en 20% = reducción estimada del 0.6% en tasas nacionales

### 2. Crear programas específicos para hombres

**Evidencia del modelo:**
- Género es el predictor más fuerte (coeficiente: +0.349 para hombres)
- Tasas masculinas 3x superiores a femeninas

**Acción recomendada:**
- Campañas de **destigmatización** dirigidas a población masculina
- Crear **canales de comunicación** que resuenen con hombres
- Programas de prevención adaptados culturalmente
- Integrar salud mental en contextos masculinos (deportes, trabajo, veteranos)

### 3. Asignación proactiva (no reactiva) de recursos

**Evidencia del modelo:**
- Paradoja de causalidad inversa → recursos se concentran donde problema ya es grave

**Acción recomendada:**
- Usar **modelos predictivos** para identificar regiones en riesgo antes de que tasas aumenten
- Asignar recursos de forma **preventiva** a áreas con perfiles de alto riesgo pero baja cobertura actual
- Monitoreo continuo con sistemas de alerta temprana

### 4. Mejorar recolección global de datos

**Evidencia del análisis:**
- 50% de valores nulos en algunas variables de recursos
- Datos faltantes concentrados en países más vulnerables

**Acción recomendada:**
- Establecer **estándares globales** para reporte de datos de salud mental (WHO, gobiernos)
- Priorizar inversión en sistemas de información en países en desarrollo
- Crear bases de datos actualizadas y accesibles
- "No puedes gestionar lo que no mides"

### 5. Focalizar ayuda internacional en poblaciones de alto riesgo

**Evidencia del análisis:**
- Mapas coropléticos muestran escasez crítica en África, Asia, Sudamérica
- Datos brutos confirman grupo etario 80+ con tasas más altas

**Acción recomendada:**
- Programas de ayuda internacional deben **priorizar** regiones con <1 psiquiatra/100k habitantes
- Diseñar intervenciones **culturalmente apropiadas**
- Enfoque especial en población adulta mayor
- Superar barreras de acceso (geográficas, económicas, culturales)

---

## 🚀 Cómo ejecutar el proyecto

### Requisitos previos

1. Python 3.8 o superior
2. Jupyter Notebook o Google Colab
3. Datasets descargados de Kaggle

### Opción 1: Google Colab (recomendado)

```bash
1. Descarga los 4 archivos CSV de Kaggle
2. Sube el notebook a Google Drive
3. Abre con Google Colab
4. Sube los CSVs a Colab o móntalos desde Drive
5. Ejecuta las celdas secuencialmente
```

### Opción 2: Entorno local

```bash
# Clonar el repositorio
git clone https://github.com/malurosbolea-ux/mental-health-suicide-analysis.git
cd mental-health-suicide-analysis

# Crear entorno virtual
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# Instalar dependencias
pip install pandas numpy matplotlib seaborn plotly scikit-learn jupyter

# Descargar datasets
# Coloca los 4 CSVs en el directorio data/

# Abrir Jupyter Notebook
jupyter notebook Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb
```

---

## 📚 Estructura del notebook

El análisis está organizado en las siguientes secciones:

1. **Importación de librerías y carga de datos**
2. **Unificación de datasets**
   - Merge de Human Resources + Facilities
   - Merge de Age-standardized + Crude rates
   - Fusión final en DataFrame maestro
3. **Limpieza de datos**
   - Identificación de valores nulos
   - Imputación por mediana
4. **Manejo de outliers**
   - Visualización de distribuciones (boxplots)
   - Transformación logarítmica
5. **Análisis exploratorio de datos (EDA)**
   - Estadísticas descriptivas
   - Identificación de patrones
6. **Preparación para modelado**
   - Selección de target y features
   - One-Hot Encoding
   - Train-test split
7. **Modelado predictivo**
   - Linear Regression (baseline)
   - Cross-validation (Linear Regression vs Random Forest)
   - Lasso Regression con GridSearchCV
8. **Análisis de coeficientes**
   - Interpretación de resultados
   - Fenómeno de causalidad inversa
9. **Visualizaciones avanzadas**
   - Heatmap de correlaciones
   - Scatter plot con línea de regresión
   - Choropleth maps interactivos (Plotly)
10. **Predicciones y escenarios**
    - Escenario: +20% instalaciones ambulatorias
    - Escenario: Diferencia por género
11. **Conclusiones y recomendaciones**
12. **Bibliografía**

---

## 🎓 Competencias técnicas demostradas

Este proyecto demuestra dominio en:

- ✅ **Python avanzado** para ciencia de datos
- ✅ **Pandas y NumPy** para manipulación y análisis de datos complejos
- ✅ **Limpieza de datos profesional** (imputación, manejo de outliers, transformaciones)
- ✅ **Análisis exploratorio de datos (EDA)** profundo y sistemático
- ✅ **Visualización de datos** con Matplotlib, Seaborn y Plotly
- ✅ **Machine Learning supervisado** (regresión lineal, Lasso, Random Forest)
- ✅ **Validación de modelos** (train-test split, cross-validation)
- ✅ **Optimización de hiperparámetros** (GridSearchCV)
- ✅ **Interpretación de modelos** y análisis de coeficientes
- ✅ **Análisis de causalidad** y pensamiento crítico estadístico
- ✅ **Mapas interactivos** con Plotly (choropleth maps)
- ✅ **Comunicación de resultados** y storytelling con datos
- ✅ **Generación de insights accionables** para políticas públicas

---

## 📊 Métricas clave del proyecto

| Métrica | Valor | Interpretación |
|---------|-------|----------------|
| **R² (R-squared)** | 0.342 | 34.2% de variación en tasas de suicidio explicada por el modelo |
| **RMSE** | 0.570 | Error promedio de predicción en escala logarítmica |
| **Cross-validation RMSE** | 0.573 | Rendimiento consistente en 5 folds (modelo robusto) |
| **Lasso RMSE** | 0.570 | Rendimiento equivalente con regularización L1 |
| **Features seleccionadas** | 4 | Todas validadas como relevantes por Lasso (ninguna eliminada) |
| **Países analizados** | 276 | Cobertura global comprehensiva |
| **Reducción predicha (escenario +20%)** | 0.60% | Impacto estimado de aumentar instalaciones ambulatorias |
| **Ratio de tasas hombre/mujer** | ~3:1 | Disparidad de género en vulnerabilidad al suicidio |

---

## 🌟 Conclusiones finales

### La respuesta a la pregunta inicial

**¿Existe una relación medible entre inversión en salud mental y tasas de suicidio?**

**Respuesta: Sí, rotundamente, aunque compleja.**

A través de un modelo de regresión lineal validado rigurosamente con cross-validation, se determinó que **34.2% de la variación en las tasas globales de suicidio puede explicarse** por la disponibilidad de recursos de salud mental y el género. Este es un hallazgo estadísticamente significativo que confirma la hipótesis central del proyecto.

### Tres conclusiones críticas

1. **El género es el factor dominante:**  
   El modelo identificó el sexo como el predictor individual más poderoso, confirmando la mayor vulnerabilidad de la población masculina (tasas ~3x superiores a las de mujeres). Esto alinea con datos epidemiológicos globales y señala la necesidad urgente de programas específicos por género.

2. **La eficacia de la atención comunitaria:**  
   Crucialmente, la inversión en **instalaciones ambulatorias y atención comunitaria** se asocia con una **reducción directa en tasas de suicidio**, sugiriendo que las políticas enfocadas en servicios accesibles, descentralizados y menos estigmatizados son una estrategia efectiva.

3. **La "paradoja" de los recursos especializados:**  
   El modelo reveló una relación "paradójica" donde mayor concentración de psiquiatras correlaciona con tasas más altas. La interpretación correcta no es causal sino de **"causalidad inversa"**: los recursos más especializados se concentran reactivamente en regiones donde el problema ya es grave. Esto subraya la necesidad de **cambiar de un enfoque reactivo a uno proactivo**.

### El desafío de los datos

El principal obstáculo del proyecto fue la **calidad y completitud de los datos** sobre recursos en muchos países, especialmente en regiones más vulnerables. Esto subraya la necesidad crítica de mejorar los sistemas globales de reporte para análisis futuros más precisos.

### Mensaje final

Este análisis ha transformado datos complejos y dispersos en una conclusión clara: aunque no existen soluciones únicas, **la inversión estratégica en salud mental, especialmente a nivel comunitario, es un factor clave y medible** para abordar el desafío global del suicidio. Los modelos predictivos como el desarrollado en este proyecto pueden ser herramientas poderosas para informar políticas públicas basadas en evidencia.

---

## 📚 Bibliografía

### Libros de referencia

- James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). *An Introduction to Statistical Learning: with Applications in R*. Springer.
- VanderPlas, J. (2016). *Python Data Science Handbook: Essential Tools for Working with Data*. O'Reilly Media.

### Recursos web

- **World Health Organization (WHO).** (2021). Suicide - Fact Sheets. [https://www.who.int/news-room/fact-sheets/detail/suicide](https://www.who.int/news-room/fact-sheets/detail/suicide)
- **National Institute of Mental Health (NIMH).** Suicide Prevention. U.S. Department of Health and Human Services. [https://www.nimh.nih.gov/health/topics/suicide-prevention](https://www.nimh.nih.gov/health/topics/suicide-prevention)
- **Ritchie, H., Roser, M., & Ortiz-Ospina, E.** (2018). Suicide. *Our World in Data*. [https://ourworldindata.org/suicide](https://ourworldindata.org/suicide)
- **Ministerio de Sanidad de España.** Estrategia de Salud Mental del Sistema Nacional de Salud. [https://www.sanidad.gob.es/organizacion/sns/planCalidadSNS/especialidades/saludMental.htm](https://www.sanidad.gob.es/organizacion/sns/planCalidadSNS/especialidades/saludMental.htm)

### Dataset

- **Kaggle Dataset:** [Mental Health and Suicide Rates](https://www.kaggle.com/datasets/twinkle0705/mental-health-and-suicide-rates)

---

## 📧 Contacto

**María Luisa Ros Bolea**

📧 Email: malurosbolea@gmail.com  
💼 LinkedIn: [María Luisa Ros Bolea](https://www.linkedin.com/in/maría-luisa-ros-bolea-400780160/)  
🐙 GitHub: [@malurosbolea-ux](https://github.com/malurosbolea-ux)  
🌐 Portfolio: [Portfolio Profesional](https://marialuisarosboleaportfolio.my.canva.site/porfolio-profesional-mar-a-luisa-ros-bolea-actualizado)

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.

---

## 🙏 Agradecimientos

Agradezco a la Organización Mundial de la Salud (WHO) por poner a disposición pública los datasets utilizados en este análisis. Este proyecto demuestra el poder de los datos abiertos para abordar desafíos críticos de salud pública global.

Un agradecimiento especial a la comunidad de ciencia de datos por las herramientas open-source que hicieron posible este análisis.

---

## ⚠️ Nota importante

Este proyecto tiene fines **educativos y de investigación**. Las predicciones y recomendaciones generadas deben ser consideradas como **insights preliminares basados en datos históricos**, no como sustitutos de estudios epidemiológicos exhaustivos o asesoramiento profesional en salud pública.

La relación entre recursos de salud mental y tasas de suicidio es **compleja y multifactorial**. Este análisis captura correlaciones estadísticas significativas pero no establece causalidad definitiva. Las decisiones de política pública deben basarse en múltiples fuentes de evidencia y contexto local.

---

**⭐ Si este proyecto te resulta útil o interesante, considera darle una estrella en GitHub!**

*Desarrollado con 💜 y datos por María Luisa Ros Bolea - Noviembre 2025*

---

## 🔗 Enlaces rápidos

- [📊 Ver notebook completo](Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb)
- [📄 Descargar informe PDF](A_Global_Analysis_of_Mental_Health_Resources_and_Suicide_Rates_by_Maria_Luisa_Ros_Bolea.pdf)
- [📁 Descargar datasets (Kaggle)](https://www.kaggle.com/datasets/twinkle0705/mental-health-and-suicide-rates)
- [🌐 Mi portfolio profesional](https://marialuisarosboleaportfolio.my.canva.site/porfolio-profesional-mar-a-luisa-ros-bolea-actualizado)
