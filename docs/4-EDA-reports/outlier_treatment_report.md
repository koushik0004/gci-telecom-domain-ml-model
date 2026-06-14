# OUTLIER TREATMENT

Winsorization at the 1st and 99th percentiles was applied to the prioritized features without changing the original columns.

## Cap Summary

    feature  lower_bound  upper_bound  affected_rows  original_min  original_max  capped_min  capped_max      capped_column
 change_mou    -835.9800    751.46000           1984      -3875.00    31219.2500   -835.9800   751.46000  change_mou_capped
 change_rev    -104.5743    121.88250           1984      -1107.74     9963.6575   -104.5743   121.88250  change_rev_capped
  roam_Mean       0.0000     22.40935            997          0.00     3685.2000      0.0000    22.40935   roam_Mean_capped
vceovr_Mean       0.0000    137.76850            997          0.00      896.0875      0.0000   137.76850 vceovr_Mean_capped
ovrmou_Mean       0.0000    430.75000            996          0.00     4320.7500      0.0000   430.75000 ovrmou_Mean_capped