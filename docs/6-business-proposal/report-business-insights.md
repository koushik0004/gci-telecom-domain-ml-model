# Business Insight Report

This report converts the EDA findings, feature-importance analysis, and SHAP explanations into business-facing churn insights for Company A. The intent is to identify the most actionable retention patterns, the most valuable risk segments, and the operational bottlenecks that should shape the final proposal.

## Executive Summary

- Churn risk is driven primarily by customer lifecycle, device lifecycle, and recent behavior change, not by demographics alone.
- `eqpdays` and `months` are the clearest lifecycle markers, while `change_mou`, `revenue_per_usage`, `hnd_price`, and `totmrc_Mean` capture the strongest usage and value effects.
- Service issues matter, but they are secondary to device and usage signals in both the bivariate EDA and model explainability outputs.
- The model’s signal is concentrated: the top 20 features account for 69.66% of consolidated feature importance, and the top 20 SHAP features account for 64.51% of total mean absolute SHAP mass.
- The strongest business action is early intervention on customers whose usage or revenue patterns are weakening while their devices are aging or expensive.

## 1. Customer Lifecycle Insights

- Tenure is informative, but it is not a simple monotonic shield against churn.
- `months` appears in both the feature-importance and SHAP rankings, which means lifecycle stage matters even though the raw quartile trend is not perfectly linear.
- The clearest lifecycle risk appears early in the relationship, where customers have limited historical attachment and lower switching friction.
- `lor` and `uniqsubs` reinforce that relationship breadth and length help explain churn risk, but they are supporting signals rather than the dominant drivers.
- Retention campaigns should treat early-life customers as a distinct segment because their risk profile is structurally different from long-tenure customers.

## 2. Device Lifecycle Insights

- Device age is the strongest single business signal in the model.
- `eqpdays` ranks first in both feature importance and SHAP, and the bivariate EDA shows it has the strongest numeric separation between churners and non-churners.
- `hnd_price` is another major device-related separator, indicating that handset economics matter alongside device age.
- `refurb_new` and `hnd_webcap` add supporting device context, suggesting that lower-capability or less current devices are associated with greater churn risk.
- The device story is not just “older devices churn more”; it is also “device value, capability, and aging together create retention risk.”

## 3. Revenue and Usage Insights

- Recent usage change is more important than static usage volume alone.
- `change_mou`, `change_mou_log`, and `trend_gap` all support the conclusion that downward movement in activity is a warning signal.
- `avgqty`, `mou_Mean`, `mou_Mean_log`, and `totcalls` show that engagement level still matters, especially when viewed with trend features.
- Revenue intensity variables such as `totmrc_Mean`, `revenue_per_usage`, `rev_Mean`, and `adjrev_log` indicate that spend and usage do not always move together.
- Customers with high spend but weak or deteriorating usage are a priority risk segment because they combine high value with fragile engagement.

## 4. Service Quality Insights

- Service-quality variables are meaningful, but they are not the primary churn layer.
- `drop_vce_Mean` is the strongest service-quality signal in the explainability outputs, with `drop_blk_Mean` also supporting the same theme.
- The raw EDA shows service metrics separating churners only weakly, which means they should be used as supporting evidence rather than the main reason for action.
- The business takeaway is that service friction matters most when it appears alongside weak usage or device risk.
- Service quality is best used as a trigger for targeted recovery, not as a standalone churn model.

## 5. Customer Support Insights

- `custcare_Mean` is statistically informative, but the direction is not the simplistic “more support calls equals more churn” story.
- In the raw bivariate analysis, churners actually show slightly fewer customer-care minutes/calls on average.
- This suggests that support behavior may reflect customer type, issue resolution patterns, or self-selection into service contact rather than a simple dissatisfaction count.
- Support signals should therefore be interpreted as segmentation context, not as a universal churn trigger.
- Operationally, the right response is to inspect whether high-risk customers are getting unresolved service experiences rather than assuming call volume itself is the problem.

## 6. Churn Risk Segments

1. Early-life, aging-device customers
- Low tenure plus high `eqpdays` is the clearest structural risk pattern.
- These customers have not built enough relationship depth to offset handset or service friction.

2. High-value but weakly engaged customers
- High `totmrc_Mean` or `hnd_price` combined with low or declining usage is a high-priority save segment.
- These customers matter disproportionately because loss of one account removes more recurring value.

