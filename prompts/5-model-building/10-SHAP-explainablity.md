# TASK: Model Explainability and Churn Driver Analysis

## Objective

Explain why the final promoted model predicts churn.

The purpose is to translate model behavior into business insights that can support the final proposal.

---

## Input

Use the promoted LightGBM model from Step 5.9.

Dataset:

Final Assignment/data/intermediate/modeling_dataset_v2.parquet

or

Final Assignment/data/intermediate/modeling_dataset_v3.parquet

depending on promotion decision.

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.10 - Model Explainability

---

## Required Actions

Generate:

1. Global SHAP Importance

2. SHAP Summary Plot

3. SHAP Dependence Plots

For:

- months
- eqpdays
- revenue_per_usage
- avgqty
- change_mou
- drop_vce_Mean
- hnd_price

4. Identify:

- strongest churn drivers
- strongest retention drivers

5. Extract business interpretations

---

## Save Outputs

Create:

Final Assignment/telecom/shap_feature_importance.csv

Save plots:

Final Assignment/telecom/shap/

---

## Generate Report

Create:

docs/5-model-building/report-shap-analysis.md

Include:

- Top 20 Drivers
- Driver Interpretation
- Churn Risk Factors
- Customer Retention Signals

---

## Deliverables

Return:

- Top 20 SHAP Features
- Top Churn Drivers
- Top Retention Drivers
- Report Path