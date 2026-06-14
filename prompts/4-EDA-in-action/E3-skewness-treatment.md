TARGET NOTEBOOK: Final Assignment/matsuo_final_assignment.ipynb

TASK: Implement Skewness Treatment

Add a new section:

# SKEWNESS TREATMENT

Detect numeric features where:

abs(skewness) > 1

Create log-transformed versions using:

np.log1p()

Examples:

*_log

Do not overwrite originals.

Generate:

skewness_comparison_df

Columns:

feature
original_skew
transformed_skew

Save report:

docs/4-EDA-reports/skew_treatment_report.md

Save summary table:

Final Assignment/telecom/skewness_comparison.csv

Create dataset snapshot representing the complete dataframe state after skewness treatment.

Save snapshot:

Final Assignment/data/intermediate/E3_skewness.parquet

Validation:

- show top 20 skew reductions
- confirm skewness_comparison.csv created successfully
- confirm E3_skewness.parquet created successfully

Append new cells only.
