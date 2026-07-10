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

