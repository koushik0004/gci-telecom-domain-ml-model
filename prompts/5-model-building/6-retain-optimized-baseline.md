# TASK: Retrain Baseline Models Using Selected Features

## Objective

Measure the impact of feature selection.

Determine whether removing redundancy improves validation performance.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v2.parquet

Use:

StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.6 - Retraining After Feature Selection

---

## Required Actions

Retrain:

1. LightGBM
2. XGBoost
3. CatBoost

Compute:

- ROC AUC
- Accuracy
- Precision
- Recall
- F1

Compare against:

Step 5.3 baseline results

Calculate:

- score improvement
- score degradation
- feature count reduction

Determine:

- whether feature selection improved generalization
- whether feature selection reduced overfitting

---

## Save Outputs

Create:

Final Assignment/telecom/post_selection_results.csv

---

## Generate Report

Create:

docs/5-model-building/report-post-selection-models.md

---

## Selection Rule

Promote the highest ROC-AUC model.

---

## Deliverables

Return:

- comparison table
- best model
- ROC-AUC change
- report path