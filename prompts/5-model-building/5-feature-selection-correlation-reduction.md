# TASK: Feature Selection and Correlation Reduction

## Objective

Reduce feature redundancy and remove low-value predictors.

Current dataset contains 227 features.

The goal is to create a cleaner and more efficient modeling dataset.

---

## Input

Load:

Final Assignment/data/intermediate/modeling_dataset_v1.parquet

Reference:

docs/5-model-building/report-feature-importance.md
docs/4-eda/correlation_cluster_report.md
docs/4-eda/feature_governance.md

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

## Step 5.5 - Feature Selection

---

## Required Actions

Use feature importance findings.

Remove:

- Zero-importance features
- Near-zero importance features
- Redundant correlation-cluster members

Use EDA cluster recommendations.

Review:

Usage Cluster

Revenue Cluster

Service Cluster

Support Cluster

For every cluster:

- Keep strongest predictor
- Remove redundant alternatives

Preserve:

- strong business features
- governance-approved features

Do not remove:

- eqpdays
- months
- change_mou

unless evidence strongly supports removal.

Create:

df_model_v2

---

## Save Outputs

Save parquet:

Final Assignment/data/intermediate/modeling_dataset_v2.parquet

Create CSV:

Final Assignment/telecom/feature_selection_summary.csv

---

## Generate Report

Create:

docs/5-model-building/report-feature-selection.md

Include:

- Starting Feature Count
- Final Feature Count
- Removed Features
- Cluster Decisions
- Expected Benefits

---

## Deliverables

Return:

- original feature count
- final feature count
- features removed
- parquet path
- report path