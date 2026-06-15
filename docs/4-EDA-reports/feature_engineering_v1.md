# FEATURE ENGINEERING

The feature engineering step adds six derived signals recommended by the EDA plan. The dataframe is kept intact and the new columns are appended to the full modeling table.

## Derived Features

- `usage_to_charge = mou_Mean / totmrc_Mean`
- `revenue_per_usage = rev_Mean / (mou_Mean + 1)`
- `trend_gap = avg3mou - avg6mou`
- `revenue_gap = avg3rev - avg6rev`
- `service_issue_score = drop_vce_Mean + blck_vce_Mean + drop_blk_Mean`
- `support_intensity = custcare_Mean + ccrndmou_Mean + cc_mou_Mean`

## Summary Table

            feature                                       formula  null_count  null_pct      mean        std         min        25%       50%       75%         max
        revenue_gap                             avg3rev - avg6rev        2839     2.839  0.398771  19.146355  -774.00000  -3.000000  0.000000  3.000000  738.000000
  revenue_per_usage                     rev_Mean / (mou_Mean + 1)         357     0.357  0.745688   4.132132    -6.16750   0.089803  0.140197  0.257510  163.230000
service_issue_score drop_vce_Mean + blck_vce_Mean + drop_blk_Mean           0     0.000 20.022300  30.580090     0.00000   3.333333 10.666667 24.666667  840.000000
  support_intensity   custcare_Mean + ccrndmou_Mean + cc_mou_Mean           0     0.000 10.141046  27.620691     0.00000   0.000000  0.000000  9.000000 2139.616667
          trend_gap                             avg3mou - avg6mou        2839     2.839  6.577824 145.314008 -2528.00000 -37.000000  2.000000 50.000000 2284.000000
    usage_to_charge                        mou_Mean / totmrc_Mean         686     0.686 11.338052  30.390763 -6430.30303   4.168056  8.558361 14.677330  833.000000

## Validation
- Engineered features added: 6
- Rows: 100000
- Columns before: 99
- Columns after: 105
- Null counts and distribution statistics are recorded in the summary table below.