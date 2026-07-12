# Phase 0 & Phase 1 Command and Code Reference

**Project:** Retail Sales Forecasting & Analytics Platform

---

# Phase 0 — Project Setup

## Create Virtual Environment

```bash
python -m venv .venv
```

### Purpose

Creates an isolated Python environment inside the project folder.

### Why?

* Prevent package conflicts
* Reproducible environment
* Project-specific dependencies

---

## Activate Virtual Environment (PowerShell)

```powershell
.\.venv\Scripts\Activate.ps1
```

### Purpose

Activates the virtual environment.

After activation:

```text
(.venv)
```

appears before the terminal prompt.

---

## Verify Python Version

```bash
python --version
```

### Purpose

Checks which Python interpreter is currently active.

---

## Verify pip Version

```bash
pip --version
```

### Purpose

Ensures pip belongs to the activated virtual environment.

---

## Install Required Packages

```bash
pip install pandas numpy matplotlib scikit-learn jupyter openpyxl
```

### Purpose

Installs all required libraries.

---

## Why Each Package?

### pandas

Data manipulation.

---

### numpy

Numerical computation.

---

### matplotlib

Visualization.

---

### scikit-learn

Machine Learning algorithms.

---

### jupyter

Notebook environment.

---

### openpyxl

Read/write Excel (.xlsx) files using Pandas.

---

## Generate requirements.txt

```bash
pip freeze > requirements.txt
```

### Purpose

Exports every installed package and version.

Used for reproducing the environment.

---

## Verify Git

```bash
git --version
```

### Purpose

Checks Git installation.

---

## Initialize Git Repository

```bash
git init
```

### Purpose

Creates a local Git repository.

---

## Check Git Status

```bash
git status
```

### Purpose

Shows:

* Modified files
* Staged files
* Untracked files

One of the most frequently used Git commands.

---

## Stage All Files

```bash
git add .
```

### Purpose

Adds every modified file to the staging area.

---

## Stage Specific File

```bash
git add README.md
```

### Purpose

Stages only one file.

---

## Commit Changes

```bash
git commit -m "Commit message"
```

### Purpose

Creates a snapshot of the project.

Example:

```bash
git commit -m "Complete Phase 1: Dataset understanding"
```

---

# VS Code

## Select Python Interpreter

Command Palette

```
Python: Select Interpreter
```

Choose:

```
.venv
```

Purpose:

Ensures VS Code uses the project's Python environment.

---

## Select Notebook Kernel

Top-right of notebook

Choose

```
Python Environments

↓

.venv
```

Purpose

Runs notebook cells inside the virtual environment.

---

# Phase 1 — Dataset Understanding

## Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

Purpose:

Import required libraries.

---

## Read CSV Files

```python
train_df = pd.read_csv("../data/raw/train.csv")

store_df = pd.read_csv("../data/raw/store.csv")
```

Purpose

Load datasets.

---

## Handle Mixed Dtypes

```python
pd.read_csv(..., low_memory=False)
```

Purpose

Suppress mixed dtype warnings during import.

---

## Display Shape

```python
train_df.shape
```

Returns

```
(rows, columns)
```

---

## Display First Rows

```python
train_df.head()
```

Shows first five rows.

---

## Display Last Rows

```python
train_df.tail()
```

Shows last five rows.

---

## Display Column Names

```python
train_df.columns
```

Returns all column names.

---

## Dataset Information

```python
train_df.info()
```

Returns

* Data types
* Missing values
* Memory usage

---

## Summary Statistics

```python
train_df.describe()
```

Returns

* Mean
* Median (50%)
* Std
* Min
* Max
* Quartiles

---

## Describe Including Objects

```python
train_df.describe(include="all")
```

Returns statistics for categorical columns as well.

---

## Missing Values

```python
train_df.isnull().sum()
```

Returns missing value count for every column.

---

## Duplicate Rows

```python
train_df.duplicated().sum()
```

Returns number of duplicate rows.

---

## Unique Values

```python
train_df["StateHoliday"].unique()
```

