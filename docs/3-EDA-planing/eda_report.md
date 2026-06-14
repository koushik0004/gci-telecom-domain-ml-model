# Executive Summary

The telecom churn dataset is structurally sound for modeling: it contains 100,000 one-to-one customer records, a clean join key (`Customer_ID`), and a nearly balanced binary target (`churn` = 49.56%).

The strongest predictive signal comes from customer behavior and device context, not from demographics alone. In particular:

- device age and value matter, especially `eqpdays` and `hnd_price`
- declining usage and trend features matter, especially `mou_Mean`, `avg3mou`, and `change_mou`
- recent revenue and bill burden add useful separation, especially `totmrc_Mean`
- service trouble and support usage matter, but they are weaker than usage/device signals in raw form
- household and demographic fields help segmentation, but they are not the main churn drivers

The main implementation risk is not row integrity or target balance. It is feature readiness:

- `Client.csv` has heavy missingness in household fields
- many numeric variables are stored as text
- usage, revenue, and care variables are highly correlated
- time-windowed features such as `change_mou`, `change_rev`, `avg3*`, `avg6*`, and `months` need leakage validation before modeling

## High-Level Conclusions

- The data is good enough for supervised churn modeling.
- The most useful first-pass model should combine a compact set of behavioral, device, and service features.
- Missing indicators should be retained where possible because missingness itself is predictive.
- A leakage-aware feature review is required before final model training.

# Dataset Quality Assessment

## Structural Quality

| Check | Result | Interpretation |
|---|---|---|
| Source tables | `Client.csv`, `Record.csv` | Two customer-level tables with shared key `Customer_ID` |
| Row count | 100,000 in each table | Clean one-to-one structure |
| Merge result | 100,000 rows, 100 columns | No row loss in the analytical join |
| Duplicate IDs | 0 in both tables | No customer duplication |
| Target availability | `churn` in `Record.csv` | Labeled supervised problem |

## Data Type Quality

The raw CSVs are text-heavy and require semantic type cleanup.

| Issue | Examples | Required handling |
|---|---|---|
| Numeric stored as text | `totcalls`, `totmou`, `totrev`, `mou_Mean`, `eqpdays`, `months` | Cast to numeric before analysis |
| Coded binary fields | `asl_flag`, `dualband`, `hnd_webcap`, `creditcd`, `refurb_new`, `churn` | Recode explicitly |
| Categorical codes | `crclscod`, `area`, `prizm_social_one`, `ownrent`, `dwlltype`, `marital`, `ethnic` | Keep categorical |
| Identifier | `Customer_ID` | Keep only as join key |

## Distribution Quality

The dataset is not only skewed; many fields are heavily right-tailed and outlier-prone.

| Group | Main pattern |
|---|---|
| Revenue | Strong skew, heavy tails, clear outliers |
| Usage | Strong skew, heavy tails, clear outliers |
| Service quality | Extremely skewed, many zero-inflated fields |
| Household | Moderate skew, high missingness in several fields |

## Modeling Readiness

- Ready for modeling after type cleanup, missing-value strategy, and feature reduction
- Not ready for blind model fitting because correlated blocks are still dense
- Not ready for direct use of temporal features until timing is confirmed

# Missingness Insights

Missingness is concentrated in `Client.csv`, especially in household and demographic fields.

## Overall Missingness

| Dataset | Missing Cells | Missing Rate | Notes |
|---|---:|---:|---|
| `Client.csv` | 327,786 | 6.56% | Main missingness burden |
| `Record.csv` | 4,995 | 0.10% | Low and structured missingness |
| Combined raw tables | 332,781 | 3.29% | Mostly driven by `Client.csv` |

## Key Missingness Patterns

- `avg6mou`, `avg6qty`, `avg6rev` are missing together in 2,839 rows
- `creditcd`, `truck`, `rv`, `marital`, `forgntvl`, `ethnic`, and the `kid*` fields are missing together in 1,732 rows
- `change_mou` and `change_rev` are missing together in 891 rows
- billing metrics like `rev_Mean`, `mou_Mean`, `totmrc_Mean`, `ovrmou_Mean`, `ovrrev_Mean`, `vceovr_Mean`, `datovr_Mean`, and `roam_Mean` form a smaller shared block of missingness

## Missingness and Churn

Missingness is informative, not random noise.

| Row status | Churn rate |
|---|---:|
| No missing in either table | 48.40% |
| Missing only in `Client.csv` | 49.74% |
| Missing only in `Record.csv` | 74.50% |
| Missing in both tables | 76.56% |

## Practical Interpretation

- Household and demographic missingness likely reflects upstream enrichment gaps or segment-specific collection patterns
- The `Record.csv` missingness is smaller but more predictive than random
- Missing indicators should be preserved for high-value fields
- Household variables should not be dropped blindly; they need grouped handling

