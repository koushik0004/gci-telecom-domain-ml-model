# Hypothesis Seeds

These are initial assumptions only. They are grounded in the dataset columns, the column descriptions, and the business context from the earlier documents. They must be validated later through EDA and modeling.

## Candidate Feature Hypotheses

| Feature | Possible Meaning | Expected Impact | Confidence |
|---|---|---|---|
| `eqpdays` | Older handset equipment may indicate aging devices or weaker customer satisfaction | Higher values may increase churn risk | High |
| `change_mou` | Recent drop in usage can signal disengagement | Negative change likely increases churn risk | High |
| `change_rev` | Recent revenue decline can indicate reduced activity or a downgrade | Negative change likely increases churn risk | High |
| `custcare_Mean` | More customer care calls may reflect unresolved complaints | Higher values likely increase churn risk | High |
| `drop_vce_Mean` | Dropped voice calls may indicate poor service quality | Higher values likely increase churn risk | High |
| `blck_vce_Mean` | Blocked voice calls may indicate network access problems | Higher values likely increase churn risk | Medium |
| `roam_Mean` | Roaming usage may reflect travel-heavy or premium customers | Could increase or decrease churn depending on segment | Medium |
| `totmrc_Mean` | Monthly recurring charge level may proxy plan value or bill burden | Very high charges may increase churn; mid-range may be stable | Medium |
| `rev_Mean` | Average monthly revenue may capture customer value and billing burden | High revenue customers may be less likely to churn, but bill shock may matter | Medium |
| `mou_Mean` | Usage intensity may reflect engagement and stickiness | Higher usage may reduce churn risk | Medium |
| `avg3mou` | Recent 3-month usage trend may show momentum better than lifetime usage | Lower recent usage may increase churn risk | High |
| `avg3rev` | Recent 3-month revenue trend may show weakening spend | Lower recent revenue may increase churn risk | High |
| `prizm_social_one` | Social segment may correlate with value sensitivity or service preferences | Some segments may churn more often than others | Low |
| `income` | Higher-income customers may be less price-sensitive or have different plan mix | Direction uncertain without segment check | Low |
| `hnd_price` | Expensive devices may be associated with more committed customers or financing burden | Higher price could either reduce churn or increase bill sensitivity | Medium |
| `refurb_new` | Refurbished devices may correlate with lower perceived value | Refurbished status may increase churn risk | Medium |
| `hnd_webcap` | Web-capable devices may indicate more advanced usage and stronger lock-in | Higher capability may reduce churn risk | Low |
| `months` | Tenure often reduces churn as customers become more established | Higher tenure likely decreases churn risk | High |
| `actvsubs` | More active subscribers in a household may reflect shared account complexity | Could increase stickiness or create billing friction | Low |
| `uniqsubs` | Multiple unique subscribers in a household may indicate shared usage or complexity | Direction uncertain, but may matter in household-level churn | Low |

## Business Hypotheses

- Customers with poorer service experience indicators are more likely to churn than customers with stable service quality.
- Customers showing recent declines in usage or revenue are more likely to churn than customers with stable or rising activity.
- Retention campaigns should focus on high-value customers first, because saving them has higher business impact than saving low-value accounts.
- Device age and handset quality may be practical intervention levers, because a handset upgrade can be offered before the customer leaves.
- A churn-risk ranking will be more useful to the business than a simple churn/non-churn label because retention resources are limited.

## Data Hypotheses

- The strongest predictors will probably come from recent behavior features such as `change_mou`, `change_rev`, `avg3mou`, and `avg3rev`, rather than demographic fields alone.
- Usage, billing, and service-quality variables are likely correlated, so some redundancy should be expected in the feature set.
- Missingness may not be random for all columns, especially household and demographic variables, so missing-value handling may itself carry signal.
- Identifier-like fields such as `Customer_ID` should not be used as predictive features.
- Some columns may be more useful after transformation, binning, or scaling than in raw form.

## Modeling Hypotheses

- A tree-based classifier will likely outperform a purely linear baseline because churn may depend on nonlinear interactions.
- A simple baseline model should still be kept for comparison because the dataset appears balanced and interpretable features matter for the final proposal.
- Feature importance or SHAP-style explanations will help translate the model into business language.
- The model may perform better if the data is split carefully by customer rather than by row duplicates, because the tables are joined on one customer key.
- If churn is close to balanced, accuracy may be acceptable as a starting metric, but precision and recall may still be important for the retention use case.
- A model that ranks customers by risk will be more operationally valuable than a model that only outputs a hard class label.

## Working Assumptions

- `churn` is the main target unless later EDA shows a better business target.
- Features available in the current files are assumed to be pre-churn or sufficiently close to the decision point for a first-pass model.
- The business context is customer retention for a wireless telecom operator.
- These hypotheses are intentionally broad and should be narrowed or rejected after EDA.
