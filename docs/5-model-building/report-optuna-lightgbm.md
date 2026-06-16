# Phase 5 - Model Development
## Step 5.9 - Hyperparameter Optimization

## Objective
Tune the promoted LightGBM baseline on `modeling_dataset_v2.parquet` with Optuna while keeping the Step 5.2 five-fold stratified validation framework fixed.

## Search Space
- `learning_rate`: `0.01` to `0.2` on a log scale
- `num_leaves`: `8` to the fold-limited upper bound derived from `max_depth`
- `max_depth`: `-1`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `10`, `12`
- `min_child_samples`: `5` to `100`
- `feature_fraction`: `0.6` to `1.0`
- `bagging_fraction`: `0.6` to `1.0`
- `bagging_freq`: `0` to `10`
- `lambda_l1`: `1e-8` to `10.0` on a log scale
- `lambda_l2`: `1e-8` to `10.0` on a log scale
- `min_split_gain`: `0.0` to `0.5`

## Trial Summary
- Trials completed: `100`
- Best trial: `66`
- Best validation ROC AUC: `0.69505`
- Best train ROC AUC: `0.77905`
- Best train-vs-validation ROC AUC gap: `0.08400`
- The top trials were concentrated around deeper trees with fairly aggressive regularization on row/column sampling and split gain.

Top 5 trials by validation ROC AUC:

| Trial | Validation ROC AUC | Train ROC AUC | Gap | Learning Rate | Num Leaves | Max Depth | Min Child Samples |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 66 | 0.69505 | 0.77905 | 0.08400 | 0.12270 | 99 | 12 | 27 |
| 63 | 0.69493 | 0.77558 | 0.08065 | 0.13475 | 87 | 12 | 20 |
| 82 | 0.69463 | 0.80043 | 0.10580 | 0.13449 | 126 | 12 | 30 |
| 83 | 0.69438 | 0.80087 | 0.10649 | 0.13801 | 124 | 12 | 37 |
| 72 | 0.69425 | 0.79318 | 0.09893 | 0.13986 | 110 | 12 | 26 |

## Best Parameters
- `max_depth`: `12`
- `learning_rate`: `0.1226988031`
- `num_leaves`: `99`
- `min_child_samples`: `27`
- `feature_fraction`: `0.6865798643`
- `bagging_fraction`: `0.6147859226`
- `bagging_freq`: `0`
- `lambda_l1`: `0.0016395292`
- `lambda_l2`: `7.9451545464`
- `min_split_gain`: `0.4028193099`
- `n_estimators`: `50`

## Baseline ROC-AUC
- Promoted baseline from Step 5.6: `0.68724`
- Baseline replay recorded during the Optuna run: `0.68732`

## Tuned ROC-AUC
- Tuned validation ROC AUC: `0.69505`

## Improvement Analysis
- Validation ROC AUC improved by roughly `+0.0078` versus the promoted baseline.
- Accuracy increased from `0.63265` to `0.63904`.
- Precision increased from `0.62452` to `0.63348`.
- Recall moved from `0.64909` to `0.64475`.
- F1 increased from `0.63655` to `0.63905`.
- The tuned model is meaningfully stronger on the validation metric, so it satisfies the promotion rule.

## Overfitting Assessment
- Train ROC AUC increased from `0.71287` to `0.77905`.
- The train-vs-validation ROC AUC gap widened from `0.02556` to `0.08400`.
- This is a clear overfitting increase, but the validation ROC AUC gain is large enough to justify promotion under the prompt rule.
- The best trial also shows that LightGBM benefits from stronger tree capacity, weaker row sampling, and heavier split regularization at the same time.

## Recommendation
- Promote the tuned LightGBM model.
- Keep the Optuna study artifacts for reproducibility and treat the large train-validation gap as a warning sign for future calibration or nested-CV work.

## Deliverables
- Trials CSV: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/telecom/optuna_trials.csv`
- Best-parameters CSV: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/telecom/lightgbm_best_params.csv`
- Notebook: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/matsuo_final_assignment.ipynb`
