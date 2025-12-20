# Biomass-to-Glucose Yield Prediction using Machine Learning
Machine learning pipeline to predict glucose yield from lignocellulosic biomass, utilizing experimental data collected from published research on second-generation feedstocks. The project explores CatBoost, XGBoost, and Support Vector Regression algorithms for modeling and analysis.

## Project Overview
Predicts glucose yield based on feedstock properties, pretreatment, and enzymatic hydrolysis conditions.  
Enables rapid, data-driven screening of experimental setups for biofuel production.  
Utilizes curated data and ML modeling to reduce laboratory effort and compare diverse biomass conditions.

## Notebooks Included
### Catboost.ipynb
Trains and validates CatBoost regression for yield prediction, highlighting feature importance.

### XGboost.ipynb
Implements XGBoost regression and investigates key variable effects on glucose yield.

### Support-Vector-Regression.ipynb
Benchmarks a kernel-based SVR model against tree-based methods for the same task.

## Dataset
• 533 data points from 9 research studies  
• 32 columns: feed properties, pretreatment conditions, enzyme features, and glucose yield  
• Covers multiple pretreatment types (AFEX, alkali, acid, ionic liquid, steam explosion, supercritical CO₂)  

## Modeling Workflow
1. Data cleaning (missing values, outlier handling, unit harmonization)  
2. Train-test split (70/30)  
3. Model training (CatBoost, XGBoost, SVR)  
4. Evaluation (R², RMSE, residual analysis)  
5. Feature importance extraction  

## Requirements
pandas
numpy
scikit-learn
xgboost
catboost
matplotlib
seaborn

## Model Performance

| Model     | Train R² | Test R² | Train RMSE % | Test RMSE % | RMSE Gap % | Interpretation                       |
|-----------|----------|---------|--------------|-------------|------------|--------------------------------------|
| CatBoost  | 0.921    | 0.904   | 7.97%        | 8.74%       | 0.77       | Low overfitting, good generalization |
| XGBoost   | 0.938    | 0.900   | 7.03%        | 8.93%       | 1.90       | Slightly more overfitting, good performance |
| SVR       | 0.880    | 0.701   | 9.82%        | 15.45%      | 5.63       | High overfitting, poor generalization |

## Cross-Validation Summary
XGBoost and CatBoost were evaluated using 5-fold cross-validation on the 533-sample biomass-to-glucose dataset (426 train / 107 validation per fold), providing robust generalization beyond a single split.

### Performance Metrics

| Model    | Train RMSE (mean ± std) | Val RMSE (mean ± std) | Overfitting Gap |
|----------|-------------------------|-----------------------|-----------------|
| XGBoost  |	6.91 ± 0.15	           | 10.28 ± 0.93          | 3.36	           |
| CatBoost |	6.87 ± 0.41	           | 9.08 ± 0.56           | 2.22            |

CatBoost shows better generalization with lower validation RMSE and higher fold consistency.

### Key Insights
• Expected real-world RMSE: CatBoost ~9.08, XGBoost ~10.28
• Both show moderate overfitting (2–3 RMSE gap) but remain stable across folds
• Final full-data models are optimistic: XGBoost 7.05 RMSE, CatBoost 6.94 RMSE

## Outliers

| Sample ID | Reference | Feature(s) Highlighted | APE (%) | Notes |
|-----------|-----------|----------------------|---------|-------|
| R3–S4–D1 | Soudham et al. (2015) | No pretreatment | ∞ | Failed hydrolysis – Reed Canary Grass does not produce glucose without pretreatment |
| R7–S1–D2 | Horn et al. (2011) | Steam explosion pretreatment with high severity factor | 492.1 | XGBoost Test – abnormal sugar loss not captured by model |
| R2–S2–D5 | Kang et al. (2025) | Feedstock heterogeneity (aged biomass) | 140 | Both Models (Test) – underperformance not reflected in model inputs |

## Results & Insights
• CatBoost delivered the strongest performance with the highest R² and lowest RMSE among the three models, showing better generalization across diverse biomass conditions.
• Cross-validation results indicate stable performance across data splits, with CatBoost exhibiting lower validation RMSE and reduced overfitting compared to XGBoost.  
• Across all methods, enzyme identity, hydrolysis time, pH, and pretreatment severity consistently emerged as the most influential factors controlling glucose yield.  
• These results demonstrate how ML models can reliably screen process conditions and identify key variables without relying solely on exhaustive laboratory experiments.

## Contributors
- Adithya Ramanakumar
- Nahesware A C
- Dharani Dharan
