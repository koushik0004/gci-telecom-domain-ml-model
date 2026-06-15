# INTERACTION FEATURES

The interaction flags below test the EDA hypothesis that churn risk concentrates where low engagement overlaps with high bill burden, old hardware, or service trouble.

## Thresholds

- low usage: `mou_Mean <= 150.75`
- high charge: `totmrc_Mean >= 59.99`
- old device: `eqpdays >= 530.00`
- low value: `hnd_price <= 29.99`
- poor service: `drop_vce_Mean >= 7.67` or `blck_vce_Mean >= 3.67` or `drop_blk_Mean >= 12.33`

## Summary Table

     interaction_feature                                                         threshold_rule  segment segment_label  count  segment_share_pct  churn_rate  delta_vs_overall
 low_usage_x_high_charge                    mou_Mean <= Q1(150.75) and totmrc_Mean >= Q3(59.99)        0            no  98156             98.156    0.495110         -0.000510
 low_usage_x_high_charge                    mou_Mean <= Q1(150.75) and totmrc_Mean >= Q3(59.99)        1           yes   1844              1.844    0.522777          0.027157
low_usage_x_poor_service mou_Mean <= Q1(150.75) and service issue component >= its Q3 threshold        0            no  98346             98.346    0.495018         -0.000602
low_usage_x_poor_service mou_Mean <= Q1(150.75) and service issue component >= its Q3 threshold        1           yes   1654              1.654    0.531439          0.035819
  old_device_x_low_value                       eqpdays >= Q3(530.00) and hnd_price <= Q1(29.99)        0            no  84681             84.681    0.481076         -0.014544
  old_device_x_low_value                       eqpdays >= Q3(530.00) and hnd_price <= Q1(29.99)        1           yes  15319             15.319    0.576017          0.080397

## Notes

- The dataframe is retained in full; this step only adds binary interaction flags.
- Churn lift is measured against the overall dataset mean churn rate.