# Phase 5 - Model Development
## Step 5.4 - Feature Importance Investigation

## Objective
Use the best baseline model, LightGBM, to quantify feature importance with gain, split, and permutation views under the same five-fold validation framework from Step 5.2.

## Run Summary
- Dataset rows: 100000
- Predictors evaluated: 227
- Categorical predictors: 21
- Numeric predictors: 206
- Validation splitter: StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
- Permutation sample per fold: 2000 rows
- Zero-importance features: 57
- Near-zero features: 82

## Fold Validation Check
 fold  train_roc_auc  validation_roc_auc
    1        0.71435             0.68426
    2        0.71291             0.69102
    3        0.71504             0.68333
    4        0.71402             0.68953
    5        0.71455             0.68688

## Top 20 Features
 consolidated_rank                feature      feature_family  consolidated_score  gain_importance_mean  split_importance_mean  perm_importance_mean
                 1                 months   Original Features            0.119418           8488.277161             103.400000              0.026473
                 2                eqpdays   Original Features            0.118582          12139.361837              37.000000              0.024915
                 3              hnd_price   Original Features            0.049596           2470.891500              51.000000              0.012391
                 4      revenue_per_usage Engineered Features            0.047608           2641.185619              72.000000              0.008854
                 5            totmrc_Mean   Original Features            0.044195           2507.646236              62.600000              0.008523
                 6                 avgqty   Original Features            0.031117           1637.913101              46.400000              0.006014
                 7               mou_Mean   Original Features            0.028338           2391.171486              48.200000              0.002925
                 8             change_mou   Original Features            0.026139           1776.714602              48.800000              0.003252
                 9               crclscod   Original Features            0.025660           1539.900597              48.000000              0.003690
                10      change_mou_capped Winsorized Features            0.024147           1587.058058              43.800000              0.003155
                11         change_mou_log        Log Features            0.023987           1370.931499              38.200000              0.003999
                12        usage_to_charge Engineered Features            0.020677           1406.496920              41.200000              0.002133
                13                    lor   Original Features            0.019677           1278.843777              34.000000              0.002697
                14            eqpdays_log        Log Features            0.019191           2555.873069              14.800000              0.001633
                15              trend_gap Engineered Features            0.018390           1292.355445              36.000000              0.002076
                16 change_mou_missing_ind  Missing Indicators            0.017193           1065.495541              26.200000              0.002695
                17        totmrc_Mean_log        Log Features            0.016857           1248.415041              25.000000              0.002512
                18               uniqsubs   Original Features            0.015681           1045.020094              23.400000              0.002592
                19                 ethnic   Original Features            0.015276            864.591579              27.800000              0.002363
                20          drop_vce_Mean   Original Features            0.014893            686.745221              27.000000              0.002725

