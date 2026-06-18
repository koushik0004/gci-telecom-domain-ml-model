# FEATURE VALIDATION

A lightweight RandomForestClassifier was trained on the current E8 feature set after one-to-one encoding of categorical columns and median imputation of numeric gaps.

- Rows used: 100000
- Features evaluated: 107
- Holdout ROC-AUC: 0.6710
- Holdout accuracy: 0.6175
- Permutation sample size: 3000

## Top 30 Features

```text
 validation_rank           feature  validation_score  tree_importance  perm_importance_mean  perm_importance_std  tree_rank  perm_rank
               1           eqpdays          0.175976         0.097844              0.028829             0.004749          1          1
               2            months          0.118709         0.083172              0.017499             0.000352          2          2
               3        change_mou          0.043356         0.038063              0.005519             0.002582          3          4
               4            avgqty          0.036317         0.020683              0.005894             0.000258         11          3
               5       totmrc_Mean          0.032245         0.026175              0.004347             0.000521          5          5
               6          totcalls          0.025781         0.017887              0.003820             0.000204         14          6
               7            adjqty          0.024440         0.016669              0.003654             0.000137         17          7
               8 revenue_per_usage          0.024201         0.025874              0.002556             0.001050          6         11
               9            avgmou          0.022830         0.017600              0.003184             0.000583         15         10
              10       ovrmou_Mean          0.022689         0.013816              0.003581             0.000346         25          8
              11               lor          0.020756         0.011570              0.003397             0.000969         29          9
              12          mou_Mean          0.020021         0.025040              0.001702             0.000002          7         14
              13         hnd_price          0.018843         0.030647              0.000798             0.001443          4         29
              14       vceovr_Mean          0.016203         0.013089              0.002191             0.000649         27         13
              15        change_rev          0.016101         0.017907              0.001622             0.000157         13         15
              16            adjrev          0.015825         0.024469              0.000815             0.000184          9         26
              17          uniqsubs          0.014662         0.008242              0.002392             0.000024         50         12
              18       ovrrev_Mean          0.012990         0.013041              0.001468             0.000031         28         18
              19            totmou          0.012913         0.017251              0.000973             0.000160         16         23
              20            totrev          0.012438         0.024877             -0.000268             0.000242          8         80
              21         trend_gap          0.012356         0.016225              0.000963             0.001550         18         24
              22     mou_peav_Mean          0.012146         0.014319              0.001131             0.000064         23         19
              23            adjmou          0.012115         0.015157              0.001029             0.000394         21         20
              24            avgrev          0.011788         0.018613              0.000563             0.000411         12         35
              25   usage_to_charge          0.011721         0.021059              0.000270             0.000097         10         44
              26     drop_vce_Mean          0.011612         0.009713              0.001533             0.000617         42         17
              27     mou_opkv_Mean          0.011241         0.013808              0.000984             0.000548         26         22
              28            phones          0.010848         0.008086              0.001544             0.000184         51         16
              29     mou_cvce_Mean          0.010794         0.015654              0.000673             0.000272         20         33
              30           avg6qty          0.009255         0.011363              0.000811             0.000134         31         27
```