Returns unique values.

Example

```
0
a
b
c
```

---

## Value Counts

```python
train_df["Open"].value_counts()
```

Returns frequency of every category.

---

## Number of Unique Stores

```python
train_df["Store"].nunique()
```

Purpose

Counts unique stores.

---

## Group By

Used to verify Promo2 hypothesis.

```python
store_df.groupby("Promo2")[[
    "Promo2SinceWeek",
    "Promo2SinceYear",
    "PromoInterval"
]].count()
```

Purpose

Checks whether missing values depend on Promo2.

---

## Verify Merge Key

```python
set(train_df["Store"]) == set(store_df["Store"])
```

Purpose

Ensures both datasets contain identical store IDs.

Returns

```
True
```

---

## List Current Directory

```python
import os

os.listdir()
```

Purpose

Shows current working directory contents.

Useful for debugging path issues.

---

# Display All Columns

```python
pd.set_option("display.max_columns", None)
```

Purpose

Prevent Pandas from truncating columns.

---

## Display Wider Tables

```python
pd.set_option("display.width", None)
```

Purpose

Uses available notebook width.

---

## Display Longer Text

```python
pd.set_option("display.max_colwidth", None)
```

Purpose

Prevent long strings from being truncated.

---

# Git Commands Used

```bash
git init
```

Initialize repository.

---

```bash
git status
```

Check repository state.

---

```bash
git add .
```

Stage changes.

---

```bash
git commit -m "message"
```

Commit staged files.

---

# Important Concepts Learned

* Virtual Environments
* requirements.txt
* Git basics
* Relative file paths
* Pandas DataFrames
* Data types
* Missing values
* Duplicate detection
* Summary statistics
* Target leakage
* Structural missing values
* Merge key validation
* One-Hot Encoding decision
* Business understanding before preprocessing
* Industry-style project workflow

---

# Common Debugging Steps Used

### Verify current directory

```python
import os
os.getcwd()
```

---

### List directory contents

```python
os.listdir()
```

---

### Check notebook location

Used to diagnose incorrect nested notebook folders.

---

### Save notebook before Git

Always save before committing.

---

### Check Git status

```bash
git status
```

before every commit.

---

# Commands We Will Use Soon (Phase 2 Preview)

```python
pd.merge()

pd.to_datetime()

fillna()

drop()

astype()

loc[]

copy()

to_csv()
```

These will be introduced and explained in the next phase before implementation.

That's a great idea. Since you already have **Phase 0** (project setup) and **Phase 1** (dataset understanding) documentation, this list should focus **only on the new functions, methods, and coding patterns introduced in Phases 2 and 3**, avoiding repetition unless the usage or purpose changed.

This is the kind of reference that becomes invaluable before interviews.

---

# Phase 2 & Phase 3 — Code Reference

## 1. Data Filtering

### Filter open stores

```python
train_open_df = train_df[train_df["Open"] == 1].copy()
```

**Purpose**

* Removes closed-store records.
* Prevents zero sales from biasing analysis.
* `.copy()` avoids chained assignment problems.

---

## 2. Shape Inspection

```python
train_open_df.shape
```

Returns

```
(rows, columns)
```

Used to verify filtering.

---

## 3. Summary Statistics

```python
train_open_df["Sales"].describe()
```

Returns

* count
* mean
* std
* min
* quartiles
* max

Used extensively throughout EDA.

---

## 4. Percentiles

```python
train_open_df["CompetitionDistance"].describe(
    percentiles=[0.90,0.95,0.99]
)
```

Purpose

Inspect extreme values.

Useful for

* skewness
* outlier detection
* deciding transformations

---

# 5. Histogram (Plotly)

```python
px.histogram()
```

Purpose

Visualize numerical feature distributions.

Used for

* Sales
* CompetitionDistance

Important parameters

```python
x=
nbins=
title=
```

---

# 6. Histogram (Matplotlib)

```python
plt.hist()
```

Static histogram.

Kept as backup.

---

# 7. Boxplot

