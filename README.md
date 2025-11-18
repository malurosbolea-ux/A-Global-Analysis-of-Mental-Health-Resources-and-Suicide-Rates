# 🧠 Global Analysis of Mental Health Resources and Suicide Rates

**A data-driven study on the relationship between mental health investment and global suicide rates**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Latest-red.svg)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-blue.svg)](https://pandas.pydata.org/)

---

## 📖 About the Project

This project presents a comprehensive analysis of the relationship between the mental health resources available in a country and its suicide rates. Using advanced data science, machine learning, and statistical techniques, this study investigates a key question:

> **Do countries with more extensive mental health resources (higher density of psychiatrists, psychologists, and specialized facilities) have lower suicide rates?**

The analysis merges and processes four separate WHO datasets to create a full 360° view combining human resources, infrastructure, and global mortality statistics.

**Developed by:** María Luisa Ros Bolea  
**Date:** November 2025  
**Data Source:** World Health Organization (WHO)

PDF:
[A.Global.Analysis.of.Mental.Health.Resources.and.Suicide.Rates.by.Maria.Luisa.Ros.Bolea.pdf](https://github.com/user-attachments/files/23602586/A.Global.Analysis.of.Mental.Health.Resources.and.Suicide.Rates.by.Maria.Luisa.Ros.Bolea.pdf)

---

## 🎯 Objectives of the Analysis

1. Integrate scattered global datasets into one cohesive analytical framework  
2. Clean and prepare robust datasets using advanced imputation and transformation methods  
3. Explore complex variable relationships with heatmaps, scatter plots, and interactive maps  
4. Develop predictive models to quantify the impact of mental health resources  
5. Generate data-driven insights for public health policy  

---

## 📊 Datasets Used

The analysis integrates four official WHO datasets:

| Dataset | Description | Key Variables |
|---------|-------------|-----------------|
| Human Resources | Availability of mental health professionals | Psychiatrists, psychologists, nurses, social workers |
| Facilities | Mental health care infrastructure | Hospitals, clinics, outpatient facilities |
| Age-standardized suicide rates | Suicide rates adjusted by age | Age-adjusted suicide rates |
| Crude suicide rates | Raw suicide rates | Suicide rates by sex and country |

Source:  
https://www.kaggle.com/datasets/twinkle0705/mental-health-and-suicide-rates

---

## 🛠️ Technology Stack

### Languages / Environments
- Python 3.8+  
- Jupyter Notebook  
- Google Colab  

### Libraries for Data Processing
pandas>=1.3.0  
numpy>=1.21.0  

### Libraries for Visualization
matplotlib>=3.4.0  
seaborn>=0.11.0  
plotly>=5.0.0  

### Machine Learning Libraries
scikit-learn>=0.24.0  
(LinearRegression, Lasso, RandomForestRegressor, StandardScaler, train_test_split, cross_val_score)

---

## 📁 Project Structure

├── Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb  
├── A_Global_Analysis_of_Mental_Health_Resources_and_Suicide_Rates_by_Maria_Luisa_Ros_Bolea.pdf  
├── data/  
│   ├── Age-standardized suicide rates.csv  
│   ├── Crude suicide rates.csv  
│   ├── Facilities.csv  
│   └── Human Resources.csv  
└── README.md  

---

## 🔬 Methodology

### 1. Merging the datasets

The four WHO datasets were merged through these steps:

1. Human Resources + Facilities (joining by Country)  
2. Age-standardized + Crude suicide rates (joining by Country + Sex)  
3. Final merge combining resources and suicide rates  

### 2. Cleaning the data

#### Median Imputation

Many resource variables had up to 50% missing values.  
Median was chosen due to skewed distributions.

Variables imputed include:  
Psychiatrists, Psychologists, Nurses, Social Workers, Mental Hospitals, Health Units, Outpatient Facilities, Day Treatment, Residential Facilities.

### 3. Outlier Handling → Log Transformations

np.log1p() was applied to reduce skewness and stabilize variance.

### 4. Preparing for Modeling

- Target variable: 2016 suicide rate (log-transformed)  
- Features: logged mental health resource variables + encoded Sex variable  
- 80/20 train-test split  
- Consistent random state  

---

## 🤖 Predictive Modeling

### Model 1 — Linear Regression

RMSE: 0.5701  
R²: 0.3420  

This means the model explains 34.2% of global suicide rate variance — a strong result for social data.

---

### Model 2 — Cross Validation (5-fold)

Linear Regression RMSE: 0.573  
Random Forest RMSE: 0.579  

Linear Regression performs slightly better → underlying relationship appears mostly linear.

---

### Model 3 — Lasso Regression (GridSearchCV)

RMSE: 0.570  
R²: 0.341  
No coefficients reduced → all features are relevant.

---

## 📈 Coefficient Analysis

| Feature | Coefficient | Interpretation |
|---------|------------|----------------|
| Psychiatrists_log | +0.076 | Reverse causality: countries invest more where rates are high |
| health_units_log | +0.110 | Same reverse causality pattern |
| outpatient_facilities_log | -0.093 | Only protective feature |
| Sex_Female | -0.572 | Lower female suicide rates |
| Sex_Male | +0.349 | Higher male suicide rates |

---

## 🗺️ Visual Explorations

### Heatmaps
Show moderate correlations between resource variables and positive correlation with suicide rates due to inverse causality.

### Scatter Plots
Psychiatrists vs Suicide Rate, showing upward trend + wide dispersion.

### Choropleth Maps
- Global psychiatrist density  
- Outpatient facilities distribution  

Reveals severe global inequality.

---

## 🔮 Predictive Scenarios

### Scenario A — Increase Outpatient Facilities by 20%

Predicted national suicide rate reduction: **0.60%**

### Scenario B — Gender Differences

Male predicted rate: ~12.0  
Female predicted rate: ~4.2  
→ Men have ≈ 3× higher predicted suicide rate.

---

## 💡 Key Findings

1. Mental health investment correlates with measurable suicide rate differences  
2. Gender is the strongest individual predictor  
3. Outpatient facilities have the strongest protective impact  
4. Specialized resources show reverse causality  
5. Global inequality is severe and measurable  

---

## 📋 Evidence-Based Recommendations

### 1. Invest in community-based mental health services  
Most effective according to the model.

### 2. Gender-specific prevention strategies  
Male suicide risk is consistently higher.

### 3. Proactive resource allocation  
Use predictions to anticipate risk increases.

### 4. Improve global mental health data systems  
Several countries lack reliable reporting.

### 5. Target international aid to high-risk regions  
Especially where <1 psychiatrist per 100,000 people.

---

## 🚀 Running the Project

### Option 1 — Google Colab

Upload → Run → Explore

### Option 2 — Local Execution

git clone https://github.com/malurosbolea-ux/mental-health-suicide-analysis.git  
cd mental-health-suicide-analysis  
python -m venv venv  
source venv/bin/activate  
pip install pandas numpy matplotlib seaborn plotly scikit-learn jupyter  
jupyter notebook Mental_Health_and_Suicide_Rates_by_Malu-2.ipynb  

---
## 📚 Notebook Contents

- Dataset merging  
- Data cleaning and preprocessing  
- Median imputation  
- Log transformations  
- Exploratory data analysis (EDA)  
- Regression modeling  
- Cross-validation  
- Predictive scenario testing  
- Choropleth world maps  
- Policy-oriented insights  

---

## 🎓 Technical Skills Demonstrated

- Advanced Python programming  
- Data wrangling with Pandas  
- Feature engineering  
- Exploratory Data Analysis (EDA)  
- Machine learning modeling  
- Lasso regularization  
- Cross-validation  
- Hyperparameter tuning  
- Geospatial visualizations with Plotly  
- Statistical interpretation  
- Data storytelling and reporting  

---

## 📊 Key Metrics

| Metric | Value |
|--------|--------|
| R² | 0.342 |
| RMSE | 0.570 |
| CV RMSE | 0.573 |
| Countries analyzed | 276 |
| Predicted reduction with 20% facility increase | 0.60% |
| Male/Female suicide ratio | 3:1 |

---

## 🌟 Final Conclusions

- The relationship between mental health resources and suicide rates is **statistically significant and measurable**.  
- **Gender** remains the most powerful predictor of suicide rate differences.  
- **Outpatient facilities** — not specialists — produce the strongest measurable protective impact.  
- Reverse causality is real: countries with higher suicide rates tend to deploy more specialists.  
- Global inequalities in mental health infrastructure are stark and persistent.  
- The model provides actionable insights to support public health strategies.

---

## 📚 References

World Health Organization (WHO)  
National Institute of Mental Health (NIMH)  
Our World in Data  
Kaggle Datasets  
Scientific literature on global mental health systems  

---

## 📧 Contact

**María Luisa Ros Bolea**  
📧 Email: malurosbolea@gmail.com  
💼 LinkedIn: https://www.linkedin.com/in/maría-luisa-ros-bolea-400780160/  
🐙 GitHub: https://github.com/malurosbolea-ux  
🌐 Digital Portfolio: https://marialuisarosboleaportfolio.my.canva.site/porfolio-profesional-mar-a-luisa-ros-bolea-actualizado  

---

## 📄 License

MIT License.  
See LICENSE file for details.

---

## 🙏 Acknowledgments

Thanks to the World Health Organization for providing global mental health data and to the open-source community for the tools that made this project possible.

---

**⭐ If you found this project useful, feel free to star the repository!**


