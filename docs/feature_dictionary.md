# Feature Dictionary (Modeling Features)

## Target Variable

| Feature | Type | Description |
|---------|------|-------------|
| Sales | Numerical | Daily sales of the store (target variable). |

---

## Identifier

| Feature | Type | Description |
|---------|------|-------------|
| Store | Identifier | Unique store ID. Retained for experimentation during model development and evaluated for its impact on generalization. |

---

## Calendar Features

| Feature | Type | Description |
|---------|------|-------------|
| DayOfWeek | Categorical | Day of the week (1–7). |
| Year | Numerical | Transaction year. |
| Month | Ordinal | Transaction month (1–12). |
| Day | Numerical | Day of the month. |
| WeekOfYear | Numerical | ISO week number. |
| Quarter | Ordinal | Quarter of the year (1–4). |
| IsMonthStart | Binary | Indicates whether the transaction occurred on the first day of the month. |
| IsMonthEnd | Binary | Indicates whether the transaction occurred on the last day of the month. |
| IsWeekend | Binary | Indicates whether the transaction occurred on a weekend. |

---

## Promotion Features

| Feature | Type | Description |
|---------|------|-------------|
| Promo | Binary | Indicates whether a regular promotion was active. |
| Promo2 | Binary | Indicates whether the store participates in the recurring Promo2 program. |
| Promo2AgeMonths | Numerical | Number of months since Promo2 became active. Sentinel value (-1) indicates no Promo2 participation. |
| IsPromoMonth | Binary | Indicates whether the transaction occurred during a scheduled Promo2 promotion month. |

---

## Competition Features

| Feature | Type | Description |
|---------|------|-------------|
| CompetitionDistance | Numerical | Distance to the nearest competitor. Missing values were imputed with -1 to represent unavailable information. |
| CompetitionInfoAvailable | Binary | Indicates whether competition metadata is available for the store. |
| CompetitionAgeMonths | Numerical | Number of months since the nearest competitor opened. Sentinel values distinguish unavailable information from competitors that had not yet opened. |

---

## Store Characteristics

| Feature | Type | Description |
|---------|------|-------------|
| StoreType | Nominal Categorical | Classification of the store. |
| Assortment | Nominal Categorical | Product assortment level offered by the store. |

---

## Holiday Features

| Feature | Type | Description |
|---------|------|-------------|
| StateHoliday | Nominal Categorical | Type of state holiday on the transaction date. |
| SchoolHoliday | Binary | Indicates whether schools were on holiday. |

---

## Preprocessing

The following preprocessing steps are applied before model training:

- One-hot encoding:
  - StateHoliday
  - StoreType
  - Assortment

- Remaining features are passed through unchanged.

- The preprocessing pipeline is implemented using `ColumnTransformer` with `OneHotEncoder(handle_unknown="ignore")`.