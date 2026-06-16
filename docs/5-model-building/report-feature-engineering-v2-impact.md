# Phase 5 - Model Development
## Step 5.8 - Evaluate Feature Engineering V2 Impact

## Objective
Evaluate whether the telecom-specific engineered signals added in Step 5.7 improve churn prediction relative to the post-selection baseline.

## Inputs
- Baseline dataset: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v2.parquet`
- Engineered dataset: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v3.parquet`
- Step 5.6 reference: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/docs/5-model-building/report-post-selection-models.md`
- Step 5.7 reference: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/docs/5-model-building/report-feature-engineering-v2.md`
- Validation framework: `StratifiedKFold(n_splits=5, shuffle=True, random_state=42)`
- Model: `LightGBM` with the same configuration used in Step 5.6

## Dataset Comparison
- `modeling_dataset_v2` feature count: `61`
- `modeling_dataset_v3` feature count: `71`
- Added features: `10` including the target column, or `10` predictors

## Model Comparison
 comparison  feature_count  roc_auc_validation_mean  accuracy_validation_mean  precision_validation_mean  recall_validation_mean  f1_validation_mean  roc_auc_train_mean  roc_auc_gap_mean
         v2             61                  0.68724                   0.63298                    0.62510                 0.64824             0.63645             0.71283           0.02559
         v3             71                  0.68722                   0.63307                    0.62537                 0.64757             0.63627             0.71367           0.02644
v3_minus_v2             10                 -0.00002                   0.00009                    0.00027                -0.00067            -0.00018             0.00084           0.00086

## Evaluation Summary
- ROC AUC remained effectively unchanged after adding the V2 features.
- Validation ROC AUC moved from `0.68724` to `0.68722`.
- The validation gap moved from `0.02559` to `0.02644`.
- The model remains the same, so any difference is attributable to feature engineering rather than tuning.

## New Feature Importance
               feature  importance  rank top_correlated_feature  top_correlation recommendation
       usage_per_month     0.02680    12                 avgqty          0.81100           Keep
             drop_rate     0.01600    22          drop_vce_Mean          0.86954           Keep
     revenue_per_month     0.01493    24        usage_per_month          0.76236           Keep
            block_rate     0.00853    41          drop_blk_Mean          0.88447    Investigate
       phones_per_year     0.00720    43 model_changes_per_year          0.89200    Investigate
model_changes_per_year     0.00707    44        phones_per_year          0.89200    Investigate
   complaints_per_call     0.00533    49 support_to_usage_ratio          0.70439    Investigate
        change_mou_pct     0.00493    55             change_mou          1.00000         Remove
support_to_usage_ratio     0.00427    59    complaints_per_call          0.70439         Remove
        change_rev_pct     0.00200    66             change_rev          1.00000         Remove

## Importance Interpretation
- Highest importance overall: `revenue_per_usage` (`0.05813`).
- High-value new features: usage_per_month, drop_rate, revenue_per_month.
- Medium-value or investigatory features: block_rate, phones_per_year, model_changes_per_year, complaints_per_call.
- Low-value or redundant features: change_mou_pct, support_to_usage_ratio, change_rev_pct.
- Usage and revenue intensity features remain aligned with the original business hypotheses about engagement and spend.
- Device and service-quality ratios add interpretable structure, but several overlap with the existing handset and call-quality signals already present in `modeling_dataset_v2`.
- The strongest evidence is whether the model-level validation metric improves; feature importance is secondary support for interpreting the contribution of each engineered signal.

## Final Recommendation
- Keep `modeling_dataset_v2` as the operational baseline.
- `modeling_dataset_v3` did not deliver a meaningful validation gain, so the added telecom-specific features should be treated as explanatory candidates rather than a confirmed improvement.
- If downstream tuning is pursued, retain the stronger spend, usage, and service-quality ratios first and deprioritize the redundant device-ratio and percentage-change variants.

## Deliverables
- Comparison CSV: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/telecom/feature_engineering_v2_comparison.csv`
- Importance CSV: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/telecom/feature_engineering_v2_importance.csv`
- Notebook: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/matsuo_final_assignment.ipynb`
