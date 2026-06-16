# TASK: Hyperparameter Optimization for Promoted LightGBM Model

## Objective

Improve the current promoted baseline model through systematic hyperparameter optimization.

Current baseline:

- Model: LightGBM
- Dataset: modeling_dataset_v2.parquet
- Validation ROC-AUC: 0.68724

The goal is to determine whether model tuning can produce a meaningful improvement beyond the current baseline.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v2.parquet

Reference:

docs/5-model-building/report-post-selection-models.md

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.9 - Hyperparameter Optimization

Do not overwrite existing notebook content.

---

## Validation Requirements

Use the exact validation framework from Step 5.2:

StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)

Do not modify the validation strategy.

---

## Optimization Framework

Use:

Optuna

Trials:

100

Optimization Metric:

ROC-AUC

---

## Hyperparameters To Search

learning_rate

num_leaves

max_depth

min_child_samples

feature_fraction

bagging_fraction

bagging_freq

lambda_l1

lambda_l2

min_split_gain

---

## Required Actions

1. Build Optuna objective function

2. Use cross-validation inside objective

3. Track fold-level ROC-AUC

4. Track train-vs-validation gap

5. Save best parameters

6. Retrain LightGBM using best parameters

7. Compare against promoted baseline

---

## Save Outputs

Create:

Final Assignment/telecom/optuna_trials.csv

Final Assignment/telecom/lightgbm_best_params.csv

---

## Generate Report

Create:

docs/5-model-building/report-optuna-lightgbm.md

Include:

- Search Space
- Trial Summary
- Best Parameters
- Baseline ROC-AUC
- Tuned ROC-AUC
- Improvement Analysis
- Overfitting Assessment

---

## Promotion Rule

Promote tuned model only if validation ROC-AUC improves.

Otherwise keep existing baseline.

---

## Deliverables

Return:

- Best Parameters
- Baseline ROC-AUC
- Tuned ROC-AUC
- Improvement
- Report Path
- CSV Paths