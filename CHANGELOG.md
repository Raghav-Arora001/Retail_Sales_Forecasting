# Changelog

All notable changes to this project will be documented in this file.

---

## [Unreleased]

### Added

- Upcoming features

---

## Phase 0 - Project Setup (09 July 2026)

### Added

- Created project structure.
- Configured Python virtual environment.
- Installed project dependencies.
- Initialized Git repository.
- Added README.md.
- Added .gitignore.
- Configured VS Code interpreter.
- Created notebooks and source directories.


## Phase 1 - Dataset Understanding (09 July 2026)

### Added
- Completed Dataset Understanding notebook.
- Explored Rossmann sales and store datasets.
- Documented business problem and dataset structure.
- Analyzed all features and their business significance.
- Verified merge key (`Store`) between train and store datasets.

### Investigated
- Checked dataset dimensions and data types.
- Examined summary statistics.
- Identified missing values and duplicate records.
- Verified structural missing values in Promo2-related features.
- Investigated competition-related missing values.

### Decisions
- Exclude closed-store records during model training.
- Exclude `Customers` from modeling due to potential data leakage.
- Preserve raw datasets; perform transformations only in preprocessing.

# Phase 2 — Data Cleaning

**Status:** Completed

## Added

* Merged `train.csv` and `store.csv` using a left join on the `Store` key.
* Converted the `Date` column to `datetime64[ns]`.
* Created a comprehensive missing value audit with counts and percentages.
* Created `train_open_df` containing only open-store observations.
* Saved processed datasets:

  * `data/processed/merged_data.csv`
  * `data/processed/train_open.csv`

## Changed

* Established a structured preprocessing workflow following an industry-inspired data science pipeline.
* Introduced validation checkpoints after each major preprocessing step.
* Preserved both the complete merged dataset and the modeling dataset for different downstream purposes.

## Validated

* Verified merge integrity by confirming row counts and successful store matching.
* Confirmed `Date` conversion to `datetime64[ns]`.
* Verified that Promo2-related missing values are structural rather than data quality issues.
* Investigated competition-related missing values and documented observations.
* Confirmed that the open-store dataset contains only records where `Open = 1`.
* Verified that no duplicate rows were introduced during preprocessing.

## Decisions

* Deferred imputation of competition-related missing values until feature engineering.
* Preserved structural missing values in Promo2-related columns.
* Excluded closed-store records from the modeling dataset to avoid shortcut learning.
* Retained the complete merged dataset for exploratory analysis and business reporting.
* Saved processed datasets to improve reproducibility and eliminate redundant preprocessing in subsequent notebooks.

# Phase 3 - Exploratory Data Analysis (11 July 2026)

## Added
- Performed comprehensive exploratory data analysis on the Rossmann dataset.
- Analyzed sales distribution, seasonality, promotions, holidays, store characteristics, and competition.
- Investigated customer behavior using exploratory customer metrics.
- Documented key business insights and feature engineering roadmap.

## Investigated
- Sales trends across time and weekdays.
- Impact of promotions, holidays, store types, assortment, and competition on sales.
- Customer traffic and revenue per customer for key business drivers.
- Competition timeline and Promo2-related features.
- Structural missing values and unusual competition records.

## Decisions
- Retain customer-based analyses for business understanding only.
- Exclude `Customers` from predictive modeling to prevent data leakage.
- Engineer competition age and promotion duration features during preprocessing.
- Handle structural missing values during feature engineering.

## Phase 4 - Feature Engineering

### Added

- Engineered calendar-based features from the Date column.
- Created CompetitionAgeMonths from competition opening information.
- Added CompetitionInfoAvailable indicator.
- Engineered Promo2AgeMonths using Promo2 start dates.
- Created IsPromoMonth using PromoInterval.
- Added helper columns to simplify feature engineering.

### Validation

- Verified engineered feature distributions.
- Checked missing values and data types.
- Investigated CompetitionAgeMonths outlier originating from the source dataset.
- Applied business rules for duration features and sentinel values.

### Documentation

- Documented feature engineering decisions.
- Recorded business assumptions and validation process.

## Phase 5 — Data Preprocessing

### Added
- Chronological train-validation split.
- Reusable preprocessing pipeline using ColumnTransformer.
- OneHotEncoder-based categorical encoding.
- Model-ready datasets for training and validation.

### Changed
- Removed temporary helper columns.
- Removed accidental PromoAgeMonths feature.
- Dropped Date after temporal split.
- Replaced missing CompetitionDistance values with sentinel value (-1).

### Notes
Completed preprocessing workflow and prepared the project for model development.

