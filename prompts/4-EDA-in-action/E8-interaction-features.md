TARGET NOTEBOOK: Final Assignment/matsuo_final_assignment.ipynb

TASK: Build Interaction Features

Add a new section:

# INTERACTION FEATURES

Create:

low_usage_x_high_charge

old_device_x_low_value

low_usage_x_poor_service

Use EDA quartiles to define thresholds.

Generate:

interaction_summary_df

Save report:

docs/4-EDA-reports/interaction_feature_report.md

Save summary table:

Final Assignment/telecom/interaction_summary.csv

Create dataset snapshot representing the complete dataframe state after interaction feature generation.

Save snapshot:

Final Assignment/data/intermediate/E8_interactions.parquet

Validation:

- show churn rate by interaction segment
- confirm interaction_summary.csv created successfully
- confirm E8_interactions.parquet created successfully

Append new cells only.
