# Phase 5 - Model Development
## Step 5.10 - SHAP Analysis Report

## Objective
Summarize the SHAP artifacts produced by Step 5.10 and convert them into a business-facing explanation of churn and retention drivers.

## Source Artifacts
- `Final Assignment/telecom/shap_feature_importance.csv`
- `Final Assignment/telecom/shap_driver_summary.csv`
- `Final Assignment/telecom/shap/shap_summary.png`
- `Final Assignment/telecom/shap/shap_importance.png`
- `Final Assignment/telecom/shap/dependence_months.png`
- `Final Assignment/telecom/shap/dependence_eqpdays.png`
- `Final Assignment/telecom/shap/dependence_revenue_per_usage.png`
- `Final Assignment/telecom/shap/dependence_avgqty.png`
- `Final Assignment/telecom/shap/dependence_change_mou.png`
- `Final Assignment/telecom/shap/dependence_drop_vce_Mean.png`
- `Final Assignment/telecom/shap/dependence_hnd_price.png`
- `Final Assignment/telecom/lightgbm_best_params.csv`
- `docs/5-model-building/report-feature-importance.md`

## Executive Summary
- The promoted LightGBM model from Step 5.9 remains the reference model for explainability, with tuned validation ROC AUC `0.69505` and best trial `66`.
- SHAP importance is concentrated in device age, tenure, usage, and revenue variables. The top 20 features account for `64.51%` of total mean absolute SHAP mass.
- `eqpdays`, `months`, `eqpdays_log`, `revenue_per_usage`, and `hnd_price` are the strongest global drivers.
- The dependence plots show clear nonlinear behavior, so the mean SHAP sign should be read together with the feature-range pattern.

## Model Metadata
- Model: LightGBM
- Best trial: `66`
- Max depth: `12`
- Learning rate: `0.12269880305829967`
- Num leaves: `99`
- Min child samples: `27`
- Feature fraction: `0.6865798643049159`
- Bagging fraction: `0.6147859226286729`
- Best validation ROC AUC: `0.6950476477650352`
- Best train ROC AUC: `0.7790484319886338`
- Train-validation ROC AUC gap: `0.08400078422359858`

## Top 20 SHAP Features
| Rank | Feature | Mean abs SHAP | Mean SHAP | Direction |
|---:|---|---:|---:|---|
| 1 | `eqpdays` | 0.139369 | -0.019277 | retention |
| 2 | `months` | 0.121309 | 0.018668 | churn |
| 3 | `eqpdays_log` | 0.105016 | -0.010492 | retention |
| 4 | `revenue_per_usage` | 0.098995 | -0.000738 | retention |
| 5 | `hnd_price` | 0.084167 | 0.013767 | churn |
| 6 | `months_log` | 0.059073 | 0.005030 | churn |
| 7 | `crclscod` | 0.058884 | -0.004770 | retention |
| 8 | `totmrc_Mean` | 0.058854 | 0.003322 | churn |
| 9 | `change_mou` | 0.058171 | 0.000034 | churn |
| 10 | `change_mou_log` | 0.055671 | -0.002756 | retention |
| 11 | `lor` | 0.055039 | 0.001779 | churn |
| 12 | `mou_Mean_log` | 0.049646 | 0.002022 | churn |
| 13 | `trend_gap` | 0.048569 | 0.000397 | churn |
| 14 | `uniqsubs` | 0.048249 | -0.003801 | retention |
| 15 | `mou_cvce_Mean_log` | 0.045071 | -0.003648 | retention |
| 16 | `totmrc_Mean_log` | 0.044735 | -0.001366 | retention |
| 17 | `drop_vce_Mean` | 0.044154 | 0.001006 | churn |
| 18 | `avgqty` | 0.040481 | -0.000952 | retention |
| 19 | `area` | 0.032779 | -0.000127 | retention |
| 20 | `mouiwylisv_Mean` | 0.031864 | 0.000585 | churn |

## Strongest Churn Drivers
| Rank | Feature | Mean SHAP | Mean abs SHAP |
|---:|---|---:|---:|
| 1 | `months` | 0.018668 | 0.121309 |
| 2 | `hnd_price` | 0.013767 | 0.084167 |
| 3 | `avgmou_log` | 0.005406 | 0.029252 |
| 4 | `months_log` | 0.005030 | 0.059073 |
| 5 | `actvsubs` | 0.004216 | 0.007630 |
| 6 | `totmrc_Mean` | 0.003322 | 0.058854 |
| 7 | `rev_Mean_log` | 0.003008 | 0.018381 |
| 8 | `adjrev_log` | 0.002263 | 0.017602 |
| 9 | `mou_Mean_log` | 0.002022 | 0.049646 |
| 10 | `lor` | 0.001779 | 0.055039 |

