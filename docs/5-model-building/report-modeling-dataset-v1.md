# Phase 5 - Model Development
## Step 5.1 - Modeling Dataset Creation

## Validation

- Row count: 100000
- Column count: 228
- Target column present: True
- Missing values remaining: 0
- Row count unchanged: True
- Customer_ID removed: True

## Target Distribution

 churn  count   pct
     0  50438 50.44
     1  49562 49.56

## Transformation Summary

             component  count                                                  notes
    missing indicators     43 Created for features with missingness before treatment
   winsorized features      5      1st/99th percentile caps saved as _capped columns
     skew log features     72                 log1p transforms saved as _log columns
feature engineering v1      6         usage/revenue/service/support derived features
  interaction features      3                quartile-based binary interaction flags

- Overlap features with both winsorization and skew treatment: change_mou, change_rev, ovrmou_Mean, roam_Mean, vceovr_Mean
- Total newly created columns: 129

## Final Schema Summary

          feature_type  count  pct_of_columns  null_count  null_pct                                       example_columns
    numeric predictors    206           90.35           0       0.0 rev_Mean, mou_Mean, totmrc_Mean, da_Mean, ovrmou_Mean
categorical predictors     21            9.21           0       0.0  new_cell, crclscod, asl_flag, prizm_social_one, area
                target      1            0.44           0       0.0                                                 churn

