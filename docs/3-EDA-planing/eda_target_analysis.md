# Churn Overview

The target variable is `churn` in `Record.csv`. It is a binary classification label that indicates whether a customer churned in the defined post-observation window.

| Item | Value |
|---|---:|
| Total customers | 100,000 |
| Non-churn (`0`) | 50,438 |
| Churn (`1`) | 49,562 |
| Churn rate | 49.56% |
| Non-churn rate | 50.44% |
| Class ratio (`0`:`1`) | 1.02:1 |

The target is close to perfectly balanced. That is helpful for baseline modeling because the dataset does not suffer from the extreme minority-class problem seen in many churn projects.

![Target balance](./assets/target_balance.svg)

# Churn Distribution

| Class | Count | Percentage | Business meaning |
|---|---:|---:|---|
| `0` | 50,438 | 50.44% | Customer remained active through the churn window |
| `1` | 49,562 | 49.56% | Customer churned in the churn window |

Key distribution observations:

- The positive class is the churned customer class (`1`), and it is not rare.
- The dataset is only slightly skewed toward non-churn, so class imbalance handling is not the first issue to solve.
- A trivial majority-class model would achieve about **50.44% accuracy**, which is only marginally better than chance.
- Because the classes are so close in size, the real challenge is separation quality, not resampling imbalance.

# Business Interpretation

Churn here represents direct customer loss and therefore direct revenue exposure for the telecom business.

- Each churned customer creates replacement cost, retention cost, and future revenue loss.
- Because the label is balanced, retention operations should not assume that churn is a small tail event.
- The business value comes from ranking customers by risk and acting on the highest-probability cases first.
- A campaign built only on the hard class label would be less useful than a probability score that supports prioritization and threshold selection.

The earlier EDA context points to the most plausible churn drivers:

- declining usage and revenue trends,
- poorer service quality,
- higher customer-care contact,
- older equipment,
- and weaker recent engagement.

That means the first business separation is likely to come from behavior and service experience rather than from demographics alone.

# Modeling Implications

- This is a standard binary classification problem, not a regression problem.
- Accuracy is a valid baseline metric because the classes are nearly balanced, but it is not sufficient on its own.
- Precision, recall, F1, ROC-AUC, and especially threshold-based evaluation should be used to understand retention tradeoffs.
- Stratified train/validation/test splits should preserve the near-50/50 class structure.
- Class weights or resampling are optional, not mandatory, because imbalance is mild.
- Probability outputs will be more useful than hard labels for campaign targeting.
- Features that are close to the churn window, such as `change_mou`, `change_rev`, `avg3mou`, `avg3rev`, and `months`, need careful leakage review before modeling.
- Missing indicators may be worth keeping because earlier EDA showed that missingness itself is associated with churn.

Baseline expectations:

| Metric | Baseline expectation |
|---|---|
| Accuracy | About 50.44% from always predicting `0` |
| Random guess accuracy | About 50% |
| Model value threshold | Must outperform the majority baseline and improve ranking quality |

# Initial Predictive Signals

The strongest first-pass separation opportunities come from the feature groups that already have a plausible link to churn behavior.

| Candidate signal | Why it may separate churn | Actionability |
|---|---|---|
| `change_mou` | Usage drop can indicate disengagement | High |
| `change_rev` | Revenue decline can signal downgrade or reduced activity | High |
| `avg3mou`, `avg3rev` | Recent trend features can capture weakening activity faster than lifetime averages | High |
| `custcare_Mean` | More customer-care contact can reflect unresolved dissatisfaction | High |
| `drop_vce_Mean`, `blck_vce_Mean` | Poor voice service quality can push customers out | High |
| `drop_dat_Mean`, `blck_dat_Mean` | Data-service issues may be especially important for more connected users | High |
| `eqpdays` | Older devices may correlate with lower satisfaction or aging contracts | Medium |
| `months` | Tenure often reduces churn, but not always if service problems persist | Medium |
| `rev_Mean`, `totmrc_Mean` | High bill burden or high-value accounts may show different churn behavior | Medium |
| `mou_Mean` | Persistent low engagement can reflect a weak attachment to the service | Medium |
| Missingness flags in `Client.csv` and `Record.csv` | Missingness was shown earlier to have a meaningful churn association | Medium |
| Household and demographic fields | Useful for segmentation, though usually weaker than behavior and service signals | Low to Medium |

Likely class-separation pattern:

- High-risk customers should cluster around declining usage, declining revenue, service complaints, and older equipment.
- Lower-risk customers should cluster around stable usage, stable revenue, fewer support contacts, and longer tenure.
- Household and demographic variables may refine the segmentation, but they are unlikely to be the main separator on their own.

## Churn Separation Takeaway

The target is already balanced, so the main modeling gain will come from learning meaningful boundaries between churners and non-churners. The most promising separation is expected from recent behavior, service quality, and revenue change signals, with missingness and household context playing a supporting role.

# Key Findings

- `churn` is a balanced binary target with 49.56% churn rate.
- The majority-class baseline is only 50.44%, so any useful model must do more than predict the dominant class.
- The target distribution is healthy for standard supervised classification and does not require aggressive imbalance correction.
- The best early separation opportunities are likely in trend, service-quality, and support-contact features.
- Probability ranking will be more valuable than a simple churn label for retention action.
- Leakage checks remain important for the recent-history variables, even though the target itself is cleanly defined.