## Strongest Retention Drivers
| Rank | Feature | Mean SHAP | Mean abs SHAP |
|---:|---|---:|---:|
| 1 | `eqpdays` | -0.019277 | 0.139369 |
| 2 | `eqpdays_log` | -0.010492 | 0.105016 |
| 3 | `crclscod` | -0.004770 | 0.058884 |
| 4 | `uniqsubs` | -0.003801 | 0.048249 |
| 5 | `mou_cvce_Mean_log` | -0.003648 | 0.045071 |
| 6 | `change_mou_log` | -0.002756 | 0.055671 |
| 7 | `avgrev` | -0.002623 | 0.021562 |
| 8 | `ovrmou_Mean_capped` | -0.002607 | 0.021653 |
| 9 | `asl_flag` | -0.002564 | 0.031860 |
| 10 | `refurb_new` | -0.002168 | 0.020225 |

## Feature-Level Business Interpretation
- `eqpdays` is the strongest global signal. The dependence plot shows a strong nonlinear split by device age, so device lifecycle is a first-order churn input rather than a linear effect.
- `months` behaves as a tenure gate. Very short-tenure customers sit in the high-risk region, while longer-tenure customers are generally more protected.
- `revenue_per_usage` and `hnd_price` show that value and device economics matter. The dependence curves are not monotonic, which suggests segmented customer behavior rather than a single threshold.
- `change_mou` and `change_mou_log` confirm that recent usage drift matters. Sudden changes in activity are more informative than the raw usage level alone.
- `drop_vce_Mean` remains relevant and supports the service-quality hypothesis, but it is clearly secondary to tenure and device/usage signals.

## Customer Lifecycle Insights
- The model separates early-life customers from established customers.
- Short-tenure customers carry the strongest churn risk, especially in the lower `months` band visible in the dependence plot.
- `eqpdays` adds a second lifecycle axis that reflects device aging or device tenure. The plot shows that lifecycle and handset age interact rather than duplicating each other.
- `uniqsubs` and `lor` reinforce the lifecycle story by capturing relationship breadth and length.

## Revenue and Usage Insights
- `revenue_per_usage`, `totmrc_Mean`, `rev_Mean_log`, and `adjrev_log` show that spend intensity and usage efficiency are both important.
- The `revenue_per_usage` dependence plot indicates that high values are associated with higher churn contribution, which can flag customers whose spend is misaligned with their usage profile.
- `avgqty` and `mou_Mean_log` show that usage scale itself is meaningful, but it is strongest when paired with spend and trend variables.

## Service Quality Insights
- `drop_vce_Mean` remains one of the most interpretable service-quality signals in the model.
- `drop_blk_Mean` is weaker than `drop_vce_Mean` in the SHAP ranking but still supports the broader service-friction theme from earlier feature importance work.
- The SHAP output suggests service problems matter, but they are not the dominant explanatory layer compared with tenure and device economics.

## Device Lifecycle Insights
- `hnd_price`, `eqpdays`, and `eqpdays_log` form a consistent device-lifecycle cluster.
- The `hnd_price` dependence plot is tiered rather than smooth, which implies different customer responses across price bands.
- Low-price and very high-price regions behave differently from the middle of the distribution, so device value should be treated as segmented rather than linear.

## Customer Risk Signals
- Sudden movement in usage, revenue, or handset-related variables should be treated as a churn warning.
- Short tenure combined with unusual device economics is a stronger risk pattern than any single raw feature alone.
- The presence of `change_mou`, `change_rev`, and their transformed versions in the top 20 confirms that change over time is more informative than static activity.

## Retention Signals
- Long-tenure and low-device-age customers show the clearest retention signals in the SHAP output.
- Low `eqpdays`, low `eqpdays_log`, and stable usage profiles all push the model toward retention.
- `crclscod`, `uniqsubs`, and `asl_flag` appear as supporting retention signals, but they are weaker than the core lifecycle variables.

## Recommendations
- Keep `eqpdays`, `months`, `revenue_per_usage`, `hnd_price`, `change_mou`, and `drop_vce_Mean` as primary explainability anchors.
- Use the dependence plots to communicate that the model is nonlinear and segmented, not threshold-only.
- Reuse the top 20 SHAP list as the primary business shortlist for retention interventions.
- Align any future feature pruning or reporting with the earlier feature-importance report, since both analyses point to the same core lifecycle and usage drivers.

## Report Path
- `docs/5-model-building/report-shap-analysis.md`
