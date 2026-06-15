# Phase 5 - Model Development
## Step 5.2 - Validation Framework

## Validation Summary
- Dataset rows: 100000
- Features used for CV: 227
- Target column: churn
- Overall churn rate: 0.49562
- Validation rows covered exactly once: True
- Validation duplicates across folds: 0

## Fold Summary
 fold  train_rows  validation_rows  train_churn_rate  validation_churn_rate  churn_rate_gap  validation_pos  validation_neg
    1       80000            20000           0.49561                0.49565         0.00004            9913           10087
    2       80000            20000           0.49561                0.49565         0.00004            9913           10087
    3       80000            20000           0.49562                0.49560         0.00002            9912           10088
    4       80000            20000           0.49562                0.49560         0.00002            9912           10088
    5       80000            20000           0.49562                0.49560         0.00002            9912           10088

## Churn Distribution
 churn  count   pct
     0  50438 50.44
     1  49562 49.56

## Leakage Assessment
- Train/validation overlap is zero in every fold.
- Validation rows are disjoint across folds and cover the full dataset exactly once.
- Stratification keeps fold churn rates aligned with the global class balance.

## Validation Design Rationale
- Use `StratifiedKFold` to preserve the near-balanced churn distribution in each fold.
- Keep preprocessing fit steps inside each training fold during later model training to avoid leakage.
- Reuse this splitter for all later benchmark models so score comparisons stay consistent.

## Recommendations
- Fit imputers, encoders, and scalers inside fold-specific pipelines only.
- Use the same fold generator and random seed for every later benchmark.
- If hyperparameter tuning is added later, use nested CV or a separate holdout to keep selection bias low.