## Newly Created Columns

                family           source_feature               created_column                                         notes
     missing_indicator                 rev_Mean         rev_Mean_missing_ind                                        median
     missing_indicator                 mou_Mean         mou_Mean_missing_ind                                        median
     missing_indicator              totmrc_Mean      totmrc_Mean_missing_ind                                        median
     missing_indicator                  da_Mean          da_Mean_missing_ind                                        median
     missing_indicator              ovrmou_Mean      ovrmou_Mean_missing_ind                                        median
     missing_indicator              ovrrev_Mean      ovrrev_Mean_missing_ind                                        median
     missing_indicator              vceovr_Mean      vceovr_Mean_missing_ind                                        median
     missing_indicator              datovr_Mean      datovr_Mean_missing_ind                                        median
     missing_indicator                roam_Mean        roam_Mean_missing_ind                                        median
     missing_indicator               change_mou       change_mou_missing_ind                                        median
     missing_indicator               change_rev       change_rev_missing_ind                                        median
     missing_indicator                  avg6mou          avg6mou_missing_ind                                        median
     missing_indicator                  avg6qty          avg6qty_missing_ind                                        median
     missing_indicator                  avg6rev          avg6rev_missing_ind                                        median
     missing_indicator         prizm_social_one prizm_social_one_missing_ind                                       MISSING
     missing_indicator                     area             area_missing_ind                                       MISSING
     missing_indicator                 dualband         dualband_missing_ind                                       MISSING
     missing_indicator               refurb_new       refurb_new_missing_ind                                       MISSING
     missing_indicator                hnd_price        hnd_price_missing_ind                                        median
     missing_indicator                   phones           phones_missing_ind                                        median
     missing_indicator                   models           models_missing_ind                                        median
     missing_indicator               hnd_webcap       hnd_webcap_missing_ind                                       MISSING
     missing_indicator                    truck            truck_missing_ind                                        median
     missing_indicator                       rv               rv_missing_ind                                        median
     missing_indicator                  ownrent          ownrent_missing_ind                                       MISSING
     missing_indicator                      lor              lor_missing_ind                                        median
     missing_indicator                 dwlltype         dwlltype_missing_ind                                       MISSING
     missing_indicator                  marital          marital_missing_ind                                       MISSING
     missing_indicator                   adults           adults_missing_ind                                        median
     missing_indicator                 infobase         infobase_missing_ind                                       MISSING
     missing_indicator                   income           income_missing_ind                                        median
     missing_indicator                 numbcars         numbcars_missing_ind                                        median
     missing_indicator                 HHstatin         HHstatin_missing_ind                                       MISSING
     missing_indicator                 dwllsize         dwllsize_missing_ind                                       MISSING
     missing_indicator                 forgntvl         forgntvl_missing_ind                                        median
     missing_indicator                   ethnic           ethnic_missing_ind                                       MISSING
     missing_indicator                   kid0_2           kid0_2_missing_ind                                       MISSING
     missing_indicator                   kid3_5           kid3_5_missing_ind                                       MISSING
     missing_indicator                  kid6_10          kid6_10_missing_ind                                       MISSING
     missing_indicator                 kid11_15         kid11_15_missing_ind                                       MISSING
     missing_indicator                 kid16_17         kid16_17_missing_ind                                       MISSING
     missing_indicator                 creditcd         creditcd_missing_ind                                       MISSING
     missing_indicator                  eqpdays          eqpdays_missing_ind                                        median
    winsorized_feature               change_mou            change_mou_capped                       clip_change_mou_p01_p99
    winsorized_feature               change_rev            change_rev_capped                       clip_change_rev_p01_p99
    winsorized_feature                roam_Mean             roam_Mean_capped                        clip_roam_Mean_p01_p99
    winsorized_feature              vceovr_Mean           vceovr_Mean_capped                      clip_vceovr_Mean_p01_p99
    winsorized_feature              ovrmou_Mean           ovrmou_Mean_capped                      clip_ovrmou_Mean_p01_p99
              skew_log            blck_dat_Mean            blck_dat_Mean_log                                         log1p
              skew_log         roam_Mean_capped                roam_Mean_log                                         log1p
              skew_log            recv_sms_Mean            recv_sms_Mean_log                                         log1p
              skew_log            drop_dat_Mean            drop_dat_Mean_log                                         log1p
              skew_log            unan_dat_Mean            unan_dat_Mean_log                                         log1p
              skew_log            mou_opkd_Mean            mou_opkd_Mean_log                                         log1p
              skew_log                 uniqsubs                 uniqsubs_log                                         log1p
              skew_log            callfwdv_Mean            callfwdv_Mean_log                                         log1p
              skew_log              datovr_Mean              datovr_Mean_log                                         log1p
              skew_log            mou_cdat_Mean            mou_cdat_Mean_log                                         log1p
              skew_log        change_rev_capped               change_rev_log                                 log1p_shifted
              skew_log            mou_pead_Mean            mou_pead_Mean_log                                         log1p
              skew_log            custcare_Mean            custcare_Mean_log                                         log1p
              skew_log            plcd_dat_Mean            plcd_dat_Mean_log                                         log1p
              skew_log             opk_dat_Mean             opk_dat_Mean_log                                         log1p
              skew_log            comp_dat_Mean            comp_dat_Mean_log                                         log1p
              skew_log            peak_dat_Mean            peak_dat_Mean_log                                         log1p
              skew_log            threeway_Mean            threeway_Mean_log                                         log1p
              skew_log            ccrndmou_Mean            ccrndmou_Mean_log                                         log1p
              skew_log            callwait_Mean            callwait_Mean_log                                         log1p
              skew_log              cc_mou_Mean              cc_mou_Mean_log                                         log1p
              skew_log                  da_Mean                  da_Mean_log                                         log1p
              skew_log                 rev_Mean                 rev_Mean_log                                 log1p_shifted
              skew_log            inonemin_Mean            inonemin_Mean_log                                         log1p
              skew_log            blck_vce_Mean            blck_vce_Mean_log                                         log1p
              skew_log       ovrmou_Mean_capped              ovrmou_Mean_log                                         log1p
              skew_log          mouiwylisv_Mean          mouiwylisv_Mean_log                                         log1p
              skew_log            drop_blk_Mean            drop_blk_Mean_log                                         log1p
              skew_log              ovrrev_Mean              ovrrev_Mean_log                                         log1p
              skew_log                 actvsubs                 actvsubs_log                                         log1p
              skew_log          mouowylisv_Mean          mouowylisv_Mean_log                                         log1p
              skew_log                 totcalls                 totcalls_log                                         log1p
              skew_log       vceovr_Mean_capped              vceovr_Mean_log                                         log1p
              skew_log                   adjqty                   adjqty_log                                         log1p
              skew_log            recv_vce_Mean            recv_vce_Mean_log                                         log1p
              skew_log          iwylis_vce_Mean          iwylis_vce_Mean_log                                         log1p
              skew_log                  avg3rev                  avg3rev_log                                         log1p
              skew_log            drop_vce_Mean            drop_vce_Mean_log                                         log1p
              skew_log            unan_vce_Mean            unan_vce_Mean_log                                         log1p
              skew_log                   totrev                   totrev_log                                         log1p
              skew_log                   adjrev                   adjrev_log                                         log1p
              skew_log                   totmou                   totmou_log                                         log1p
              skew_log                  avg6rev                  avg6rev_log                                 log1p_shifted
              skew_log                   adjmou                   adjmou_log                                         log1p
              skew_log          owylis_vce_Mean          owylis_vce_Mean_log                                         log1p
              skew_log                   avgrev                   avgrev_log                                         log1p
              skew_log             opk_vce_Mean             opk_vce_Mean_log                                         log1p
              skew_log            mou_rvce_Mean            mou_rvce_Mean_log                                         log1p
              skew_log            mou_opkv_Mean            mou_opkv_Mean_log                                         log1p
              skew_log            peak_vce_Mean            peak_vce_Mean_log                                         log1p
              skew_log                   avgqty                   avgqty_log                                         log1p
              skew_log                   phones                   phones_log                                         log1p
              skew_log                  avg6qty                  avg6qty_log                                         log1p
              skew_log        change_mou_capped               change_mou_log                                 log1p_shifted
              skew_log            mou_peav_Mean            mou_peav_Mean_log                                         log1p
              skew_log                  avg3qty                  avg3qty_log                                         log1p
              skew_log              totmrc_Mean              totmrc_Mean_log                                 log1p_shifted
              skew_log            comp_vce_Mean            comp_vce_Mean_log                                         log1p
              skew_log            complete_Mean            complete_Mean_log                                         log1p
              skew_log            plcd_vce_Mean            plcd_vce_Mean_log                                         log1p
              skew_log             attempt_Mean             attempt_Mean_log                                         log1p
              skew_log            mou_cvce_Mean            mou_cvce_Mean_log                                         log1p
              skew_log                   models                   models_log                                         log1p
              skew_log                   avgmou                   avgmou_log                                         log1p
              skew_log                   months                   months_log                                         log1p
              skew_log                 mou_Mean                 mou_Mean_log                                         log1p
              skew_log                  avg6mou                  avg6mou_log                                         log1p
              skew_log                  avg3mou                  avg3mou_log                                         log1p
              skew_log                       rv                       rv_log                                         log1p
              skew_log                    truck                    truck_log                                         log1p
              skew_log                 forgntvl                 forgntvl_log                                         log1p
              skew_log                  eqpdays                  eqpdays_log                                 log1p_shifted
feature_engineering_v1          usage_to_charge              usage_to_charge                        mou_Mean / totmrc_Mean
feature_engineering_v1        revenue_per_usage            revenue_per_usage                     rev_Mean / (mou_Mean + 1)
feature_engineering_v1                trend_gap                    trend_gap                             avg3mou - avg6mou
feature_engineering_v1              revenue_gap                  revenue_gap                             avg3rev - avg6rev
feature_engineering_v1      service_issue_score          service_issue_score drop_vce_Mean + blck_vce_Mean + drop_blk_Mean
feature_engineering_v1        support_intensity            support_intensity   custcare_Mean + ccrndmou_Mean + cc_mou_Mean
   interaction_feature  low_usage_x_high_charge      low_usage_x_high_charge                           quartile_based_flag
   interaction_feature   old_device_x_low_value       old_device_x_low_value                           quartile_based_flag
   interaction_feature low_usage_x_poor_service     low_usage_x_poor_service                           quartile_based_flag
