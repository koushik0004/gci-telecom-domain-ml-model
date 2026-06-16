# Phase 5 - Model Development
## Step 5.7 - Feature Engineering V2

## Objective
Create a second-generation set of telecom-specific predictive signals on top of the selected modeling dataset.

## Input
- Selected dataset: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v2.parquet`
- Reference docs: `docs/business_understanding.md`, `docs/hypothesis_seeds.md`

## Feature Set
- `revenue_per_month = avgrev / months`
- `usage_per_month = avgqty / months`
- `change_rev_pct = change_rev / 100`
- `change_mou_pct = change_mou / 100`
- `phones_per_year = phones / (months / 12)`
- `model_changes_per_year = max(phones - 1, 0) / (months / 12)`
- `drop_rate = drop_vce_Mean / months`
- `block_rate = drop_blk_Mean / months`
- `support_to_usage_ratio = support_intensity / (avgqty + 1)`
- `complaints_per_call = custcare_Mean / (avgqty + 1)`

## Validation Notes
- All features are computed from pre-churn or static fields already present in the selected modeling dataset.
- `models` is not present in `modeling_dataset_v2`, so handset count is used as the available proxy for the requested device-change signal.
- `drop_blk_Mean` is the best available service-quality proxy for the requested block-rate feature in this selected dataset.
- The new ratios use guarded denominators and do not introduce target leakage.

## Summary Table
```text
               feature                            formula  null_count  null_pct      mean       std        min       25%       50%       75%        max
     revenue_per_month                    avgrev / months           0  0.000000  3.991612  3.590338   0.009000  1.758416  2.991538  5.003750  89.071429
       usage_per_month                    avgqty / months           0  0.000000 12.238829 14.924005   0.000000  3.390909  7.533431 15.447206 339.588750
        change_rev_pct                   change_rev / 100           0  0.000000 -0.010148  0.501384 -11.077400 -0.072031 -0.003150  0.015450  99.636575
        change_mou_pct                   change_mou / 100           0  0.000000 -0.138654  2.748557 -38.750000 -0.860000 -0.062500  0.617500 312.192500
       phones_per_year             phones / (months / 12)           0  0.000000  1.301917  0.892369   0.200000  0.727273  1.090909  1.600000  19.500000
model_changes_per_year max(phones - 1, 0) / (months / 12)           0  0.000000  0.486738  0.802978   0.000000  0.000000  0.000000  0.800000  18.000000
             drop_rate             drop_vce_Mean / months           0  0.000000  0.425052  0.784634   0.000000  0.040404  0.172840  0.484848  29.333333
            block_rate             drop_blk_Mean / months           0  0.000000  0.735468  1.436332   0.000000  0.086957  0.305556  0.809524  69.952381
support_to_usage_ratio   support_intensity / (avgqty + 1)           0  0.000000  0.058495  0.252452   0.000000  0.000000  0.000000  0.051298  44.043360
   complaints_per_call       custcare_Mean / (avgqty + 1)           0  0.000000  0.010046  0.031846   0.000000  0.000000  0.000000  0.009221   3.626924
```

## Count Summary
- Rows: `100000`
- Columns before: `62`
- Columns after: `72`
- New features added: `10`

## Deliverables
- Parquet: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v3.parquet`
- Notebook: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/matsuo_final_assignment.ipynb`
