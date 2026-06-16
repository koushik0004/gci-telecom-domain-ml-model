# Final Assignment Storyline

This storyline turns the telecom churn project into a consulting-style narrative for the Matsuo Lab final submission. It follows the same logic as the analysis pipeline: define the business problem, show the data evidence, explain the model, and end with a practical retention strategy.

## Executive Narrative

Company A faces a churn problem that is not random and not primarily demographic. The evidence points instead to a combination of device aging, weakening usage, revenue-to-usage imbalance, and secondary service friction. The model confirms that the most actionable churn signals are available before customers leave, which means the business can intervene early rather than reacting after revenue is already lost.

The story of the project is therefore simple:

1. The business problem is customer churn and recurring revenue loss.
2. The data shows that churn risk is concentrated in specific lifecycle and behavior patterns.
3. The model identifies and ranks those patterns reliably enough to guide action.
4. The business proposal translates those signals into a targeted retention strategy.
5. The final recommendation is to use churn scoring as an intervention-ranking tool, not just a classification label.

## Speaker Notes

### Opening

- Start with the business context: Company A is a telecom operator with recurring-revenue exposure to churn.
- Make the main point immediately: the project is about preventing avoidable customer loss, not just improving a model metric.

### Core Message

- Emphasize that the strongest churn signals are device age, usage decline, and revenue-usage mismatch.
- Clarify that demographics are weaker than behavior and device signals, so broad segmentation is not enough.

### Interpretation

- Explain that the model is useful because it surfaces early warning patterns before churn happens.
- Avoid claiming causality. The model identifies predictive patterns that support action, but it does not prove that a specific intervention will cause retention.

### Business Proposal

- Present the retention strategy as a ranked set of initiatives:
  - device refresh offers,
  - usage-decline early warning workflows,
  - value-tiered prioritization,
  - onboarding and first-cycle retention,
  - service recovery for at-risk accounts.
- Note that the order matters because the evidence shows device and usage signals are more important than service signals alone.

### Closing

- End with the practical recommendation: use the scorecard to decide who gets contacted, what offer they get, and how much spend is justified.
- State that the business value comes from focusing effort on the customers most likely to churn and most worth saving.

## Final Report Paths

- `docs/business_understanding.md`
- `docs/3-EDA-planing/eda_target_analysis.md`
- `docs/3-EDA-planing/eda_bivariate.md`
- `docs/4-EDA-reports/feature_dictionary.md`
- `docs/4-EDA-reports/correlation_cluster_report.md`
- `docs/4-EDA-reports/missingness_features_report.md`
- `docs/5-model-building/report-feature-selection.md`
- `docs/5-model-building/report-feature-importance.md`
- `docs/5-model-building/report-shap-analysis.md`
- `docs/6-business-proposal/report-business-insights.md`
- `docs/6-business-proposal/report-retention-strategy.md`