# Target Insights

`churn` is the binary label in `Record.csv`. It indicates whether a customer churned in the defined post-observation window.

## Target Balance

| Class | Count | Share |
|---|---:|---:|
| `0` | 50,438 | 50.44% |
| `1` | 49,562 | 49.56% |

## Interpretation

- The target is nearly balanced
- Majority-class accuracy is only 50.44%
- This is a standard binary classification problem, not an imbalance problem
- Probability ranking will be more useful than hard class labels for retention action

## Modeling Implication

- Use stratified splits
- Track precision, recall, F1, and ROC-AUC
- Class weighting or resampling is optional, not the first priority

# Top Churn Drivers

The strongest churn separators are dominated by device age, handset value, usage volume, and recent trend features.

## Numeric Drivers

| Rank | Feature | Direction vs churn | Evidence summary |
|---:|---|---|---|
| 1 | `eqpdays` | Higher in churn | Strongest numeric separator |
| 2 | `hnd_price` | Lower in churn | Churners own cheaper devices |
| 3 | `totmrc_Mean` | Lower in churn | Monthly recurring charge separates classes |
| 4 | `mou_Mean` | Lower in churn | Lower engagement aligns with churn |
| 5 | `avg3mou` | Lower in churn | Recent usage trend is useful |
| 6 | `change_mou` | More negative in churn | Usage decline matters |
| 7 | `custcare_Mean` | Lower in churn in raw form | Surprise counterexample; not a simple “more calls = churn” story |
| 8 | `drop_vce_Mean` | Slightly lower in churn in raw form | Weak but useful service signal |

## Categorical Drivers

| Rank | Feature | Signal strength | Riskier category examples |
|---:|---|---|---|
| 1 | `hnd_webcap` | Strongest categorical signal | Missing / `WC` |
| 2 | `crclscod` | Strong material signal | `A2` |
| 3 | `ethnic` | Material signal | `O` |
| 4 | `asl_flag` | Material signal | `N` |
| 5 | `dualband` | Moderate signal | `N` |
| 6 | `area` | Moderate signal | Northwest/Rocky Mountain area |

## Key Readout

- Device age and handset value are the cleanest early separators
- Trend features improve separation, but only moderately
- Service and household features add refinement, not dominance

# Customer Segments

The EDA suggests a few practical churn segments that are useful for targeting and feature design.

## Segment 1: Low Usage, High Bill Burden

- low `mou_Mean`
- high `totmrc_Mean`
- often lower `rev_Mean`

This is the clearest risk pocket and is reinforced by the bivariate interaction analysis.

## Segment 2: Older Device, Lower Engagement

- high `eqpdays`
- lower `hnd_price`
- lower usage

Older, cheaper devices are associated with higher churn risk.

## Segment 3: Poor Service Experience

- elevated `drop_vce_Mean`
- elevated `blck_vce_Mean`
- sometimes elevated `drop_blk_Mean`

These signals are weaker on their own but become meaningful when stacked with low usage or high charge burden.

## Segment 4: Trend Deterioration

- negative `change_mou`
- negative `change_rev`
- lower `avg3mou` relative to longer-horizon behavior

This segment is behaviorally important and likely represents disengaging customers.

## Segment 5: Household / Demographic Context

- `crclscod`, `ethnic`, `area`, `prizm_social_one`, `ownrent`, `dwllsize`

These features improve segmentation but are not the primary churn engine.

# Revenue Insights

Revenue fields separate churners, but they are less powerful than device age and usage.

## Main Findings

- `totmrc_Mean` is a stronger revenue separator than `rev_Mean`
- lifetime and rolling revenue fields are directionally useful but weaker than usage and device features
- high bill burden can matter most when paired with low usage

## Revenue Signal Summary

| Feature | Direction vs churn | Interpretation |
|---|---|---|
| `totmrc_Mean` | Lower in churn | Lower recurring charge is associated with churn, likely reflecting weaker account commitment |
| `rev_Mean` | Slightly lower in churn | Weak standalone separator |
| `avg3rev` | Slightly lower in churn | Recent revenue trend helps, but modestly |
| `avg6rev` | Slightly lower in churn | Similar to `avg3rev`, with more missingness |
| `change_rev` | Lower / more negative in churn | Directionally useful, but weaker than `change_mou` |

## Revenue Block Interpretation

- revenue measures are highly correlated with each other
- the block should be compressed in modeling
- one level feature plus one trend feature is usually enough

# Service Quality Insights

Service-quality variables are informative, but they are weaker than usage and device signals in raw bivariate form.

## Main Findings

- voice drop and block metrics are directionally associated with churn, but the effect sizes are modest
- customer-care usage does not behave like the naive “more care contact means more churn” story
- support and service issues become more important when they co-occur with low usage or high bill burden

## Service Quality Signal Summary

