# Global Analysis of Mental Health Resources and Suicide Rates

> A comprehensive data science study examining the relationship between mental health investment and global suicide rates using WHO data.

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Plotly](https://img.shields.io/badge/Plotly-Visualization-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)](https://plotly.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## Table of Contents

- [About the Project](#about-the-project)
- [Key Research Question](#key-research-question)
- [Key Findings](#key-findings)
- [Datasets](#datasets)
- [Methodology](#methodology)
- [Results](#results)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Visualizations](#visualizations)
- [Policy Recommendations](#policy-recommendations)
- [Limitations](#limitations)
- [Author](#author)
- [References](#references)
- [License](#license)

---

## About the Project

This project presents a comprehensive analysis of the relationship between mental health resources available in countries worldwide and their suicide rates. Using advanced data science, machine learning, and statistical techniques, this study integrates four distinct WHO datasets to create a 360-degree view of global mental health infrastructure and mortality statistics.

**Author:** Maria Luisa Ros Bolea
**Date:** November 2025
**Data Source:** World Health Organization (WHO)

### Full Report

[Download PDF Report](https://github.com/user-attachments/files/23602586/A.Global.Analysis.of.Mental.Health.Resources.and.Suicide.Rates.by.Maria.Luisa.Ros.Bolea.pdf)

---

## Key Research Question

> **Do countries with more extensive mental health resources (higher density of psychiatrists, psychologists, and specialized facilities) have lower suicide rates?**

---

## Key Findings

| Finding | Description |
|---------|-------------|
| **R-squared: 34.2%** | Mental health resources and gender explain over one-third of suicide rate variance globally |
| **Gender is the strongest predictor** | Males have approximately 3x higher predicted suicide rates than females |
| **Outpatient facilities are protective** | Only resource type showing negative correlation with suicide rates |
| **Reverse causality observed** | Countries with higher suicide rates tend to have more specialists (reactive investment) |
| **Global inequality is severe** | Median psychiatrist density is only 1.1 per 100,000 people |

---

## Datasets

This analysis integrates four official WHO datasets:

| Dataset | Description | Key Variables |
|---------|-------------|---------------|
| **Human Resources** | Availability of mental health professionals | Psychiatrists, psychologists, nurses, social workers per 100k |
| **Facilities** | Mental health care infrastructure | Hospitals, clinics, outpatient facilities, day treatment centers |
| **Age-standardized Suicide Rates** | Suicide rates adjusted by age | Age-adjusted rates by country and sex |
| **Crude Suicide Rates** | Raw suicide rates | Rates by sex, country, and year (2000-2016) |

**Source:** [Kaggle - Mental Health and Suicide Rates](https://www.kaggle.com/datasets/twinkle0705/mental-health-and-suicide-rates)

---

## Methodology

### 1. Data Integration

```
Human Resources + Facilities → Resources DataFrame (by Country)
Age-standardized + Crude Rates → Suicide DataFrame (by Country + Sex)
Resources + Suicide → Final Combined Dataset
```

### 2. Data Cleaning

- **Missing Values:** Columns with >50% null values removed
- **Imputation:** Median imputation for remaining nulls (chosen due to skewed distributions)
- **Duplicates:** Identified and handled appropriately

### 3. Feature Engineering

- **Log Transformation:** Applied `np.log1p()` to handle outliers and stabilize variance
- **Encoding:** One-hot encoding for categorical variables (Sex)
- **Feature Selection:** Validated using Lasso regularization (no features eliminated)

### 4. Modeling Pipeline

```
Data Split (80/20) → StandardScaler → Model Training → Cross-Validation → Evaluation
```

**Models Evaluated:**
- Linear Regression
- Random Forest Regressor
- Lasso Regression (with GridSearchCV hyperparameter tuning)

---

## Results

### Model Performance

| Model | RMSE | R-squared | Notes |
|-------|------|-----------|-------|
| Linear Regression | 0.570 | 0.342 | Best overall performance |
| Random Forest | 0.579 | - | Slightly worse than linear |
| Lasso (GridSearchCV) | 0.570 | 0.341 | Confirms all features are relevant |

### Feature Coefficients

| Feature | Coefficient | Interpretation |
|---------|-------------|----------------|
| Sex_Male | +0.349 | Higher male suicide rates |
| Sex_Female | -0.572 | Lower female suicide rates |
| health_units_log | +0.110 | Reverse causality pattern |
| Psychiatrists_log | +0.076 | Reverse causality pattern |
| outpatient_facilities_log | **-0.093** | **Only protective feature** |

### Predictive Scenarios

| Scenario | Prediction |
|----------|------------|
| 20% increase in outpatient facilities | **-0.60%** suicide rate reduction |
| Typical country - Male | ~12.0 per 100k |
| Typical country - Female | ~4.2 per 100k |
| Male/Female ratio | **~3:1** |

---

## Technology Stack

### Core Technologies

| Category | Technologies |
|----------|-------------|
| **Language** | Python 3.8+ |
| **Environment** | Jupyter Notebook, Google Colab |
| **Data Processing** | Pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn, Plotly |
| **Machine Learning** | Scikit-learn |
| **Geospatial** | GeoPandas |

### Key Libraries

```python
# Data manipulation
pandas >= 1.3.0
numpy >= 1.21.0

# Visualization
matplotlib >= 3.4.0
seaborn >= 0.11.0
plotly >= 5.0.0

# Machine Learning
scikit-learn >= 0.24.0

# Geospatial
geopandas >= 0.10.0
```

---

## Project Structure

```
A-Global-Analysis-of-Mental-Health-Resources-and-Suicide-Rates/
|
+-- Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb  # Main analysis notebook
|
+-- A.Global.Analysis.of.Mental.Health.Resources.and.Suicide.Rates.by.Maria.Luisa.Ros.Bolea.pdf  # Full report
|
+-- README.md                                        # This file
+-- requirements.txt                                 # Python dependencies
+-- LICENSE                                          # MIT License
+-- .gitignore                                       # Git ignore rules
```

---

## Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager
- Git

### Local Setup

```bash
# Clone the repository
git clone https://github.com/malurosbolea-ux/A-Global-Analysis-of-Mental-Health-Resources-and-Suicide-Rates.git

# Navigate to project directory
cd A-Global-Analysis-of-Mental-Health-Resources-and-Suicide-Rates

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

---

## Usage

### Option 1: Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com/)
2. Upload `Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb`
3. Upload the required CSV datasets to `/content/`
4. Run all cells

### Option 2: Local Jupyter Notebook

```bash
# Start Jupyter Notebook
jupyter notebook

# Open the notebook file
# Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb
```

### Required Data Files

Download from [Kaggle](https://www.kaggle.com/datasets/twinkle0705/mental-health-and-suicide-rates):
- `Age-standardized suicide rates.csv`
- `Crude suicide rates.csv`
- `Facilities.csv`
- `Human Resources.csv`

---

## Visualizations

The notebook includes several types of visualizations:

### Statistical Visualizations
- **Correlation Heatmaps:** Show relationships between all variables
- **Box Plots:** Identify outliers before and after log transformation
- **Scatter Plots with Regression Lines:** Visualize individual feature relationships

### Geospatial Visualizations
- **Choropleth Maps:**
  - Global suicide rates (2016)
  - Psychiatrist density by country
  - Outpatient facility distribution

---

## Policy Recommendations

Based on the analysis findings:

### 1. Invest in Community-Based Services
Outpatient facilities show the strongest protective association. Priority should be given to accessible, community-level mental health services.

### 2. Implement Gender-Specific Prevention
Male suicide risk is consistently ~3x higher. Prevention strategies should address male-specific risk factors and barriers to seeking help.

### 3. Proactive Resource Allocation
Use predictive models to anticipate risk increases rather than react to existing high rates.

### 4. Improve Data Systems
Several countries lack reliable mental health data. International investment in reporting infrastructure is essential.

### 5. Target International Aid
Regions with <1 psychiatrist per 100,000 people should receive priority support.

---

## Limitations

- **Model explains 34.2% of variance:** Many unmeasured factors (socioeconomic, cultural) influence suicide rates
- **Data quality varies:** Some countries have incomplete or unreliable reporting
- **Correlation =/= Causation:** Observed relationships may not be causal
- **Temporal limitations:** Analysis focused on 2016 data
- **Missing data:** Required extensive imputation which may introduce bias

---

## Technical Skills Demonstrated

- Advanced Python programming
- Data wrangling with Pandas
- Feature engineering and selection
- Exploratory Data Analysis (EDA)
- Machine learning modeling
- Lasso regularization
- Cross-validation techniques
- Hyperparameter tuning (GridSearchCV)
- Geospatial visualizations with Plotly
- Statistical interpretation
- Data storytelling and reporting

---

## Author

**Maria Luisa Ros Bolea**

| Platform | Link |
|----------|------|
| Email | malurosbolea@gmail.com |
| LinkedIn | [Maria Luisa Ros Bolea](https://www.linkedin.com/in/mar%C3%ADa-luisa-ros-bolea-400780160/) |
| GitHub | [@malurosbolea-ux](https://github.com/malurosbolea-ux) |
| Portfolio | [Digital Portfolio](https://marialuisarosboleaportfolio.my.canva.site/porfolio-profesional-mar-a-luisa-ros-bolea-actualizado) |

---

## References

- World Health Organization (WHO) - Mental Health Atlas
- National Institute of Mental Health (NIMH)
- Our World in Data - Suicide Statistics
- Kaggle Datasets - Mental Health and Suicide Rates
- Scientific literature on global mental health systems

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

Special thanks to:
- The World Health Organization for providing comprehensive global mental health data
- The Kaggle community for making datasets accessible
- The open-source community for the tools that made this analysis possible

---

<div align="center">

**If you found this project useful, please consider giving it a star!**

Made with dedication by Maria Luisa Ros Bolea

</div>