```python
px.box()
```

Purpose

Detect

* outliers
* spread
* skewness

---

# 8. Line Plot

```python
px.line()
```

Purpose

Time-series visualization.

Used for

Daily sales trend.

---

# 9. Bar Plot

```python
px.bar()
```

Purpose

Compare grouped statistics.

Used for

* Promo
* Holidays
* StoreType
* Assortment
* Competition bins

Useful arguments

```python
text_auto=".0f"

hover_data=[...]

color=
```

---

# 10. GroupBy

```python
.groupby()
```

Most frequently used operation.

Purpose

Aggregate rows belonging to the same category.

Example

```python
df.groupby("Promo")
```

---

# 11. Multiple Aggregations

```python
.agg(
    Average_Sales=("Sales","mean"),
    Observation_Count=("Sales","count")
)
```

Purpose

Compute multiple statistics in one operation.

Introduced named aggregation syntax.

---

# 12. Reset Index

```python
.reset_index()
```

Purpose

Convert grouped index back into columns.

Useful before plotting.

---

# 13. GroupBy with as_index=False

```python
.groupby(
    ...,
    as_index=False
)
```

Purpose

Avoid needing

```python
.reset_index()
```

after grouping.

Cleaner syntax.

---

# 14. Value Counts

```python
.value_counts()
```

Purpose

Frequency of unique values.

Used for

* Competition year
* Competition month
* PromoInterval

---

## Sorted frequencies

```python
.value_counts().sort_index()
```

Keeps numeric order.

---

# 15. Mapping Values

```python
.map()
```

Purpose

Replace encoded values with readable labels.

Example

```python
mapping={
    0:"No Promo",
    1:"Promo"
}

df["Promo"]=df["Promo"].map(mapping)
```

---

# 16. Dictionary Mapping

Created mappings for

* Promo
* Promo2
* StateHoliday
* SchoolHoliday
* StoreType
* Assortment

Purpose

Improve plot readability.

---

# 17. Binning

```python
pd.cut()
```

Purpose

Convert continuous variables into ranges.

Used for

CompetitionDistance.

Example

```
<1km
1–2.5km
2.5–5km
...
```

---

# 18. Named Bins

```python
labels=
```

Purpose

Readable interval names.

---

# 19. Mean Customer Count

```python
Average_Customers=("Customers","mean")
```

Purpose

Business analysis only.

Not used for modeling.

---

# 20. Revenue Per Customer

Created manually.

```python
summary["sales_per_customer"]=(
    summary["Average_Sales"]/
    summary["Average_Customers"]
)
```

Purpose

Understand

Sales

=

Customers

×

Revenue per customer

One of the most valuable analyses in Phase 3.

---

# 21. Missing Values

```python
.isna().sum()
```

Purpose

Count missing values.

Used on

Competition

PromoInterval

Timeline features.

---

# 22. Column Selection

```python
df[
    [
        "A",
        "B"
    ]
]
```

Purpose

Operate on multiple columns.

---

# 23. Boolean Filtering

```python
df[df["Promo"]==1]
```

Purpose

Subset rows.

---

# 24. loc

```python
df.loc[
    condition,
    columns
]
```

Purpose

Conditional row and column selection.

Used

Investigating

Store 815

Competition year

1900

---

# 25. nunique()

```python
.nunique()
```

Purpose

Count distinct values.

Used

Checking

Store 815 uniqueness.

---

# 26. unique()

```python
.unique()
```

Purpose

Return distinct values.

Useful

Verifying

unexpected categories.

---

# 27. Hover Data

```python
hover_data=[]
```

Plotly feature.

Displays additional information on hover.

---

# 28. text_auto

```python
text_auto=".0f"
```

Automatically prints values above bars.

---

# 29. update_layout()

```python
fig.update_layout()
```

Used for

* titles
* axis labels
* formatting

---

# 30. show()

```python
fig.show()
```

Render interactive Plotly figure.

---

# 31. Copy

```python
.copy()
```

Purpose

Avoid chained assignment warnings.

