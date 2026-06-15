# FEATURE VALIDATION

A lightweight RandomForestClassifier was trained on the current E8 feature set after one-to-one encoding of categorical columns and median imputation of numeric gaps.

- Rows used: 100000
- Features evaluated: 107
- Holdout ROC-AUC: 0.6750
- Holdout accuracy: 0.6211
- Permutation sample size: 3000

## Top 30 Features

```text
 validation_rank             feature  validation_score  tree_importance  perm_importance_mean  perm_importance_std  tree_rank  perm_rank
               1             eqpdays          0.142083         0.089191              0.021366             0.003430          1          1
               2              months          0.135179         0.083635              0.020462             0.000688          2          2
               3          change_mou          0.054861         0.037910              0.007870             0.003680          3          3
               4              avgqty          0.038749         0.019723              0.006331             0.000406         10          4
               5              adjqty          0.024793         0.017210              0.003548             0.000451         12          5
               6            totcalls          0.022754         0.017059              0.003118             0.000386         14          7
               7         totmrc_Mean          0.021280         0.022879              0.002157             0.000589          7         13
               8                 lor          0.019916         0.010169              0.003251             0.000951         32          6
               9   revenue_per_usage          0.019348         0.024878              0.001514             0.000041          5         17
              10         ovrrev_Mean          0.018999         0.013234              0.002714             0.000157         24          9
              11       mou_cvce_Mean          0.018237         0.016588              0.002179             0.000343         16         12
              12            mou_Mean          0.018139         0.024229              0.001320             0.000280          6         19
              13            crclscod          0.018058         0.010847              0.002769             0.000055         30          8
              14              avgmou          0.017396         0.016630              0.001990             0.000458         15         14
              15         ovrmou_Mean          0.016819         0.013188              0.002241             0.000261         25         11
              16           hnd_price          0.014204         0.028409             -0.000568             0.001269          4        103
              17            uniqsubs          0.013876         0.007060              0.002267             0.000162         52         10
              18         vceovr_Mean          0.013758         0.012034              0.001697             0.000248         28         16
              19           trend_gap          0.012708         0.015585              0.001077             0.001418         18         23
              20       mou_opkv_Mean          0.011390         0.011457              0.001241             0.000127         29         21
              21            asl_flag          0.011343         0.004892              0.001950             0.000338         63         15
              22          change_rev          0.010903         0.016131              0.000622             0.000101         17         30
              23     usage_to_charge          0.010684         0.019341              0.000222             0.000008         11         48
              24              adjrev          0.010508         0.021017             -0.000304             0.000414          8         94
              25       drop_vce_Mean          0.010507         0.009072              0.001309             0.000139         41         20
              26              totrev          0.010431         0.020862             -0.000247             0.000477          9         92
              27 service_issue_score          0.010356         0.008517              0.001336             0.000127         47         18
              28              avgrev          0.009972         0.017174              0.000304             0.000017         13         41
              29       inonemin_Mean          0.009358         0.008336              0.001137             0.000352         49         22
              30              totmou          0.009188         0.014717              0.000401             0.000122         19         39
```
