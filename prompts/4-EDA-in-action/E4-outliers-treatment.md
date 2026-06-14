TARGET NOTEBOOK: Final Assignment/matsuo_final_assignment.ipynb

TASK: Implement Outlier Treatment

Add a new section:

# OUTLIER TREATMENT

Apply winsorization:

lower = 1 percentile
upper = 99 percentile

Prioritize:

change_rev
change_mou
roam_Mean
ovrmou_Mean
vceovr_Mean

Create:

*_capped

Do not overwrite originals.

Generate:

outlier_summary_df

Save report:

docs/4-EDA-reports/outlier_treatment_report.md

Save summary table:

Final Assignment/telecom/outlier_summary.csv

Create dataset snapshot representing the complete dataframe state after outlier treatment.

Save snapshot:

Final Assignment/data/intermediate/E4_outlier.parquet

Validation:

- show cap thresholds and affected rows
- confirm outlier_summary.csv created successfully
- confirm E4_outlier.parquet created successfully

Append new cells only.