Safe dataframe manipulation.

---

# 32. Business Analysis Pattern (Most Important)

This became the standard workflow throughout Phase 3.

```
Business Question

↓

Hypothesis

↓

Grouping

↓

Visualization

↓

Observation

↓

Business Interpretation

↓

Decision
```

This wasn't just code—it became the analytical framework for every feature.

---

# 33. Customer Analysis Pattern (Introduced in Phase 3)

For important business features:

```
Average Sales

↓

Average Customers

↓

Revenue per Customer

↓

Explain WHY sales differ
```

This transformed simple EDA into explanatory analysis.

---

# 34. Structural Missing Value Identification

New concept introduced:

Not all missing values are errors.

Examples:

* Competition features
* PromoInterval
* Promo2 timeline

Meaning

Missing values themselves carry business information.

---

# 35. Hypothesis Validation Workflow

Another important methodology introduced.

```
Initial hypothesis

↓

EDA

↓

Customer analysis

↓

Accept

or

Reject

↓

Explain why
```

Examples

❌ Type B premium hypothesis

❌ Extra assortment hypothesis

❌ Promo2 hypothesis

---

# ⭐ Most Important New Concepts Learned

If I had to summarize Phases 2 and 3 into the most valuable takeaways, they would be:

1. Filtering data appropriately before analysis (`Open == 1`).
2. Performing hypothesis-driven EDA instead of descriptive EDA.
3. Using `groupby()` with named aggregations for business analysis.
4. Leveraging Plotly for interactive visualizations.
5. Distinguishing **customer traffic** from **revenue per customer** to explain sales differences.
6. Recognizing and correctly handling **structural missing values**.
7. Investigating unexpected results rather than accepting initial assumptions.
8. Using EDA to **motivate feature engineering**, ensuring derived features have clear business meaning.

---


# Phase 4 Code Reference — Feature Engineering

This document contains the important Python, Pandas functions, methods, and programming concepts used during Phase 4 — Feature Engineering.

The objective is not only to remember syntax but to understand:

* Why the function was used.
* What problem it solved.
* How it contributed to feature creation.
* Common mistakes and interview considerations.

---

# 1. Datetime Feature Extraction

## `.dt` Datetime Accessor

### Purpose

The `.dt` accessor allows extraction of individual components from a Pandas datetime column.

In this project, it was used to convert raw transaction dates into meaningful calendar features.

Example:

```python
train_open_df["Year"] = train_open_df["Date"].dt.year
```

---

### Features Created Using `.dt`

Created:

* Year
* Month
* Day
* Quarter
* WeekOfYear
* IsMonthStart
* IsMonthEnd
* IsWeekend

---

# `.dt.year`

## Purpose

Extracts the year component from a datetime column.

Example:

```python
2015-07-01 → 2015
```

Used for:

```python
Year
```

---

## Business Reason

Year allows the model to learn long-term yearly trends.

---

# `.dt.month`

## Purpose

Extracts month number.

Example:

```python
2015-07-01 → 7
```

Used for:

```python
Month
```

---

## Business Reason

Retail sales often have monthly seasonality due to:

* Holidays
* Weather
* Shopping cycles

---

# `.dt.day`

## Purpose

Extracts day of month.

Example:

```python
2015-07-15 → 15
```

Used for:

```python
Day
```

---

# `.dt.quarter`

## Purpose

Returns quarter of year.

Output:

```
1,2,3,4
```

Example:

January → Q1

---

## Business Reason

Captures broader seasonal periods.

---

# `.dt.isocalendar()`

## Purpose

Returns ISO calendar information.

Example:

```python
df["Date"].dt.isocalendar()
```

Returns:

* ISO year
* ISO week
* ISO weekday

---

Used:

```python
.dt.isocalendar().week
```

to create:

```python
WeekOfYear
```

---

## Why ISO Week Was Used

Normal calendar weeks can vary around year boundaries.

ISO weeks provide consistent week numbering.

---

# `.dt.is_month_start`

## Purpose

