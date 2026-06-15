# TASK: Train Baseline Model Suite

## Objective

Establish baseline performance before any feature pruning or optimization.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v1.parquet

Use validation framework from Step 5.2

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.3 - Baseline Models

---

## Models To Train

1. Logistic Regression

2. Random Forest

3. XGBoost

4. LightGBM

5. CatBoost

---

## Evaluation Metrics

For every fold compute:

- ROC AUC
- Accuracy
- Precision
- Recall
- F1 Score

Compute:

- mean score
- standard deviation

---

## Save Outputs

Create:

Final Assignment/telecom/baseline_model_results.csv

---

## Generate Report

Create:

docs/5-model-building/report-baseline-models.md

Include:

- model leaderboard
- fold statistics
- mean metrics
- standard deviations
- train vs validation comparison
- overfitting observations

---

## Selection Rule

Rank models by:

ROC AUC

Select best candidate for next phase.

---

## Deliverables

Return:

- leaderboard table
- best model
- csv path
- report path