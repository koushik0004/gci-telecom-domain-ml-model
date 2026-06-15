# TASK: Telecom Feature Engineering V2

## Objective

Create second-generation telecom-specific predictive signals.

Only proceed after feature-selection results are available.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v2.parquet

Reference:

docs/4-eda/business_understanding.md
docs/4-eda/hypothesis_seeds.md

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.7 - Feature Engineering V2

---

## Required Actions

Create telecom-specific signals.

Usage Behaviour:

- revenue_per_month
- usage_per_month

Trend Behaviour:

- change_rev_pct
- change_mou_pct

Device Signals:

- phones_per_year
- model_changes_per_year

Service Quality:

- drop_rate
- block_rate

Customer Engagement:

- support_to_usage_ratio
- complaints_per_call

Create only features that are mathematically valid.

Avoid introducing leakage.

Create:

df_model_v3

---

## Save Outputs

Save:

Final Assignment/data/intermediate/modeling_dataset_v3.parquet

---

## Generate Report

Create:

docs/5-model-building/report-feature-engineering-v2.md

---

## Deliverables

Return:

- features created
- dataset shape
- report path