Checks whether date is the first day of a month.

Returns:

Boolean

Example:

```
True
False
```

Used:

```python
IsMonthStart
```

---

# `.dt.is_month_end`

## Purpose

Checks whether date is the last day of a month.

Used:

```python
IsMonthEnd
```

---

# `.dt.dayofweek`

## Purpose

Returns weekday number.

Mapping:

```
Monday = 0
Tuesday = 1
...
Sunday = 6
```

---

Used with:

```python
.isin([5,6])
```

to identify weekends.

---

# 2. Boolean Feature Creation

# `.isin()`

## Purpose

Checks whether values belong to a collection.

Example:

```python
dayofweek.isin([5,6])
```

Output:

```
True
False
```

---

## Project Usage

Used to create:

```python
IsWeekend
```

Logic:

```
Saturday OR Sunday → True
Other days → False
```

---

# `.notna()`

## Purpose

Checks whether values are not missing.

Example:

```python
df["CompetitionDistance"].notna()
```

---

## Project Usage

Created:

```python
CompetitionInfoAvailable
```

Logic:

```
Competition information exists → True
Missing → False
```

---

# 3. Datetime Construction

# `pd.to_datetime()`

## Purpose

Converts strings or numbers into Pandas datetime objects.

---

## Project Usage

Created:

* CompetitionOpenDate
* Promo2StartDate

Example:

```python
pd.to_datetime(date_string)
```

---

## Common Mistake

Incorrect date parsing can silently create incorrect features.

Always validate:

```python
df["date"].min()
df["date"].max()
```

---

# ISO Date Formatting

Used when creating Promo2 start dates.

Format:

```python
"%G-W%V-%u"
```

Meaning:

| Code | Meaning     |
| ---- | ----------- |
| %G   | ISO year    |
| %V   | ISO week    |
| %u   | ISO weekday |

Example:

```
2015-W10-1
```

means:

Monday of ISO week 10 in 2015.

---

# 4. String Operations

# `.str.zfill()`

## Purpose

Adds leading zeros to strings.

Example:

Before:

```
5
```

After:

```
05
```

---

## Project Usage

Used while constructing ISO week dates.

---

# `.dt.strftime()`

## Purpose

Formats datetime values into strings.

Example:

```python
df["Date"].dt.strftime("%b")
```

Output:

```
Jan
Feb
Mar
```

---

## Project Usage

Created:

```python
TransactionMonth
```

Used for comparing:

* Transaction month
* PromoInterval

---

# 5. Conditional Assignment

# `.loc[]`

## Purpose

Allows selection and modification of specific rows and columns.

Syntax:

```python
df.loc[row_condition, column]
```

---

## Project Usage

Used for:

* Applying business rules
* Assigning sentinel values
* Updating engineered features

Example:

```python
df.loc[df["CompetitionAgeMonths"] < 0,
       "CompetitionAgeMonths"] = 0
```

---

# Common Mistake

Avoid chained indexing:

Incorrect:

```python
df[df["A"]>0]["B"]=value
```

Correct:

```python
df.loc[df["A"]>0,"B"]=value
```

---

# `.mask()`

## Purpose

Conditionally replaces values.

Example:

```python
series.mask(condition, replacement)
```

---

## Project Usage

Used for:

Negative duration correction.

Example:

Invalid:

```
CompetitionAgeMonths = -50
```

Converted to:

```
0
```

---

# 6. Row-wise Operations

# `.apply()`

## Purpose

Applies a function along rows or columns.

---

## Project Usage

Used to create:

```python
IsPromoMonth
```

because each row required comparison between:

* Store promotion schedule
* Transaction month

---

## Important Consideration

`.apply()` is slower than vectorized operations.

It should not be used unnecessarily.

---

# `lambda`

## Purpose

Creates small anonymous functions.

Example:

```python
lambda x: x+1
```

---

## Project Usage

Used inside `.apply()`.

---

# `pd.notna()`

## Purpose

Checks whether a value is not missing.

Used inside lambda logic.

---

