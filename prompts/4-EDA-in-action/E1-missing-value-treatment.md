TARGET NOTEBOOK: Final Assignment/matsuo_final_assignment.ipynb

TASK: Implement Missing Value Treatment

Open the notebook and identify the current modeling dataframe.

Reuse the existing dataframe. Do not reload data or create a duplicate dataframe.

Add a new section:

# MISSING VALUE TREATMENT

For every feature with missing values:

* create a missing indicator column
* median impute numeric columns
* fill categorical columns with "MISSING"

Keep all original columns.

Generate:

missingness_summary_df

Columns:

* feature
* missing_before
* missing_after
* indicator_created
* imputation_strategy

Save report:

docs/4-EDA-reports/missingness_features_report.md

Save summary table:

Final Assignment/telecom/missingness_summary.csv

Create a dataset snapshot representing the complete dataframe state after missing-value treatment.

Save snapshot:

Final Assignment/data/intermediate/E1_missingness.parquet

Validation:

* missing count before treatment
* missing count after treatment
* indicators created
* dataframe shape before and after
* confirm E1_missingness.parquet created successfully

Append new cells only.

Do not remove features.
Do not overwrite existing notebook sections.
