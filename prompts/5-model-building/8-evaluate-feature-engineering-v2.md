# TASK: Evaluate Feature Engineering V2 Impact

## Objective

Evaluate whether the newly created telecom-specific features improve churn prediction performance.

This is a controlled experiment.

The goal is NOT to optimize the model.

The goal is to measure the contribution of the V2 engineered features relative to the post-selection baseline dataset.

---

## Context

Current best model:

LightGBM

Current promoted baseline:

modeling_dataset_v2.parquet

Current validation ROC-AUC:

0.68724

The V2 feature engineering step created 10 new telecom-specific features and produced:

Final Assignment/data/intermediate/modeling_dataset_v3.parquet

Before proceeding to hyperparameter tuning, SHAP, or business proposal generation, we must verify whether these new features provide measurable predictive value.

---

## Input Files

Load:

Final Assignment/data/intermediate/modeling_dataset_v2.parquet

Final Assignment/data/intermediate/modeling_dataset_v3.parquet

Reference Reports:

docs/5-model-building/report-post-selection-models.md

docs/5-model-building/report-feature-engineering-v2.md

---

## Notebook Update Requirements

Append new cells to:

Final Assignment/matsuo_final_assignment.ipynb

Create section:

# Phase 5 - Model Development
## Step 5.8 - Evaluate Feature Engineering V2 Impact

Do not overwrite existing notebook content.

---

## Validation Requirements

Use the exact same validation framework from Step 5.2:

```python
StratifiedKFold(
    n_splits=5,
    shuffle=True,
    random_state=42
)
```

This must remain unchanged to ensure fair comparison.

---

## Model Requirements

Use the same LightGBM configuration that produced the Step 5.6 benchmark.

Do not perform hyperparameter tuning.

Do not change model settings.

The only difference between experiments should be the feature set.

---

## Experiment A

Train LightGBM using:

modeling_dataset_v2.parquet

Collect:

- ROC AUC
- Accuracy
- Precision
- Recall
- F1 Score

Store fold-level results.

---

## Experiment B

Train LightGBM using:

modeling_dataset_v3.parquet

Collect:

- ROC AUC
- Accuracy
- Precision
- Recall
- F1 Score

Store fold-level results.

---

## Comparative Analysis

Calculate:

- ROC-AUC Difference
- Accuracy Difference
- Precision Difference
- Recall Difference
- F1 Difference

Evaluate:

- Did performance improve?
- Did performance remain unchanged?
- Did performance decline?

Determine whether the new telecom features contribute useful predictive signal.

---

## New Feature Contribution Analysis

Specifically evaluate the contribution of:

- revenue_per_month
- usage_per_month
- change_rev_pct
- change_mou_pct
- phones_per_year
- model_changes_per_year
- drop_rate
- block_rate
- support_to_usage_ratio
- complaints_per_call

Compute:

- Feature importance ranking
- Relative contribution
- Redundancy with existing features

Identify:

- High-value new features
- Medium-value new features
- Low-value or redundant new features

---

## Save Outputs

Create:

Final Assignment/telecom/feature_engineering_v2_comparison.csv

Create:

Final Assignment/telecom/feature_engineering_v2_importance.csv

---

## Generate Report

Create:

docs/5-model-building/report-feature-engineering-v2-impact.md

---

## Report Requirements

Include:

### Dataset Comparison

- V2 feature count
- V3 feature count

### Model Comparison

- ROC AUC comparison
- Accuracy comparison
- Precision comparison
- Recall comparison
- F1 comparison

### New Feature Evaluation

Table containing:

| Feature | Importance | Rank | Recommendation |
|----------|----------|----------|----------|

Recommendation values:

- Keep
- Investigate
- Remove

### Business Interpretation

Explain:

- Which telecom behaviours appear predictive
- Which engineered features align with original business hypotheses
- Whether telecom-specific feature engineering added measurable value

### Final Recommendation

Choose one:

1. Promote modeling_dataset_v3
2. Keep modeling_dataset_v2
3. Create reduced V3 dataset

Justify the decision using validation results.

---

## Deliverables

Return:

- Experiment A metrics
- Experiment B metrics
- Metric deltas
- Top 20 features
- Best new engineered feature
- Worst new engineered feature
- Recommendation for next phase
- Report path
- CSV paths