# Target Understanding

## Target Definition

The target variable is `churn` in `Record.csv`.

- Target type: binary classification
- Meaning: whether a customer churned between 31 and 60 days after the observation date
- Source: `docs/2-dataset-understanding/dataset_schema.md`

Because the target is binary, the modeling task is to predict churn risk rather than a continuous value. The target is already present in the labeled training table, so `Record.csv` is the primary modeling dataset.

## Distribution Summary

The raw target distribution in `Record.csv` is:

| Class | Count | Percentage |
| --- | ---: | ---: |
| `0` | 50,438 | 50.44% |
| `1` | 49,562 | 49.56% |

Additional distribution notes:

- Total rows analyzed: 100,000
- The classes are nearly balanced
- The positive class (`1`) represents churned customers
- The negative class (`0`) represents customers who did not churn in the target window

## Business Interpretation

This target supports the main business objective of customer retention.

- A `1` indicates a customer is at risk of revenue loss for the telecom operator.
- A `0` indicates a customer who remained active during the observation window.
- The target is aligned with a practical retention use case because it enables risk ranking, outreach prioritization, and campaign targeting.

From a business standpoint, predicting churn helps Company A focus retention effort on customers most likely to leave instead of applying broad and expensive campaigns to the full base.

## Modeling Implications

- This is a supervised classification problem, not a regression problem.
- Class balance is close to 50/50, so accuracy is a reasonable baseline metric.
- Confusion matrix, precision, recall, and F1 score are still useful because the cost of false positives and false negatives may differ in a retention workflow.
- Probability-based outputs would be useful for ranking customers by churn risk and selecting a campaign threshold.
- Since the target is already in `Record.csv`, any merged feature set must preserve the label only in the modeling table and exclude it from predictors.

## Potential Challenges

- Leakage risk: some recency or trend variables may reflect information too close to the churn window and should be checked carefully.
- Threshold choice: a business retention campaign may prefer higher recall or a different tradeoff than raw accuracy.
- Label timing: the definition of churn is tied to a specific post-observation window, so feature timing must stay strictly before that window.
- Business action dependency: the target is useful only if the final proposal includes a concrete intervention such as a retention offer, service follow-up, or plan adjustment.
- Near-balanced classes: while this is good for training, it still requires evaluation beyond accuracy to understand the real tradeoff between catching churners and avoiding unnecessary outreach.
