# Final Slide Outline

This outline follows the required final-assignment structure and maps each slide to the message it should carry.

## 1. Business Background

- Company A is a telecom operator with recurring-revenue exposure.
- The project focuses on churn because customer loss directly reduces future revenue.
- The business goal is to identify at-risk customers early enough to intervene.

## 2. Problem Definition

- The core problem is that Company A may be reacting too late to customers who are already on a churn path.
- Broad retention outreach is inefficient without a ranked risk view.
- The task is to identify actionable churn patterns and turn them into business initiatives.

## 3. Dataset Overview

- Source data includes customer, usage, billing, handset, and churn label information.
- The final feature set captures lifecycle, device, service, support, and revenue signals.
- Missingness was handled with indicators where appropriate.

## 4. EDA Findings

- Churn is balanced at roughly half of the sample, so the task is primarily ranking and prioritization.
- The strongest separators are device age, usage decline, and handset value.
- Demographic variables are weaker than behavior and device variables.

## 5. Modeling Approach

- Use a binary churn classifier built from pre-churn features only.
- Focus on explainability and ranking utility, not only raw prediction.
- Feature selection reduced the feature space to a more compact set of business-relevant signals.

## 6. Model Results

- The model concentrates signal in a relatively small set of features.
- Top features include `eqpdays`, `months`, `hnd_price`, `revenue_per_usage`, `totmrc_Mean`, and `change_mou`.
- SHAP and feature importance tell a consistent story about device, usage, and value risk.

## 7. Churn Drivers

- Aging devices are the strongest single churn driver.
- Declining usage is an early warning sign.
- Service quality matters, but it is secondary to device and behavior.
- Customer-care behavior is informative but not a simple churn proxy.

## 8. Business Proposal

- The recommended strategy is a targeted retention program, not a broad discount campaign.
- Priority initiatives:
  - device refresh offers,
  - usage-decline early warning,
  - value-tiered prioritization,
  - early-life onboarding,
  - service recovery for at-risk accounts.

## 9. Impact Estimation

- Impact should be framed as retained revenue, reduced churn, and better campaign ROI.
- The exact monetary result depends on assumptions for average revenue, intervention cost, save rate, and model capture rate.
- The model helps Company A spend retention budget on the customers most worth saving.

## 10. Recommendations

- Deploy the churn score as an action-ranking tool.
- Start with the highest-risk, highest-value segments.
- Use device and usage triggers as the primary routing logic.

## 11. Risks

- False positives can waste retention budget.
- False negatives can miss customers who would have been saved.
- Poorly targeted discounts can reduce margin.
- Predictive patterns should not be presented as causal proof.

## 12. Next Steps

- Validate the retention workflow with a pilot campaign.
- Measure save rate, churn rate, and retained revenue by segment.
- Refine thresholds and offers based on response data.
- Monitor the scorecard and refresh it as behavior changes.

## Speaker Notes

- Open with the business value of reducing churn in a recurring-revenue telecom context.
- Use the EDA slides to show that churn is behavior- and device-driven.
- Use the model results and churn-driver slides to establish confidence in the risk ranking.
- Transition into the proposal by saying that the goal is not only to predict churn, but to act on it.
- Close with the operational recommendation that the model should feed a prioritized retention workflow.

