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