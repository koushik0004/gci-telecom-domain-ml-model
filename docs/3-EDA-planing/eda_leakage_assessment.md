# Leakage Review

This review checks whether any feature could expose information from the churn window or after the prediction point. The dataset is customer-level and the label is defined as churn occurring between 31 and 60 days after the observation date, so only features measured strictly before that point are safe for modeling.

The main conclusion is that there is no obvious direct label leakage from the column names alone. The real risk is timing ambiguity in derived historical features, especially the rolling windows and change variables.

## Core Readout

- `Customer_ID` is an identifier only and must never be used as a predictive feature.
- `churn` is the target and must be excluded from predictors.
- Most profile, household, device, billing, usage, and service-quality variables look usable if they were recorded at the observation snapshot.
- The highest-risk fields are the time-windowed and trend features: `change_mou`, `change_rev`, `avg3*`, `avg6*`, and `months`.
- Two columns remain under-documented in the schema and should be validated for semantics before modeling: `recv_sms_Mean` and `iwylis_vce_Mean`.

# Feature Timing Assessment

| Feature group | Examples | Timing assessment | Reason |
|---|---|---|---|
| Static customer and household descriptors | `area`, `ownrent`, `dwlltype`, `dwllsize`, `HHstatin`, `income`, `marital`, `ethnic`, `prizm_social_one`, `asl_flag` | Likely safe | These describe customer context rather than future behavior. |
| Device and subscription attributes | `hnd_price`, `hnd_webcap`, `dualband`, `refurb_new`, `new_cell`, `truck`, `rv`, `forgntvl`, `creditcd` | Likely safe | These are state variables available at the snapshot point if coded correctly. |
| Contemporaneous usage and billing metrics | `rev_Mean`, `mou_Mean`, `totmrc_Mean`, `da_Mean`, `ovrmou_Mean`, `ovrrev_Mean`, `drop_vce_Mean`, `drop_dat_Mean`, `blck_vce_Mean`, `blck_dat_Mean`, `custcare_Mean`, `attempt_Mean`, `complete_Mean` | Likely safe | These are behavioral summaries, but they are not inherently post-outcome unless the source window is wrong. |
| Rolling history features | `avg3mou`, `avg3qty`, `avg3rev`, `avg6mou`, `avg6qty`, `avg6rev` | Requires validation | They are windowed summaries and must be confirmed to end before the churn observation window. |
| Trend features | `change_mou`, `change_rev` | Requires validation | They compare recent behavior to earlier behavior, so the reference periods must be strictly pre-churn. |
| Tenure | `months` | Requires validation | Tenure is usually safe, but it must be measured at the observation date and not at a later account state. |
| Underdocumented fields | `recv_sms_Mean`, `iwylis_vce_Mean` | Requires validation | The schema does not fully define them, so they need semantic confirmation before they are trusted. |

# Safe Features

The following groups are the safest to keep in a first-pass model, assuming standard type cleanup and no hidden timestamp issues:

- `Customer_ID` should be retained only as a join key, not as a feature.
- Household and demographic fields: `area`, `ownrent`, `dwlltype`, `dwllsize`, `HHstatin`, `income`, `marital`, `ethnic`, `prizm_social_one`, `asl_flag`, `kid0_2`, `kid3_5`, `kid6_10`, `kid11_15`, `kid16_17`, `infobase`.
- Device and plan fields: `hnd_price`, `hnd_webcap`, `dualband`, `refurb_new`, `new_cell`, `truck`, `rv`, `forgntvl`, `creditcd`, `crclscod`.
- Core usage, billing, and service fields: `rev_Mean`, `mou_Mean`, `totmrc_Mean`, `da_Mean`, `ovrmou_Mean`, `ovrrev_Mean`, `vceovr_Mean`, `datovr_Mean`, `roam_Mean`, `drop_vce_Mean`, `drop_dat_Mean`, `blck_vce_Mean`, `blck_dat_Mean`, `unan_vce_Mean`, `unan_dat_Mean`, `plcd_vce_Mean`, `plcd_dat_Mean`, `recv_vce_Mean`, `comp_vce_Mean`, `comp_dat_Mean`, `custcare_Mean`, `ccrndmou_Mean`, `cc_mou_Mean`, `inonemin_Mean`, `threeway_Mean`, `mou_cvce_Mean`, `mou_cdat_Mean`, `mou_rvce_Mean`, `owylis_vce_Mean`, `mouowylisv_Mean`, `mouiwylisv_Mean`, `peak_vce_Mean`, `peak_dat_Mean`, `mou_peav_Mean`, `mou_pead_Mean`, `opk_vce_Mean`, `opk_dat_Mean`, `mou_opkv_Mean`, `mou_opkd_Mean`, `drop_blk_Mean`, `attempt_Mean`, `complete_Mean`, `callfwdv_Mean`, `callwait_Mean`.

These are safe in the leakage sense, but they still need ordinary preprocessing:

- numeric casting
- missing-value handling
- categorical encoding
- redundancy reduction for highly correlated fields

# Features Requiring Validation

These features are not automatically leaky, but they need explicit timing verification before they are used in the final model:

- `change_mou`
- `change_rev`
- `avg3mou`
- `avg3qty`
- `avg3rev`
- `avg6mou`
- `avg6qty`
- `avg6rev`
- `months`
- `recv_sms_Mean`
- `iwylis_vce_Mean`

Validation questions to answer:

- Are the rolling-window features measured strictly before the churn observation date?
- Are the `change_*` fields computed from periods that end before the churn window begins?
- Is `months` a true tenure-at-snapshot field, or could it reflect later account status?
- What exactly do `recv_sms_Mean` and `iwylis_vce_Mean` measure, and are they pre-outcome summaries?

# Potential Leakage Risks

The leakage risk is concentrated in feature timing, not in the label construction itself.

## Primary Risks

- If `change_mou` or `change_rev` uses activity from the churn window or later, the model will see information that would not be available at scoring time.
- If `avg3*` or `avg6*` windows overlap the churn window, they become future-looking summaries rather than predictors.
- If `months` is recorded after churn eligibility is already influenced by the label window, it can act as a post-outcome proxy.
- If any undocumented field is actually a later-cycle summary, it must be removed until its timing is proven safe.

## What Does Not Look Like Leakage

- `Customer_ID` is not a leakage feature, but it is an ID-only field and must be excluded.
- The regular usage, billing, household, and device fields do not appear to encode the churn label directly.
- The strong bivariate and multivariate signal in usage, revenue, and device age is consistent with legitimate predictive structure, not obvious target leakage.

# Modeling Recommendations

- Build a baseline model using only the clearly safe features first.
- Keep `change_mou`, `change_rev`, `avg3*`, `avg6*`, and `months` in a separate candidate set until their timing is confirmed.
- Run an ablation test:
  - model A: safe features only
  - model B: safe features plus validated temporal features
  - compare lift to quantify how much the time-windowed fields help
- Drop `Customer_ID` from all training matrices.
- Keep `churn` isolated as the label and never derive features from it.
- If the temporal features are validated, use regularization or feature selection to prevent the model from over-weighting redundant historical summaries.
- Document the feature timing decision for every derived field before model training begins.

## Bottom Line

There is no obvious direct leakage from the dataset structure, but the derived historical windows are the main governance risk. The conservative and correct approach is to treat `change_mou`, `change_rev`, `avg3*`, `avg6*`, and `months` as conditional features that only enter the model after timing validation.
