# FEATURE DICTIONARY

- Final row count: 100000
- Final feature count: 107
- Target column: churn
- Excluded columns: none

## Feature Type Summary

          feature_type  count  pct_of_columns  null_count  null_pct                                       example_columns
    numeric predictors     86           79.63      154290      1.79 rev_Mean, mou_Mean, totmrc_Mean, da_Mean, ovrmou_Mean
categorical predictors     21           19.44      195400      9.30  new_cell, crclscod, asl_flag, prizm_social_one, area
                target      1            0.93           0      0.00                                                 churn

## Dictionary

                 feature   dtype feature_type      role governance_type  included_in_model_ready
                rev_Mean float64      numeric predictor     conditional                     True
                mou_Mean float64      numeric predictor     conditional                     True
             totmrc_Mean float64      numeric predictor     conditional                     True
                 da_Mean float64      numeric predictor     conditional                     True
             ovrmou_Mean float64      numeric predictor     conditional                     True
             ovrrev_Mean float64      numeric predictor     conditional                     True
             vceovr_Mean float64      numeric predictor     conditional                     True
             datovr_Mean float64      numeric predictor     conditional                     True
               roam_Mean float64      numeric predictor     conditional                     True
              change_mou float64      numeric predictor     conditional                     True
              change_rev float64      numeric predictor     conditional                     True
           drop_vce_Mean float64      numeric predictor     conditional                     True
           drop_dat_Mean float64      numeric predictor     conditional                     True
           blck_vce_Mean float64      numeric predictor     conditional                     True
           blck_dat_Mean float64      numeric predictor     conditional                     True
           unan_vce_Mean float64      numeric predictor     conditional                     True
           unan_dat_Mean float64      numeric predictor     conditional                     True
           plcd_vce_Mean float64      numeric predictor     conditional                     True
           plcd_dat_Mean float64      numeric predictor     conditional                     True
           recv_vce_Mean float64      numeric predictor     conditional                     True
           recv_sms_Mean float64      numeric predictor     conditional                     True
           comp_vce_Mean float64      numeric predictor     conditional                     True
           comp_dat_Mean float64      numeric predictor     conditional                     True
           custcare_Mean float64      numeric predictor     conditional                     True
           ccrndmou_Mean float64      numeric predictor     conditional                     True
             cc_mou_Mean float64      numeric predictor     conditional                     True
           inonemin_Mean float64      numeric predictor     conditional                     True
           threeway_Mean float64      numeric predictor     conditional                     True
           mou_cvce_Mean float64      numeric predictor     conditional                     True
           mou_cdat_Mean float64      numeric predictor     conditional                     True
           mou_rvce_Mean float64      numeric predictor     conditional                     True
         owylis_vce_Mean float64      numeric predictor     conditional                     True
         mouowylisv_Mean float64      numeric predictor     conditional                     True
         iwylis_vce_Mean float64      numeric predictor     conditional                     True
         mouiwylisv_Mean float64      numeric predictor     conditional                     True
           peak_vce_Mean float64      numeric predictor     conditional                     True
           peak_dat_Mean float64      numeric predictor     conditional                     True
           mou_peav_Mean float64      numeric predictor     conditional                     True
           mou_pead_Mean float64      numeric predictor     conditional                     True
            opk_vce_Mean float64      numeric predictor     conditional                     True
            opk_dat_Mean float64      numeric predictor     conditional                     True
           mou_opkv_Mean float64      numeric predictor     conditional                     True
           mou_opkd_Mean float64      numeric predictor     conditional                     True
           drop_blk_Mean float64      numeric predictor     conditional                     True
            attempt_Mean float64      numeric predictor     conditional                     True
           complete_Mean float64      numeric predictor     conditional                     True
           callfwdv_Mean float64      numeric predictor     conditional                     True
           callwait_Mean float64      numeric predictor     conditional                     True
                   churn   int64       target    target         unknown                     True
                  months   int64      numeric predictor            safe                     True
                uniqsubs   int64      numeric predictor            safe                     True
                actvsubs   int64      numeric predictor            safe                     True
                new_cell     str  categorical predictor            safe                     True
                crclscod     str  categorical predictor            safe                     True
                asl_flag     str  categorical predictor            safe                     True
                totcalls   int64      numeric predictor     conditional                     True
                  totmou float64      numeric predictor     conditional                     True
                  totrev float64      numeric predictor     conditional                     True
                  adjrev float64      numeric predictor     conditional                     True
                  adjmou float64      numeric predictor     conditional                     True
                  adjqty   int64      numeric predictor     conditional                     True
                  avgrev float64      numeric predictor     conditional                     True
                  avgmou float64      numeric predictor     conditional                     True
                  avgqty float64      numeric predictor     conditional                     True
                 avg3mou   int64      numeric predictor     conditional                     True
                 avg3qty   int64      numeric predictor     conditional                     True
                 avg3rev   int64      numeric predictor     conditional                     True
                 avg6mou float64      numeric predictor     conditional                     True
                 avg6qty float64      numeric predictor     conditional                     True
                 avg6rev float64      numeric predictor     conditional                     True
        prizm_social_one     str  categorical predictor            safe                     True
                    area     str  categorical predictor            safe                     True
                dualband     str  categorical predictor            safe                     True
              refurb_new     str  categorical predictor            safe                     True
               hnd_price float64      numeric predictor            safe                     True
                  phones float64      numeric predictor            safe                     True
                  models float64      numeric predictor            safe                     True
              hnd_webcap     str  categorical predictor            safe                     True
                   truck float64      numeric predictor            safe                     True
                      rv float64      numeric predictor            safe                     True
                 ownrent     str  categorical predictor            safe                     True
                     lor float64      numeric predictor            safe                     True
                dwlltype     str  categorical predictor            safe                     True
                 marital     str  categorical predictor            safe                     True
                  adults float64      numeric predictor            safe                     True
                infobase     str  categorical predictor            safe                     True
                  income float64      numeric predictor            safe                     True
                numbcars float64      numeric predictor            safe                     True
                HHstatin     str  categorical predictor            safe                     True
                dwllsize     str  categorical predictor            safe                     True
                forgntvl float64      numeric predictor            safe                     True
                  ethnic     str  categorical predictor            safe                     True
                  kid0_2     str  categorical predictor            safe                     True
                  kid3_5     str  categorical predictor            safe                     True
                 kid6_10     str  categorical predictor            safe                     True
                kid11_15     str  categorical predictor            safe                     True
                kid16_17     str  categorical predictor            safe                     True
                creditcd     str  categorical predictor            safe                     True
                 eqpdays float64      numeric predictor            safe                     True
         usage_to_charge float64      numeric predictor      not_listed                     True
       revenue_per_usage float64      numeric predictor      not_listed                     True
               trend_gap float64      numeric predictor      not_listed                     True
             revenue_gap float64      numeric predictor      not_listed                     True
     service_issue_score float64      numeric predictor      not_listed                     True
       support_intensity float64      numeric predictor      not_listed                     True
 low_usage_x_high_charge   int64      numeric predictor      not_listed                     True
  old_device_x_low_value   int64      numeric predictor      not_listed                     True
low_usage_x_poor_service   int64      numeric predictor      not_listed                     True