# 7. Validation Functions

Feature engineering requires validation before model training.

---

# `.describe()`

## Purpose

Generates statistical summary.

Checks:

* Mean
* Standard deviation
* Min
* Max
* Percentiles

---

## Project Usage

Used to validate:

* CompetitionAgeMonths
* Promo2AgeMonths

---

# `.value_counts()`

## Purpose

Counts unique values.

Example:

```python
df["IsPromoMonth"].value_counts()
```

---

Used to validate boolean features.

---

# `.info()`

## Purpose

Displays:

* Data types
* Missing values
* Memory usage

---

Used after feature creation to verify:

* Correct dtypes
* No unexpected missing values

---

# `.isna().sum()`

## Purpose

Counts missing values column-wise.

Example:

```python
df.isna().sum()
```

---

Used for feature validation.

---

# `.nlargest()`

## Purpose

Returns largest values.

Used for:

* Investigating outliers
* Checking abnormal durations

---

# `.nsmallest()`

## Purpose

Returns smallest values.

Used for:

* Finding negative values
* Debugging incorrect calculations

---

# 8. Important Programming Concepts Learned

## Feature Engineering

Transforming raw data into meaningful model inputs.

---

## Temporal Features

Extracting time-related patterns:

Examples:

* Month
* Week
* Quarter
* Weekend

---

## Duration Features

Representing elapsed influence.

Examples:

Instead of:

```
CompetitionOpenSinceYear
```

use:

```
CompetitionAgeMonths
```

---

## Business Semantics

Features should represent real-world processes.

---

## Helper Columns

Temporary columns used to simplify calculations.

Examples:

* CompetitionOpenDate
* Promo2StartDate
* TransactionMonth

---

## Sentinel Values

Special values representing meaningful missing states.

Examples:

```
-1 → Information unavailable
0 → Valid state where event has not started
```

---

## Feature Validation

Checking:

* Correct values
* Correct ranges
* Correct data types
* Correct business logic

before modeling.

---

# Interview Questions

## Why did you create CompetitionAgeMonths instead of using CompetitionOpenSinceYear?

Because elapsed competition duration better represents competitive influence than a raw historical date.

---

## Why did you use sentinel values?

Because missing values represented different business states, not random missing data.

---

## Why was IsPromoMonth required when Promo2 already existed?

Promo2 only indicates participation in a recurring promotion program. IsPromoMonth captures whether the promotion was active during the transaction period.

---

## Why validate features before training?

Incorrect features can introduce silent errors and negatively affect model performance.

# Phase 5 Code & Function Reference

## Pandas

### sort_values()

Used to order observations chronologically before creating the train-validation split.

---

### iloc

Used to split the dataset based on row position.

---

### drop()

Used to remove helper columns and separate the target variable.

---

### isna()

Used to identify remaining missing values.

---

### loc[]

Used for conditional replacement of missing values.

---

## Scikit-learn

### ColumnTransformer

Applies different preprocessing operations to different groups of features within a single reusable preprocessing object.

---

### OneHotEncoder

Converts nominal categorical variables into binary indicator columns.

Parameters used:

* handle_unknown="ignore"
* sparse_output=False

---

### fit()

Learns preprocessing parameters from the training data only.

Examples:

* Learns categorical levels.
* Stores encoding mappings.

---

### transform()

Applies the learned preprocessing to any dataset without relearning.

---

### get_feature_names_out()

Returns the complete list of transformed feature names after preprocessing.

---

### named_transformers_

Provides access to fitted transformers inside a ColumnTransformer.

Useful for inspection and debugging.

---

### categories_

Displays the categories learned by a fitted OneHotEncoder.

---

## Concepts Learned

* Temporal validation
* Data leakage prevention
* fit vs transform
* One-Hot Encoding
* ColumnTransformer
* Model-ready datasets
* Reusable preprocessing
* Production ML workflow



# Phase 6

## 1. Input Data

**Key Components**