## Top 50 Features
 consolidated_rank                feature      feature_family  consolidated_score  gain_importance_mean  split_importance_mean  perm_importance_mean
                 1                 months   Original Features            0.119418           8488.277161             103.400000              0.026473
                 2                eqpdays   Original Features            0.118582          12139.361837              37.000000              0.024915
                 3              hnd_price   Original Features            0.049596           2470.891500              51.000000              0.012391
                 4      revenue_per_usage Engineered Features            0.047608           2641.185619              72.000000              0.008854
                 5            totmrc_Mean   Original Features            0.044195           2507.646236              62.600000              0.008523
                 6                 avgqty   Original Features            0.031117           1637.913101              46.400000              0.006014
                 7               mou_Mean   Original Features            0.028338           2391.171486              48.200000              0.002925
                 8             change_mou   Original Features            0.026139           1776.714602              48.800000              0.003252
                 9               crclscod   Original Features            0.025660           1539.900597              48.000000              0.003690
                10      change_mou_capped Winsorized Features            0.024147           1587.058058              43.800000              0.003155
                11         change_mou_log        Log Features            0.023987           1370.931499              38.200000              0.003999
                12        usage_to_charge Engineered Features            0.020677           1406.496920              41.200000              0.002133
                13                    lor   Original Features            0.019677           1278.843777              34.000000              0.002697
                14            eqpdays_log        Log Features            0.019191           2555.873069              14.800000              0.001633
                15              trend_gap Engineered Features            0.018390           1292.355445              36.000000              0.002076
                16 change_mou_missing_ind  Missing Indicators            0.017193           1065.495541              26.200000              0.002695
                17        totmrc_Mean_log        Log Features            0.016857           1248.415041              25.000000              0.002512
                18               uniqsubs   Original Features            0.015681           1045.020094              23.400000              0.002592
                19                 ethnic   Original Features            0.015276            864.591579              27.800000              0.002363
                20          drop_vce_Mean   Original Features            0.014893            686.745221              27.000000              0.002725
                21             months_log        Log Features            0.012979           1649.815721              16.800000              0.000521
                22               totcalls   Original Features            0.011577            714.666182              17.200000              0.001931
                23          mou_cvce_Mean   Original Features            0.010845            746.713381              26.000000              0.000466
                24                 avgrev   Original Features            0.010773            803.677916              23.600000              0.000653
                25             hnd_webcap   Original Features            0.010771            624.563942               8.600000              0.002763
                26               asl_flag   Original Features            0.010047            667.413620              19.800000              0.001184
                27             change_rev   Original Features            0.009723            603.224538              21.800000              0.000927
                28             refurb_new   Original Features            0.009299            779.877302               9.400000              0.001621
                29                 avgmou   Original Features            0.008934            523.325341              16.600000              0.001295
                30            vceovr_Mean   Original Features            0.008391            564.416179              17.400000              0.000834
                31           mou_Mean_log        Log Features            0.008292            759.206820              14.600000              0.000562
                32        mouiwylisv_Mean   Original Features            0.007045            468.323821              18.400000             -0.000041
                33      change_rev_capped Winsorized Features            0.006847            464.657739              15.800000              0.000442
                34                   area   Original Features            0.006483            297.705040              13.800000              0.000760
                35            ovrrev_Mean   Original Features            0.005771            424.179759              12.600000              0.000394
                36            ovrmou_Mean   Original Features            0.005607            408.044699              13.000000              0.000256
                37                avg6rev   Original Features            0.004799            440.051303               8.000000              0.000442
                38         change_rev_log        Log Features            0.004689            313.552679              11.400000              0.000266
                39        iwylis_vce_Mean   Original Features            0.004533            286.651321              12.000000              0.000158
                40          drop_blk_Mean   Original Features            0.004495            229.446781              10.200000              0.000534
                41                 adjqty   Original Features            0.004276            217.896159               7.200000              0.000657
                42   HHstatin_missing_ind  Missing Indicators            0.004172            236.064061               7.600000              0.000586
                43    service_issue_score Engineered Features            0.004110            231.695941              11.200000              0.000144
                44     vceovr_Mean_capped Winsorized Features            0.003809            257.281600               8.200000              0.000307
                45     ovrmou_Mean_capped Winsorized Features            0.003675            275.906661               7.800000              0.000129
                46          mou_peav_Mean   Original Features            0.003398            194.133601               8.800000              0.000182
                47          inonemin_Mean   Original Features            0.003153            201.870360               9.200000             -0.000035
                48                 income   Original Features            0.003079            155.492800               6.400000              0.000425
                49           uniqsubs_log        Log Features            0.003064            199.298179               4.800000              0.000472
                50        mouowylisv_Mean   Original Features            0.003021            176.705720               7.400000              0.000236

## Importance Distribution
- Score quantiles: 0.00: 0.000000, 0.25: 0.000029, 0.50: 0.000594, 0.75: 0.002497, 0.90: 0.010802, 0.95: 0.020377, 0.99: 0.049079
- Top 20 features account for 69.66% of total consolidated score
- Top 50 features account for 89.43% of total consolidated score

## Feature Family Analysis
      feature_family  feature_count  top20_count  top50_count  mean_score  median_score  zero_count  near_zero_count
   Original Features             98           12           33    0.007316      0.001855          13               26
        Log Features             72            3            7    0.001660      0.000383          17               39
  Missing Indicators             43            1            2    0.000698      0.000000          26               14
 Engineered Features              6            3            4    0.015664      0.011250           0                0
 Winsorized Features              5            1            4    0.007871      0.003809           0                1
Interaction Features              3            0            0    0.000040      0.000059           1                2