3. Usage-deterioration customers
- Negative movement in `change_mou` and related trend features identifies disengagement earlier than lifetime averages.
- This segment is attractive for proactive retention because the signal appears before full churn.

4. Service-friction customers
- Customers with elevated `drop_vce_Mean` or related quality indicators should be routed to service recovery if they also show churn risk in behavior or device signals.

5. Device-friction customers
- Customers with older or less capable handsets, or weak web-capability signals, are more vulnerable to churn, especially when their usage is already softening.

## 7. High-Value Customer Risk Factors

- High-value accounts are not automatically safe; they can be the most expensive losses.
- `totmrc_Mean` and `revenue_per_usage` show that revenue intensity is a meaningful risk dimension.
- `hnd_price` indicates that customers with economically meaningful devices also carry retention risk if their engagement weakens.
- High-value customers with declining `change_mou` or weak usage history deserve special treatment because they combine revenue concentration with churn susceptibility.
- The strategic objective should be value retention, not just churn reduction.

## 8. Key Business Bottlenecks

1. Device refresh friction
- The strongest churn signal is tied to device age, which suggests the business may be leaving customers on aging devices too long.

2. Weak early-life retention
- Tenure matters, but the early relationship period remains risky, implying onboarding and first-cycle retention are not strong enough.

3. Late reaction to usage decline
- Trend features are powerful, which means churn is observable before departure, but the business may not be acting soon enough on those early declines.

4. Service recovery is secondary
- Service issues matter, but they are not the top driver, suggesting that service remediation alone will not solve most churn.

5. Overreliance on broad segmentation
- Demographic and household variables are weaker than behavior and device signals, so broad segmentation alone is not enough for accurate prioritization.

## 9. Strategic Opportunities

- Build an intervention trigger around device age, usage decline, and revenue-usage mismatch.
- Prioritize customers with high `eqpdays`, falling `change_mou`, and high `hnd_price` for proactive retention offers.
- Use service-quality signals to route customers into a repair-and-save workflow when device or usage risk is already present.
- Design a value-tiered retention policy so the highest-value accounts receive faster, more tailored intervention.
- Use the model output as a ranking tool, not just a yes/no churn label, so the business can control campaign spend.
- Keep the core lifecycle and usage features in the operational scorecard because they are supported by both the EDA and explainability results.

## Top 10 Insights

1. `eqpdays` is the strongest overall churn driver and the clearest device-lifecycle signal.
2. `months` matters, but tenure alone is not a sufficient protection against churn.
3. Recent usage decline is more predictive than static usage level.
4. `hnd_price` is a major churn separator and should be treated as a value-risk signal.
5. `revenue_per_usage` identifies customers whose spend and activity are misaligned.
6. `totmrc_Mean` shows that monthly revenue contributes to risk segmentation.
7. `drop_vce_Mean` confirms that service quality still matters, but it is secondary.
8. `custcare_Mean` is not a simple proxy for churn intent and should be interpreted carefully.
9. Demographic and household variables add segmentation value but are weaker than device and behavior variables.
10. The best business response is a ranked retention workflow that combines lifecycle, device, usage, and value signals.

## Top 5 Bottlenecks

1. Customers are aging into higher churn risk because device lifecycle appears to be a major weak point.
2. The business likely reacts too late to usage deterioration, even though trend features reveal the risk early.
3. High-value customers can become high-loss customers if spend is not matched by engagement.
4. Service recovery alone is insufficient because service quality is not the dominant churn layer.
5. Broad segmentation is too coarse; the strongest action needs to be driven by behavior and device signals.

## Recommended Business Message

Company A should not treat churn as a random outcome or a purely demographic problem. The evidence shows that churn is concentrated in customers with older devices, weaker recent usage, and unfavorable revenue-to-usage patterns. A targeted retention program should therefore focus on early lifecycle intervention, device-refresh offers, service recovery where needed, and value-based prioritization.

## Source Basis

- `docs/4-EDA-reports/feature_dictionary.md`
- `docs/4-EDA-reports/correlation_cluster_report.md`
- `docs/4-EDA-reports/missingness_features_report.md`
- `docs/3-EDA-planing/eda_bivariate.md`
- `docs/3-EDA-planing/eda_target_analysis.md`
- `docs/5-model-building/report-feature-importance.md`
- `docs/5-model-building/report-shap-analysis.md`
- `docs/5-model-building/report-feature-selection.md`
