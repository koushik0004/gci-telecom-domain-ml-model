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

| fold | train_rows | validation_rows | train_churn_rate | validation_churn_rate | churn_rate_gap | validation_pos | validation_neg |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 80000 | 20000 | 0.49561 | 0.49565 | 0.00004 | 9913 | 10087 |
| 2 | 80000 | 20000 | 0.49561 | 0.49565 | 0.00004 | 9913 | 10087 |
| 3 | 80000 | 20000 | 0.49562 | 0.49560 | 0.00003 | 9912 | 10088 |
| 4 | 80000 | 20000 | 0.49562 | 0.49560 | 0.00003 | 9912 | 10088 |
| 5 | 80000 | 20000 | 0.49562 | 0.49560 | 0.00003 | 9912 | 10088 |

## Churn Distribution

| churn | count | pct |
| --- | ---: | ---: |
| 0 | 50438 | 50.44 |
| 1 | 49562 | 49.56 |

## Validation Design Rationale

- `StratifiedKFold` keeps the target distribution stable in every fold, which matters because the churn class balance is close to 50/50.
- `shuffle=True` and `random_state=42` make the split reproducible.
- Each fold uses 80,000 training rows and 20,000 validation rows, so all later model comparisons will be on the same split geometry.
- The framework is reusable: later model steps should consume this splitter rather than creating ad hoc partitions.

## Leakage Assessment

- Train and validation indices are disjoint within every fold.
- Validation indices are unique across folds and cover the full dataset exactly once.
- Because the modeling dataset is one row per customer and `Customer_ID` was removed in Step 5.1, there is no row-level identifier leakage in the CV split.
- The remaining leakage risk is procedural: any preprocessing fit on the full dataset would leak information into validation. That should be avoided by fitting transforms inside each fold.

## Recommendations

- Use the same `StratifiedKFold(n_splits=5, shuffle=True, random_state=42)` object for all later benchmark models.
- Wrap imputation, encoding, scaling, and model fitting in a fold-specific pipeline.
- If model tuning is added later, use nested CV or a separate holdout to keep selection bias under control.
- Keep this fold summary as the reference point for comparing later models.
