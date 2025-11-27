# COVID-19 Data Analysis

This repository contains a complete end-to-end data science analysis of the OWID COVID-19 dataset.  
The project covers data cleaning, exploratory data analysis (EDA), statistical hypothesis testing, machine learning modeling, and time-series analysis.

Dataset Source: https://github.com/owid/covid-19-data/tree/master/public/data

---

## Project Overview

This project aims to:
1. Clean and preprocess a large-scale, heterogeneous global COVID-19 dataset.
2. Explore and visualize key patterns across countries and continents.
3. Conduct formal statistical hypothesis testing.
4. Build and optimize machine learning models for infection-rate prediction.
5. Perform global time-series analysis on new COVID-19 cases.

---

## 1. Data Acquisition & Preprocessing

The raw dataset contained **136,250 rows** and **67 columns**.

### Cleaning Steps:
- **Static Imputation**  
  - Numerical columns (population, median_age, gdp_per_capita): mean  
  - Categorical columns (continent): mode  
- **Time-Series Imputation**  
  - Daily metrics (total_cases, new_cases): forward-fill → backward-fill  
- **Context-Based Zero Imputation**  
  - Vaccination metrics: set to 0 where missing (vaccination not started)  
- **Duplicate Removal**  
  - Removed **19,166 duplicate rows** → Final dataset: **112,888 rows**

---

## 2. Exploratory Data Analysis (EDA)

Key visual analyses performed:
- **Continent-wise new case trends** (Africa, Asia, Europe, North America, South America)
- **Distribution of new cases across continents**
- **Country-level comparisons** (India, USA, Brazil)
- **Correlation jointplots** showing density relationships between:
  - total_cases_per_million  
  - handwashing_facilities  
  - population_density  
  - life_expectancy  

All visual outputs are included in the notebook.

---

## 3. Statistical Hypothesis Testing

Eight hypotheses were tested using Z-tests, t-tests, p-value methods, and Chi-square tests.

### Examples:
- Countries with GDP > $20,000 have higher average cases per million  
  - **Test:** Z-Test  
  - **Result:** Null hypothesis rejected  
- Countries with life expectancy < 70 have higher average infection rates  
  - **Test:** P-value method  
  - **Result:** Null hypothesis rejected  
- Variance of cases per million in low-density countries (0–1000) is lower than global variance  
  - **Test:** Chi-square  
  - **Result:** Null hypothesis rejected  

---

## 4. Machine Learning & Model Optimization

Regression models were trained to predict infection rates.

### Initial Model Performance:
- **Linear Regression:** 0.913  
- **KNN Regressor:** 0.998  

### Optimization Steps:
- **Multicollinearity Reduction**  
  - Removed features with correlation > 0.7 (11 columns removed)  
- **Feature Importance**  
  - Calculated using Mutual Information  
- **Imbalanced Target Handling**  
  - Applied RandomUnderSampler from imblearn  

### Final Model Scores:
- **Linear Regression:** 0.953  
- **KNN Regressor:** 0.998  

---

## 5. Time Series Analysis

Performed on global aggregated "new cases" data:
- **Decomposition:** Trend, seasonal, and residual components  
- **Stationarity Testing:** Dickey-Fuller test, rolling mean, rolling std  
- **Autocorrelation:** ACF plot to examine temporal dependency  

---

## Technical Stack

- **Languages:** Python  
- **Environment:** Jupyter Notebook  

### Libraries Used:
- pandas, numpy  
- scikit-learn  
- scipy.stats  
- imblearn  
- statsmodels  
- matplotlib, seaborn  

---

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/extracontrast/Covid-data-analysis.git
```

### 2. Install Dependencies
Make sure to install:
- pandas  
- numpy  
- matplotlib  
- seaborn  
- scikit-learn  
- imblearn  
- statsmodels  

### 3. Open the Notebook
```bash
jupyter notebook covid_data_analysis.ipynb
```

---

## Project Structure
```
Covid-data-analysis/
│
├── covid_data_analysis.ipynb   # Main analysis notebook
├── README.md                   # Project documentation
```
---

This README summarizes the complete analysis as implemented in the notebook.
