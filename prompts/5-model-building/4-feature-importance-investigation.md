# TASK: Feature Importance Investigation

## Objective

Identify which features actually drive churn prediction in the current best-performing model.

The goal is to determine:

- which original features matter
- which engineered features matter
- which missing indicators matter
- which transformed features matter
- which features contribute little or no signal

This step will drive all later feature-selection decisions.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v1.parquet

Reference:

docs/5-model-building/report-baseline-models.md
docs/4-eda/feature_validation_report.md
docs/4-eda/correlation_cluster_report.md

Best baseline model:

LightGBM

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.4 - Feature Importance Investigation

---

## Required Actions

Train LightGBM using the same validation framework.

Compute:

1. Gain Importance
2. Split Importance
3. Permutation Importance

Create a consolidated feature ranking.

Compare findings against:

- feature validation report
- correlation cluster report
- business hypotheses

Specifically investigate:

- eqpdays
- months
- change_mou
- change_rev
- avgqty
- totcalls
- revenue_per_usage
- service_issue_score
- drop_vce_Mean

Identify:

- Top 50 features
- Top 20 features
- Features with zero importance
- Features with near-zero importance

Group findings by:

- Original Features
- Missing Indicators
- Log Features
- Engineered Features
- Interaction Features

---

## Save Outputs

Create:

Final Assignment/telecom/feature_importance.csv

---

## Generate Report

Create:

docs/5-model-building/report-feature-importance.md

Include:

- Top 50 Features
- Importance Distribution
- Feature Family Analysis
- Business Interpretation
- Candidate Removal List

---

## Deliverables

Return:

- Top 20 features
- Number of zero-importance features
- Number of near-zero features
- Report path
- CSV path