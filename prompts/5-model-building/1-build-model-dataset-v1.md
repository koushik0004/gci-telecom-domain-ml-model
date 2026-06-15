# TASK: Build Modeling Dataset V1

## Objective

Create the first production-ready modeling dataset by applying all approved EDA outputs.

This step must consolidate:

- Missing value treatment
- Missing indicators
- Skewness treatment
- Outlier treatment
- Feature Engineering V1
- Interaction Features

into a single modeling dataset.

---

## Input Files

Use:

Final Assignment/telecom/Client.csv

Final Assignment/telecom/Record.csv

Reference reports:

docs/4-eda/report-missingness-features.md
docs/4-eda/report-skew-treatment.md
docs/4-eda/report-outlier-treatment.md
docs/4-eda/report-feature-engineering-v1.md
docs/4-eda/report-interaction-features.md
docs/4-eda/report-eda-action-matrix.md

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Do not overwrite existing cells.

Add clear markdown sections.

Create section:

# Phase 5 - Model Development
## Step 5.1 - Modeling Dataset Creation

---

## Required Actions

1. Load Client.csv and Record.csv

2. Merge datasets using Customer_ID

3. Remove Customer_ID from modeling features

4. Recreate all missing value treatments

5. Recreate all missing indicators

6. Recreate all skewness transformations

7. Recreate all winsorized features

8. Recreate Feature Engineering V1 features

9. Recreate interaction features

10. Verify:

- No missing values remain
- Target column churn exists
- Row count remains unchanged

11. Create dataframe:

df_model_v1

---

## Save Outputs

Save parquet:

Final Assignment/data/intermediate/modeling_dataset_v1.parquet

---

## Generate Report

Create:

docs/5-model-building/report-modeling-dataset-v1.md

Include:

- row count
- column count
- target distribution
- number of engineered features
- number of missing indicators
- transformation summary
- final schema summary

---

## Deliverables

Return:

- dataframe shape
- number of features
- parquet path
- report path
- list of newly created columns