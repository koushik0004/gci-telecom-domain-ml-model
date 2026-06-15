# Phase 5 - Model Development
## Step 5.5 - Feature Selection

## Objective
Reduce redundancy and low-value predictors before the next baseline retraining pass.

## Inputs
- Starting dataset: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v1.parquet`
- Feature importance report: `docs/5-model-building/report-feature-importance.md`
- Correlation cluster report: `docs/4-EDA-reports/correlation_cluster_report.md`
- Governance reference: `docs/4-EDA-reports/feature_governance.md`

## Selection Rule
- Remove all zero-importance features.
- Remove all near-zero importance features.
- For each correlation cluster, keep the highest-scoring surviving member and drop the redundant alternatives.
- Preserve the protected business signals `eqpdays`, `months`, and `change_mou` unless there is strong evidence to remove them.

## Count Summary
- Starting feature count: `227`
- Final feature count: `61`
- Removed features: `166`
- Output width including target: `62` columns

## Removal Summary
```text
    selection_reason  count
near_zero_importance     82
     zero_importance     57
   cluster_redundant     27
```

## Cluster Decisions
```text
cluster_theme  cluster_size representative_feature  representative_score  retained_count  removed_count                                                                                                                                                                                                                                                                         removed_members
        usage            22                 avgqty              0.031117               1             21 attempt_Mean; avg3mou; avg3qty; avg6mou; avg6qty; avgmou; comp_vce_Mean; complete_Mean; inonemin_Mean; mou_Mean; mou_cvce_Mean; mou_opkv_Mean; mou_peav_Mean; mou_rvce_Mean; mouowylisv_Mean; opk_vce_Mean; owylis_vce_Mean; peak_vce_Mean; plcd_vce_Mean; recv_vce_Mean; unan_vce_Mean
      revenue             6               totcalls              0.011577               1              5                                                                                                                                                                                                                                                  adjmou; adjqty; adjrev; totmou; totrev
      service             4                   None                   NaN               0              4                                                                                                                                                                                                                               comp_dat_Mean; opk_dat_Mean; peak_dat_Mean; plcd_dat_Mean
      support             3          custcare_Mean              0.002114               1              2                                                                                                                                                                                                                                                              cc_mou_Mean; ccrndmou_Mean
    service_2             2                   None                   NaN               0              2                                                                                                                                                                                                                                                            mou_cdat_Mean; mou_opkd_Mean
  revenue_aux             4                 avgrev              0.010773               1              3                                                                                                                                                                                                                                                              avg3rev; avg6rev; rev_Mean
      overage             3            vceovr_Mean              0.008391               1              2                                                                                                                                                                                                                                                                ovrmou_Mean; ovrrev_Mean
      quality             2          drop_blk_Mean              0.004495               1              1                                                                                                                                                                                                                                                                           blck_vce_Mean
       device             2                 phones              0.001486               1              1                                                                                                                                                                                                                                                                                  models
```

## Top Retained Features
```text
 consolidated_rank                feature      feature_family  consolidated_score
                 1                 months   Original Features            0.119418
                 2                eqpdays   Original Features            0.118582
                 3              hnd_price   Original Features            0.049596
                 4      revenue_per_usage Engineered Features            0.047608
                 5            totmrc_Mean   Original Features            0.044195
                 6                 avgqty   Original Features            0.031117
                 8             change_mou   Original Features            0.026139
                 9               crclscod   Original Features            0.025660
                10      change_mou_capped Winsorized Features            0.024147
                11         change_mou_log        Log Features            0.023987
                12        usage_to_charge Engineered Features            0.020677
                13                    lor   Original Features            0.019677
                14            eqpdays_log        Log Features            0.019191
                15              trend_gap Engineered Features            0.018390
                16 change_mou_missing_ind  Missing Indicators            0.017193
                17        totmrc_Mean_log        Log Features            0.016857
                18               uniqsubs   Original Features            0.015681
                19                 ethnic   Original Features            0.015276
                20          drop_vce_Mean   Original Features            0.014893
                21             months_log        Log Features            0.012979
```

## Expected Benefits
- Lower redundancy across usage, revenue, support, quality, and device signals.
- Smaller feature space for the Step 5.6 retraining comparison.
- Cleaner interpretation because the strongest member from each correlated family is retained instead of the full cluster.
- Protected business drivers remain in the modeling set for continuity with the EDA hypotheses.

## Deliverables
- Parquet: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/data/intermediate/modeling_dataset_v2.parquet`
- Summary CSV: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/telecom/feature_selection_summary.csv`
- Notebook: `/Users/koushiksadhukhan/projects/gci-telecom-domain-ml-model/Final Assignment/matsuo_final_assignment.ipynb`
