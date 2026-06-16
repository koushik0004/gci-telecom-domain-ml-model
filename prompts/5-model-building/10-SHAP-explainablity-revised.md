### Phase A: Notebook Update Only

# TASK: Step 5.10 - Model Explainability (Notebook Update Only)

## Objective

Add SHAP explainability code to the existing notebook.

The purpose is to generate SHAP artifacts that will later be used for business interpretation and reporting.

---

## Input

Use the promoted LightGBM model from Step 5.9.

Use:

* Final Assignment/data/intermediate/modeling_dataset_v2.parquet

or

* Final Assignment/data/intermediate/modeling_dataset_v3.parquet

depending on the final promoted dataset.

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.10 - Model Explainability

---

## IMPORTANT EXECUTION RULES

* DO NOT execute the notebook.
* DO NOT run any existing notebook cells.
* DO NOT rerun EDA, feature engineering, model training, Optuna, or previous steps.
* ONLY append new code cells.
* New cells must load required artifacts from disk.
* New cells must be independently executable.
* Assume the user will manually run the newly added cells.

---

## Required Actions

Generate notebook code that:

1. Loads the promoted model.

2. Loads the final modeling dataset.

3. Computes Global SHAP Importance.

4. Generates SHAP Summary Plot.

5. Generates SHAP Dependence Plots for:

   * months
   * eqpdays
   * revenue_per_usage
   * avgqty
   * change_mou
   * drop_vce_Mean
   * hnd_price

6. Identifies:

   * strongest churn drivers
   * strongest retention drivers

7. Saves all outputs to disk.

---

## Save Outputs

Create:

Final Assignment/telecom/shap_feature_importance.csv

Save plots:

Final Assignment/telecom/shap/

Expected files include:

* shap_summary.png
* shap_importance.png
* dependence_months.png
* dependence_eqpdays.png
* dependence_revenue_per_usage.png
* dependence_avgqty.png
* dependence_change_mou.png
* dependence_drop_vce_Mean.png
* dependence_hnd_price.png

---

## Deliverables

Return:

* Summary of newly added notebook cells
* List of expected output files

Do not generate business interpretation or markdown reports in this step.

---

---

### Phase B: Report Generation After Manual Execution

# TASK: Step 5.10 - SHAP Analysis Report Generation

## Objective

Generate the SHAP analysis report using artifacts that were already created by the notebook.

---

## Prerequisite

Assume the user has already executed the Step 5.10 notebook cells manually.

Do NOT modify the notebook.

Do NOT execute any notebook code.

Do NOT retrain any model.

---

## Input Artifacts

Use:

Final Assignment/telecom/shap_feature_importance.csv

and all files under:

Final Assignment/telecom/shap/

including:

* shap_summary.png
* shap_importance.png
* dependence_months.png
* dependence_eqpdays.png
* dependence_revenue_per_usage.png
* dependence_avgqty.png
* dependence_change_mou.png
* dependence_drop_vce_Mean.png
* dependence_hnd_price.png

Also use:

* report-feature-importance.md
* final promoted model metadata

if available.

---

## Required Analysis

Generate:

1. Top 20 SHAP Features

2. Strongest Churn Drivers

3. Strongest Retention Drivers

4. Feature-Level Business Interpretation

5. Customer Lifecycle Insights

6. Revenue and Usage Insights

7. Service Quality Insights

8. Device Lifecycle Insights

9. Customer Risk Signals

10. Retention Signals

---

## Generate Report

Create:

docs/5-model-building/report-shap-analysis.md

---

## Deliverables

Return:

* Top 20 SHAP Features
* Top Churn Drivers
* Top Retention Drivers
* Executive Summary
* Report Path

This step is analysis-only and must rely exclusively on generated artifacts.