| Feature | Observation | Interpretation |
|---|---|---|
| `custcare_Mean` | Churners use less customer care on average | Raw support volume is not a simple dissatisfaction proxy |
| `drop_vce_Mean` | Slightly lower in churn in raw averages | Weak standalone separation |
| `blck_vce_Mean` | Slightly lower in churn in raw averages | Weak standalone separation |
| `drop_dat_Mean`, `blck_dat_Mean` | Very small effects | Useful only as supporting context |

## Service Quality Interpretation

- service issues likely amplify churn rather than dominate it
- care-related fields should probably be compressed into a support-intensity proxy
- voice and data issue metrics should be retained if modeling flexibility is needed, but not all of them need to be kept separately

# Leakage Assessment

The dataset does not show obvious direct leakage from column names alone. The risk is timing ambiguity in derived historical fields.

## Safe vs Conditional Features

| Category | Feature examples | Assessment |
|---|---|---|
| Likely safe | `area`, `hnd_price`, `dualband`, `refurb_new`, `rev_Mean`, `mou_Mean`, `totmrc_Mean`, `drop_vce_Mean`, `custcare_Mean` | Usable if measured at the observation snapshot |
| Requires validation | `change_mou`, `change_rev`, `avg3mou`, `avg3rev`, `avg6mou`, `avg6rev`, `months` | Timing must be confirmed before modeling |
| Underdocumented | `recv_sms_Mean`, `iwylis_vce_Mean` | Semantics need confirmation |

## Main Leakage Risks

- `change_mou` and `change_rev` could cross into the churn window if their reference periods are not strictly pre-outcome
- `avg3*` and `avg6*` could become future-looking summaries if the windows are anchored incorrectly
- `months` could become a post-outcome proxy if not measured at the prediction snapshot

## Recommendation

- build a baseline model on clearly safe features first
- add time-windowed features only after timing validation
- keep `Customer_ID` out of the feature set
- keep `churn` as the label only

# Hypothesis Validation Summary

| Hypothesis | Result |
|---|---|
| Older handset equipment increases churn risk | Supported |
| Recent usage declines increase churn risk | Supported |
| Recent revenue decline is a strong churn trigger | Partially supported |
| More customer-care contact signals dissatisfaction | Not supported in raw form |
| Poor voice/data service increases churn | Weak / partially supported |
| Higher-value customers should be prioritized | Supported in business terms |
| Household and demographic fields add material signal | Partially supported |
| Recent trend features are more useful than static demographics | Supported |
| Refurbished or less capable devices increase churn | Supported, mildly |
| Tenure is a strong protective factor | Not strongly supported |

# Feature Engineering Opportunities

The multivariate review suggests a compact but high-value feature set. Strongly correlated columns should be compressed rather than all kept separately.

## Recommended Derived Features

- `usage_to_charge = mou_Mean / totmrc_Mean`
- `revenue_per_usage = rev_Mean / (mou_Mean + 1)`
- `trend_gap = avg3mou - avg6mou`
- `revenue_gap = avg3rev - avg6rev`
- `service_issue_score = drop_vce_Mean + blck_vce_Mean + drop_blk_Mean`
- `support_intensity = custcare_Mean + ccrndmou_Mean + cc_mou_Mean`

## Recommended Interaction Flags

- `low_usage_x_high_charge`
- `low_usage_x_poor_service`
- `old_device_x_low_value`

## Compression Targets

- usage block
- revenue block
- customer-care block
- service-issue block

# Modeling Recommendations

## Feature Strategy

- use a compact feature set first
- preserve missingness flags for informative fields
- reduce redundant correlated variables
- validate all time-windowed features before inclusion

## Model Family Strategy

- regularized linear models should work well after feature compression
- tree-based models can use more raw features, but redundancy will still hurt interpretability
- probability-based outputs should be used for ranking and threshold selection

## Evaluation Strategy

- accuracy is only a baseline
- use precision, recall, F1, ROC-AUC, and threshold analysis
- compare safe-feature and temporal-feature models through ablation

## Practical First-Pass Feature Shortlist

- `eqpdays`
- `hnd_price`
- `mou_Mean`
- `totmrc_Mean`
- `change_mou` if validated
- `change_rev` if validated
- `avg3mou` if validated
- `drop_vce_Mean`
- `custcare_Mean`
- `hnd_webcap`
- `crclscod`
- `area`

# Key Business Findings

- Churn is a real and balanced classification problem, not a rare-event anomaly.
- Device age and device value are among the most actionable early churn signals.
- Recent engagement decline is more important than static demographics.
- Revenue and service issues matter most when they align with low usage.
- Household and demographic data are useful for segmentation, but they are secondary to behavior and device context.
- Missingness is not just data quality noise; it carries predictive information.
- The final model should be compact, leakage-aware, and built for ranking customers by risk rather than only predicting class labels.

