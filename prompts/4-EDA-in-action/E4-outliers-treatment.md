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

Save:

docs/4-EDA-reports/outlier_treatment_report.md

Validation:

show cap thresholds and affected rows.

Append new cells only.
