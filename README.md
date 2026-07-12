# Retail Sales Forecasting & Analytics Platform

An end-to-end Machine Learning and Business Analytics project using the Rossmann Store Sales dataset.

## Project Objective

Build a complete retail sales forecasting pipeline using classical machine learning techniques and derive actionable business insights through exploratory data analysis and interactive dashboards.

## Project Progress

* ✅ Phase 0 – Project Setup
* ✅ Phase 1 – Dataset Understanding
* ✅ Phase 2 – Data Preparation
* ✅ Phase 3 – Exploratory Data Analysis
* ✅ Phase 4 – Feature Engineering
* ✅ Phase 5 – Data Preprocessing
* ✅ Phase 6 – Model Development
* ⏳ Phase 7 – Model Evaluation
* ⏳ Phase 8 – Dashboard & Deployment

## Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* XGBoost
* Plotly
* Power BI
* Git
* GitHub

## Project Status

### ✅ Phase 0 — Project Setup

* Project structure created
* Virtual environment configured
* Dependencies installed
* Git repository initialized
* VS Code development environment configured

### ✅ Phase 1 — Dataset Understanding

* Business problem analysis
* Dataset exploration
* Feature understanding
* Data quality assessment
* Missing value analysis
* Duplicate check
* Modeling decisions documented

### ✅ Phase 2 — Data Preparation

* Dataset merging
* Datetime conversion
* Missing value handling
* Data cleaning
* Closed-store filtering

### ✅ Phase 3 — Exploratory Data Analysis (EDA)

* Sales distribution analysis
* Store-level analysis
* Promotion analysis
* Holiday impact analysis
* Business hypothesis generation
* Customer behaviour insights

### ✅ Phase 4 — Feature Engineering

* Calendar feature extraction
* Competition feature engineering
* Promotion feature engineering
* Business-driven duration features
* Feature validation
* Feature engineering documentation

### ✅ Phase 5 — Data Preprocessing

* Removed temporary helper columns from feature engineering.
* Created a chronological train-validation split to prevent temporal leakage.
* Handled remaining missing values using sentinel-value imputation.
* Designed a preprocessing strategy based on feature semantics.
* Applied One-Hot Encoding to nominal categorical variables.
* Built a reusable preprocessing workflow using `ColumnTransformer`.
* Generated model-ready training and validation datasets.

### ✅ Phase 6 — Model Development

* Established a forecasting baseline using a Dummy Regressor.
* Developed Linear Regression, Random Forest, and XGBoost forecasting models.
* Performed hyperparameter experimentation to optimize model generalization.
* Compared models using MAE, RMSE, and R² on a chronological validation set.
* Selected XGBoost as the final forecasting model, achieving **R² = 0.729** and reducing RMSE by approximately **48%** compared to the baseline.
* Saved the trained preprocessing pipeline and final forecasting model for downstream evaluation and dashboard integration.

## Repository Structure

```text
Retail-Sales-Forecasting/
│
├── data/
│   ├── raw/
│   ├── processed/
│
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_preparation.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   ├── 04_feature_engineering.ipynb
│   ├── 05_data_preprocessing.ipynb
│   ├── 06_model_development.ipynb
│
├── src/
├── reports/
├── models/
│   ├── preprocessor.joblib
│   ├── xgboost_model.joblib
│
├── requirements.txt
├── README.md
├── CHANGELOG.md
└── .gitignore
```
