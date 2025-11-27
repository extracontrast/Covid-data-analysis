# Covid-data-analysis
Data science project

Link for downloading dataset: https://github.com/owid/covid-19-data/blob/master/public/data/README.md

This project is a detailed COVID-19 data analysis conducted in a Jupyter Notebook, encompassing the full data science workflow: sophisticated data cleaning, extensive exploratory data analysis (EDA), rigorous hypothesis testing, and optimized machine learning modeling to understand infection rate dynamics [CH].

📊 Project Goals
The core objectives of this analysis were to:
1. Apply context-specific data manipulation techniques to clean a massive, global COVID-19 dataset 
2. Statistically validate specific socio-economic and health factors against pandemic impact using formal hypothesis testing (Z-tests, t-tests, Chi-square) 
3. Develop and optimize a predictive framework for case rates by tackling critical challenges like multicollinearity and class imbalance

--------------------------------------------------------------------------------

🛠️ Technical Implementation and Methodology
1. Data Acquisition and Preprocessing
The analysis began with a comprehensive COVID-19 dataset containing 136,250 entries across 67 columns.
Data Cleaning and Imputation Strategy
A multi-layered approach was necessary to handle the diversity of missing data (NaN values):
• Static Feature Imputation: Numerical country metrics like 'population', 'median_age', and 'gdp_per_capita' were imputed using the mean. The categorical column 'continent' was imputed using the mode.
• Time Series Imputation: Time-dependent columns, including 'total_cases' and daily metric totals, utilized forward-fill (ffill) followed by backward-fill (bfill) to maintain temporal continuity.
• Contextual Zero Imputation: Vaccination metrics (e.g., 'people_vaccinated') were deliberately set to zero (0), based on the assumption that "no data means vaccination didn't start yet".
• Deduplication: The process identified and removed 19,166 duplicate rows, resulting in a cleaned dataset size of 112,888 entries.

-------------------------------------------------------------------------------------

2. Exploratory Data Analysis (EDA)
Visualization was used extensively to uncover temporal trends and geographical disparities:

Continent-Wise Time Series:
Line graphs tracking 'new cases' trends for continents (Africa, Asia, Europe, North America, South America), revealing distinct epidemic wave patterns
<img width="483" height="293" alt="image" src="https://github.com/user-attachments/assets/a973b5a4-611b-452c-a0b4-b0cf07ec359e" />

Continental Distribution:
Plots comparing the distribution of 'new cases' across continents, highlighting significant variation (e.g., Africa shows high spread/outliers)
<img width="588" height="477" alt="image" src="https://github.com/user-attachments/assets/3bb19675-9917-43a1-b1d5-e62f7fdf1f6d" />

Comparative Analysis:
Side-by-side plots comparing key metrics (total_cases, 'people_fully_vaccinated') between countries like India, USA, and Brazil
<img width="601" height="291" alt="image" src="https://github.com/user-attachments/assets/4709a56a-d76b-417f-953b-cfa8f0f5e654" />

Correlation Jointplots:
Kernel Density Estimation (KDE) jointplots visualizing the density relationship between 'total_cases_per_million' and factors like 'handwashing_facilities', 'population_density', and 'life_expectancy'
<img width="475" height="420" alt="image" src="https://github.com/user-attachments/assets/495750e6-bbce-443d-b630-61aa673d76db" />

--------------------------------------------------------------------------------------------------

3. Statistical Hypothesis Testing
A core component of the project involved testing eight formal hypotheses regarding the average and variance of 'new_cases_per_million' against various country metrics:

example:
Hypothesis Tested: Average cases per million in countries with GDP > $20,000 is greater than the population average
Test Used: Z-Test
Outcome: Null Hypothesis Rejected.

Hypothesis Tested: Average cases per million in countries with Life Expectancy < 70 is greater than the population average
Test Used: P-value Method
Outcome: Null Hypothesis Rejected.

Hypothesis Tested: The variance of total cases per million in countries with Population Density (0-1000) is less than the population average
Test Used: Chi-Square Test
Outcome: Null Hypothesis Rejected.

--------------------------------------------------------------------------------------------------------
4. Machine Learning & Optimization
The machine learning pipeline focused on regression modeling to predict infection rates, emphasizing feature engineering and data balancing.
Model Performance Optimization

1. Initial Models (Before Optimization):
    ◦ Linear Regressor Score: 0.913
    ◦ KNN Regressor Score: 0.998

2. Feature Selection: To address multicollinearity (as shown by the correlation heatmap), a function was implemented to remove features correlated above a threshold of 0.7. This step removed 11 highly correlated features. Mutual Information was also calculated to rank feature importance (e.g., 'total_cases_per_million' and 'handwashing_facilities').
<img width="650" height="785" alt="image" src="https://github.com/user-attachments/assets/7ebffdec-44ac-415b-b8ea-80f1c3f8f37a" />

4. Imbalance Handling: Due to the highly skewed distribution of the target variable, the dataset was balanced using the RandomUnderSampler technique from the imblearn library.

5. Final Models (After Optimization):
    ◦ Linear Regressor Score: 0.953 (A significant improvement from 0.913)
    ◦ KNN Regressor Score: 0.998



6. Time Series Analysis
A dedicated time series analysis was performed on the aggregated global 'new cases' data.
• Decomposition: The time series was decomposed into its trend, seasonal, and residual components using an 'additive' model.
• Stationarity Testing: The series was tested for stationarity using the Dickey-Fuller test, along with visualization of the rolling mean and standard deviation.
• Autocorrelation: An autocorrelation plot was generated to analyze temporal dependencies.

--------------------------------------------------------------------------------
💻 Technical Stack
This project was built entirely within a Jupyter Notebook environment utilizing Python and the following key libraries:
• Data Manipulation: pandas, numpy, collections
• Machine Learning/Preprocessing: sklearn (StandardScaler, LabelEncoder, LinearRegression, KNeighborsRegressor, train_test_split, Mutual Information)
• Statistical Analysis: scipy.stats
• Imbalance Handling: imblearn (RandomUnderSampler)
• Time Series: statsmodels.tsa (for decomposition and Dickey-Fuller Test)
• Visualization: matplotlib.pyplot, seaborn

--------------------------------------------------------------------------------
🏃 Getting Started
The core analysis notebook is located here: covid_data_analysis.ipynb.
1. Clone this repository: git clone https://github.com/extracontrast/Covid-data-analysis.git
2. Install required libraries (ensure imblearn and statsmodels are installed in addition to the standard stack).
3. Open covid_data_analysis.ipynb in a Jupyter environment to replicate the entire analysis pipeline.





