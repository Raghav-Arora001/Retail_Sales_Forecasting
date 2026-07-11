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