| Code                                                  | Purpose                                                                    |
| ----------------------------------------------------- | -------------------------------------------------------------------------- |
| `pd.read_csv()`                                       | Load the engineered training dataset.                                      |
| `train_test_split` (chronological split from Phase 5) | Preserve temporal ordering and prevent data leakage.                       |
| `ColumnTransformer`                                   | Apply identical preprocessing to every model.                              |
| `fit_transform()`                                     | Learn preprocessing transformations from the training set.                 |
| `transform()`                                         | Apply the learned transformations to the validation set without refitting. |

---

## 2. Baseline Model – Dummy Regressor

**Key Components**

| Code                              | Purpose                                                |
| --------------------------------- | ------------------------------------------------------ |
| `DummyRegressor(strategy="mean")` | Predict the average sales value as a baseline.         |
| `fit()`                           | Train the baseline model.                              |
| `predict()`                       | Generate baseline predictions.                         |
| `mean_absolute_error()`           | Measure average prediction error.                      |
| `root_mean_squared_error()`       | Measure error magnitude while penalizing large errors. |
| `r2_score()`                      | Measure the variance explained by the model.           |

---

## 3. Linear Regression

**Key Components**

| Code                 | Purpose                                                       |
| -------------------- | ------------------------------------------------------------- |
| `LinearRegression()` | Train the linear benchmark model.                             |
| `fit()`              | Learn linear relationships between features and sales.        |
| `predict()`          | Generate validation predictions.                              |
| `evaluate_model()`   | Compute MAE, RMSE, and R² using a common evaluation function. |

---

## 4. Random Forest Regressor

**Key Components**

| Code                      | Purpose                                        |
| ------------------------- | ---------------------------------------------- |
| `RandomForestRegressor()` | Train a nonlinear ensemble model.              |
| `n_estimators`            | Control the number of trees in the forest.     |
| `max_depth`               | Control tree complexity and study overfitting. |
| `fit()`                   | Train the ensemble model.                      |
| `predict()`               | Generate sales forecasts.                      |
| `evaluate_model()`        | Compare performance with previous models.      |

---

## 5. XGBoost Regressor

**Key Components**

| Code               | Purpose                                              |
| ------------------ | ---------------------------------------------------- |
| `XGBRegressor()`   | Train the final gradient boosting model.             |
| `learning_rate`    | Control the contribution of each boosting iteration. |
| `subsample`        | Improve generalization through row sampling.         |
| `colsample_bytree` | Improve robustness through feature sampling.         |
| `fit()`            | Train the boosting model.                            |
| `predict()`        | Generate final sales predictions.                    |
| `evaluate_model()` | Evaluate forecasting performance on unseen data.     |

---

## 6. Model Comparison

**Key Components**

| Code                    | Purpose                                       |
| ----------------------- | --------------------------------------------- |
| `results.append()`      | Store evaluation metrics for each model.      |
| `pd.DataFrame(results)` | Create a comparison table of all models.      |
| `sort_values()`         | Rank models according to performance metrics. |

---

## 7. Final Model Selection

**Key Components**

| Code                           | Purpose                                         |
| ------------------------------ | ----------------------------------------------- |
| Validation metrics             | Compare model generalization performance.       |
| Train vs Validation comparison | Detect overfitting.                             |
| Performance table              | Select the final forecasting model objectively. |

---

## 8. Model Persistence

**Key Components**

| Code                             | Purpose                          |
| -------------------------------- | -------------------------------- |
| `joblib.dump(preprocessor, ...)` | Save the preprocessing pipeline. |
| `joblib.dump(xgb_model, ...)`    | Save the trained XGBoost model.  |

---

### Libraries Used

| Library          | Purpose                                                             |
| ---------------- | ------------------------------------------------------------------- |
| **Pandas**       | Data loading, manipulation, and result storage                      |
| **NumPy**        | Numerical computations                                              |
| **Scikit-learn** | Preprocessing, regression models, evaluation metrics, and pipelines |
| **XGBoost**      | Gradient boosting regression                                        |
| **Joblib**       | Model serialization                                                 |

---



