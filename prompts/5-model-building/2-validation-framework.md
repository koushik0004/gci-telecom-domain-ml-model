# TASK: Create Validation Framework

## Objective

Create a reusable and leakage-safe validation framework for churn prediction.

This framework will be used by every model in later steps.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v1.parquet

Target:

churn

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.2 - Validation Framework

---

## Required Actions

1. Separate:

X
y

2. Configure:

StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)

3. For each fold calculate:

- train rows
- validation rows
- churn rate train
- churn rate validation

4. Verify target balance consistency

5. Verify no leakage exists between folds

6. Create reusable CV helper functions

---

## Generate Report

Create:

docs/5-model-building/report-validation-framework.md

Include:

- fold statistics
- churn distribution
- validation design rationale
- leakage assessment
- recommendations

---

## Deliverables

Return:

- fold summary table
- report path
- validation strategy summary