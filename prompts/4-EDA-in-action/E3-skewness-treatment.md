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

Save:

docs/4-EDA-reports/skew_treatment_report.md

Validation:

show top 20 skew reductions.

Append new cells only.
