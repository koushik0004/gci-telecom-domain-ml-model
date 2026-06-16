# Telecom Churn Reduction Proposal

This report translates the churn-driver evidence into a practical retention strategy for Company A. The goal is not only to reduce churn, but to focus intervention on the customers whose loss would hurt revenue most and whose churn risk is already visible in the data.

## 1. Executive Summary

- Churn is concentrated in customers with aging devices, weakening usage, and unfavorable value-to-usage patterns.
- The strongest action is early intervention, not broad discounting.
- Device refresh, usage-deterioration outreach, and value-tiered saves should be the core of the retention strategy.
- Service recovery is useful, but it should be a support layer rather than the main churn fix.
- The model should be used as a ranking tool so Company A can prioritize the highest-risk, highest-value customers first.

## 2. Current Churn Problem

- Company A appears to be losing customers before the business reacts to the warning signs.
- The model findings show that churn is not random and not mostly demographic.
- The clearest risk pattern is a combination of:
  - older devices,
  - declining usage,
  - weak revenue-to-usage alignment,
  - and, in some cases, service friction.
- This means broad retention campaigns will be inefficient because they will miss the customers whose risk is already rising.

## 3. Evidence From Data

- `eqpdays` is the strongest churn driver in both feature importance and SHAP.
- `months` matters, but tenure alone does not protect against churn.
- `change_mou`, `trend_gap`, and related trend features show that declining usage is an early warning signal.
- `hnd_price` and `revenue_per_usage` indicate that value and device economics are important parts of the churn story.
- `totmrc_Mean` shows that monthly revenue level is a meaningful prioritization variable.
- `drop_vce_Mean` is the strongest service-quality signal, but it is secondary to device and usage effects.
- `custcare_Mean` should be treated as segmentation context rather than a simple churn trigger.
- Demographic variables are weaker than behavioral and device variables, so they should not drive the main intervention design.

## 4. Recommended Initiatives

### Initiative 1: Device Refresh Save Offer

- **Target Segment**: Customers with high `eqpdays`, lower device capability, and softening usage.
- **Business Logic**: Aging handsets are the strongest churn signal. A device refresh offer reduces friction, improves perceived value, and gives the customer a concrete reason to stay.
- **Expected Benefit**: Higher retention among customers whose churn risk is tied to device lifecycle rather than pure price sensitivity.
- **Required Resources**: Device subsidy budget, offer design, eligibility rules, CRM campaign setup, and fulfillment support.
- **Risks**: Subsidy cost can be high; offers may be wasted on customers who would stay anyway if targeting is too broad.

### Initiative 2: Usage-Decline Early Warning Workflow

- **Target Segment**: Customers with falling `change_mou`, negative `trend_gap`, or shrinking engagement.
- **Business Logic**: Usage decline appears before churn, so the business should react while the customer is still salvageable.
- **Expected Benefit**: Earlier intervention, better save rates, and less dependence on reactive win-back campaigns.
- **Required Resources**: Trigger rules, daily or weekly scoring, retention playbooks, and outreach scripts.
- **Risks**: False positives can lead to unnecessary contact; the workflow must be tuned to avoid overmessaging.

### Initiative 3: Value-Tiered Retention Prioritization

- **Target Segment**: High `totmrc_Mean`, high `hnd_price`, or high `revenue_per_usage` customers with any churn warning signs.
- **Business Logic**: Not all churners have the same revenue impact. The business should protect high-value accounts first.
- **Expected Benefit**: Better retention ROI because the company focuses the best offers on the accounts with the most revenue at risk.
- **Required Resources**: Customer value tiers, campaign rules, finance-approved offer bands, and account-level prioritization.
- **Risks**: Overdiscounting high-value customers can reduce margin if offers are too generous.

### Initiative 4: Service Recovery Trigger for At-Risk Accounts

- **Target Segment**: Customers with elevated `drop_vce_Mean`, `drop_blk_Mean`, or support-related risk signals, especially when paired with weak usage.
- **Business Logic**: Service issues are not the main churn driver, but they matter when combined with other risk signals.
- **Expected Benefit**: Reduced churn from customers whose dissatisfaction is operational rather than purely commercial.
- **Required Resources**: Service escalation workflow, network or care routing, root-cause tracking, and customer follow-up process.
- **Risks**: Service recovery alone will not solve most churn, so this initiative should not be treated as the primary retention lever.

### Initiative 5: Early-Life Onboarding and First-Cycle Retention

- **Target Segment**: Lower-tenure customers, especially those with high device age or early weak engagement.
- **Business Logic**: The earliest part of the customer lifecycle is structurally vulnerable, so the business should stabilize customers before switching behavior forms.
- **Expected Benefit**: Better first-year retention and stronger relationship depth before device or usage friction builds.
- **Required Resources**: Onboarding journeys, first-cycle check-ins, welcome offers, and lifecycle-based campaign rules.
- **Risks**: If the program is too generic, it may not reach the subset of early-life customers who actually need help.

## 5. Prioritization Matrix

| Rank | Initiative | Impact | Effort | Priority | Why |
| --- | --- | --- | --- | --- | --- |
| 1 | Device Refresh Save Offer | High | Medium | Highest | Strongest model signal and clear business action |
| 2 | Usage-Decline Early Warning Workflow | High | Medium | Highest | Catches churn before it becomes final |
| 3 | Value-Tiered Retention Prioritization | High | Medium | High | Protects the most revenue per saved customer |
| 4 | Early-Life Onboarding and First-Cycle Retention | Medium-High | Medium | High | Addresses a structurally risky lifecycle stage |
| 5 | Service Recovery Trigger for At-Risk Accounts | Medium | Medium | Medium | Useful, but secondary to device and behavior drivers |

## 6. Recommended Roadmap

### Phase 1: Immediate Setup

- Build the churn-risk score as an account ranking tool.
- Define trigger rules for `eqpdays`, `change_mou`, `trend_gap`, `totmrc_Mean`, and `revenue_per_usage`.
- Create customer tiers so retention actions can be matched to value.

### Phase 2: Pilot Retention Plays

- Launch the device refresh offer for the highest-risk device-lifecycle segment.
- Launch the usage-decline outreach workflow for customers whose engagement is falling.
- Add a service recovery path for customers with both risk signals and quality issues.

### Phase 3: Expand Lifecycle Coverage

- Add onboarding and first-cycle retention journeys for lower-tenure customers.
- Refine the segmentation rules using campaign response results.
- Tighten offer eligibility so discounts are reserved for customers with the highest expected save value.

### Phase 4: Operationalize and Monitor

- Track save rate, churn rate, offer cost, and retained revenue by segment.
- Review false positives and false negatives regularly.
- Update the scorecard and campaign rules as the business learns which interventions work best.

## Top 5 Initiatives

1. Device Refresh Save Offer
2. Usage-Decline Early Warning Workflow
3. Value-Tiered Retention Prioritization
4. Early-Life Onboarding and First-Cycle Retention
5. Service Recovery Trigger for At-Risk Accounts

## Priority Ranking

1. Device Refresh Save Offer
2. Usage-Decline Early Warning Workflow
3. Value-Tiered Retention Prioritization
4. Early-Life Onboarding and First-Cycle Retention
5. Service Recovery Trigger for At-Risk Accounts

## Source Basis

- `docs/6-business-proposal/report-business-insights.md`
- `docs/5-model-building/report-feature-importance.md`
- `docs/5-model-building/report-shap-analysis.md`
- `docs/4-EDA-reports/feature_dictionary.md`
- `docs/3-EDA-planing/eda_bivariate.md`
- `docs/3-EDA-planing/eda_target_analysis.md`