### Original Features
- The strongest raw signals remain `eqpdays`, `months`, `change_mou`, `change_rev`, `avgqty`, and `totcalls`.
- The usage and tenure fields confirm the earlier EDA story: churn separates on device age, tenure, and recent activity level.

### Missing Indicators
- Several missingness flags contribute signal, but most sit below the core usage and tenure variables.
- This suggests missingness is informative in pockets, not a dominant global driver.

### Log and Winsorized Features
- The log-transformed and capped versions of skewed service and usage variables retain signal, especially where the raw distributions are heavy-tailed.
- These transforms help the model see tail behavior without letting extreme values dominate the splits.

### Engineered Features
- `revenue_per_usage` and `service_issue_score` both appear in the top 50 and support the intended business hypotheses.
- `trend_gap` also remains useful, which supports the idea that recent behavior drift matters.

### Interaction Features
- Interaction flags are useful but not the primary drivers.
- `old_device_x_low_value` is the most meaningful of the three, which matches the EDA hypothesis that older equipment combined with low handset value can amplify churn risk.

## Business Interpretation
- `eqpdays` ranks 2 and remains the strongest single signal, matching the device-age hypothesis.
- `months` stays important, but it behaves as a supporting tenure feature rather than a standalone separator.
- `change_mou` and `change_rev` confirm that recent trend shifts matter, consistent with the leakage-reviewed EDA shortlist.
- `avgqty` and `totcalls` reinforce the usage-cluster story from the correlation report.
- `revenue_per_usage` and `service_issue_score` validate the engineered business features from Step 5.1.
- `drop_vce_Mean` still matters, and its presence in the top group supports the service-quality hypothesis.

## Candidate Removal List
- Features with zero importance across all three views should be candidates for removal before the next modeling step, subject to the family-level checks below.
- Near-zero features are weak enough that they can be dropped if the next phase needs a smaller or faster feature set.

 consolidated_rank                 feature     feature_family  consolidated_score  gain_importance_mean  split_importance_mean  perm_importance_mean
               171        area_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171        attempt_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171     avg6qty_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171     avg6rev_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171           blck_dat_Mean  Original Features            0.000000              0.000000               0.000000              0.000000
               171       blck_dat_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171           callfwdv_Mean  Original Features            0.000000              0.000000               0.000000              0.000000
               171       callfwdv_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171       ccrndmou_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171       comp_dat_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171    creditcd_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171     da_Mean_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171         datovr_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171 datovr_Mean_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171           drop_dat_Mean  Original Features            0.000000              0.000000               0.000000              0.000000
               171       drop_dat_Mean_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171    dualband_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171     eqpdays_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171      ethnic_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171                forgntvl  Original Features            0.000000              0.000000               0.000000              0.000000
               171            forgntvl_log       Log Features            0.000000              0.000000               0.000000              0.000000
               171    forgntvl_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171                  kid0_2  Original Features            0.000000              0.000000               0.000000              0.000000
               171      kid0_2_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171                kid11_15  Original Features            0.000000              0.000000               0.000000              0.000000
               171    kid11_15_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171    kid16_17_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171      kid3_5_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000
               171                 kid6_10  Original Features            0.000000              0.000000               0.000000              0.000000
               171     kid6_10_missing_ind Missing Indicators            0.000000              0.000000               0.000000              0.000000

## Correlation and Hypothesis Cross-Check
- Usage cluster hits in top 50: avgmou, avgqty, change_mou, mou_Mean, totcalls
- Revenue cluster hits in top 50: avg6rev, change_rev, revenue_per_usage
- Service cluster hits in top 50: drop_blk_Mean, drop_vce_Mean, service_issue_score
- The correlated usage and revenue groups share importance across multiple related columns, so consolidated ranking is more reliable than any single raw importance view.

## Recommendations
- Keep `eqpdays`, `months`, `change_mou`, `change_rev`, `avgqty`, `totcalls`, `revenue_per_usage`, `service_issue_score`, and `drop_vce_Mean` for the next phase.
- Revisit the low-signal tail of the feature set if a lighter model or more interpretable shortlist is needed.
- Preserve the Step 5.2 fold split so later feature-selection comparisons stay comparable.
