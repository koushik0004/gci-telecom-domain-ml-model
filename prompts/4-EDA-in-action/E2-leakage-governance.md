TARGET NOTEBOOK: Final Assignment/matsuo_final_assignment.ipynb

TASK: Build Feature Governance Registry

Add a new section:

# FEATURE GOVERNANCE

Create three lists:

SAFE_FEATURES
CONDITIONAL_FEATURES
UNKNOWN_FEATURES

Classify features using EDA findings.

Create:

feature_governance_df

Columns:

feature
governance_type
reason

Save report:

docs/4-EDA-reports/feature_governance.md

Save summary table:

Final Assignment/telecom/feature_governance.csv

Create dataset snapshot representing the complete dataframe state after governance classification.

Save snapshot:

Final Assignment/data/intermediate/E2_governance.parquet

Validation:

- show counts for each governance group
- confirm feature_governance.csv created successfully
- confirm E2_governance.parquet created successfully

Do not drop features yet.
Append new cells only.
