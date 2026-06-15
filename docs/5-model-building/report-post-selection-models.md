# Phase 5 - Model Development
## Step 5.6 - Retraining After Feature Selection

## Objective
Measure the impact of feature selection on the promoted baseline models.

## Inputs
- Baseline dataset: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v1.parquet`
- Selected dataset: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v2.parquet`
- Splitter: `StratifiedKFold(n_splits=5, shuffle=True, random_state=42)`

## Count Summary
- Starting feature count: `227`
- Final feature count: `61`
- Feature count reduction: `166`
- Output width including target column: `62`

## Validation Comparison
   model  roc_auc_mean_validation_baseline  roc_auc_mean_validation_selected  roc_auc_change  roc_auc_gap_mean_baseline  roc_auc_gap_mean_selected  roc_auc_gap_change  accuracy_mean_validation_baseline  accuracy_mean_validation_selected  precision_mean_validation_baseline  precision_mean_validation_selected  recall_mean_validation_baseline  recall_mean_validation_selected  f1_mean_validation_baseline  f1_mean_validation_selected
LightGBM                           0.68700                           0.68724         0.00024                    0.02717                    0.02559            -0.00158                            0.63262                            0.63298                             0.62435                             0.62510                          0.64955                          0.64824                      0.63669                      0.63645
 XGBoost                           0.67740                           0.67689        -0.00051                    0.01355                    0.01259            -0.00095                            0.62441                            0.62414                             0.61163                             0.61122                          0.66347                          0.66394                      0.63647                      0.63647
CatBoost                           0.67152                           0.67328         0.00177                    0.00947                    0.00899            -0.00049                            0.61942                            0.62040                             0.60635                             0.60547                          0.66170                          0.67193                      0.63280                      0.63695

## Best Model
- Best candidate after feature selection: `LightGBM`
- Selected validation ROC AUC: `0.68724`
- Baseline validation ROC AUC: `0.68700`
- ROC AUC change: `+0.00024`

## Overfitting Observations
- Validation ROC AUC improved for: LightGBM, CatBoost.
- Validation ROC AUC declined for: XGBoost.
- Train-vs-validation ROC AUC gap decreased for: LightGBM, XGBoost, CatBoost.
- The reduced feature set keeps the strongest signals but removes the broad redundant families that were inflating complexity.
- The comparison is controlled because both runs use the same five-fold splitter and the same model families.

## Recommendation
- Promote `LightGBM` as the post-selection baseline.
- Keep the Step 5.2 splitter fixed for all future comparisons.

## Deliverables
- Results CSV: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/telecom/post_selection_results.csv`
- Notebook: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/matsuo_final_assignment.ipynb`
