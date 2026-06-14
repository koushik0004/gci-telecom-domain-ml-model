# EDA Objectives

- Validate which customer, usage, billing, service-quality, and household signals are most associated with churn.
- Separate actionable business hypotheses from data-quality and leakage risks before any modeling.
- Identify customer segments with distinct churn, revenue, and service-experience patterns.
- Confirm which features are stable enough, interpretable enough, and available early enough to support a retention proposal.
- Build a clear analysis path from descriptive EDA to model-ready feature selection.

# Hypotheses To Validate

## Business Hypotheses

- Churn is concentrated among customers with weaker service experience, lower engagement, or visible declines in activity.
- Retention actions will be more valuable on higher-revenue or higher-usage customers than on low-value accounts.
- Recent behavioral change signals are more informative than static demographics for identifying churn risk.
- Customers with older equipment or less capable handsets are more likely to churn or need intervention.

## Data Quality Hypotheses

- Missingness in `Client.csv` is systematic and may be concentrated in household and demographic fields.
- Some categorical codes will require careful normalization before analysis and encoding.
- Recent-history fields may contain timing or leakage risk and must be checked against the churn window.
- Usage, billing, and service metrics may be strongly correlated and require redundancy review.

## Customer Behavior Hypotheses

- Customers with declining usage, lower recent activity, or negative trend metrics are more likely to churn.
- Customers with more customer-care interaction are more dissatisfied and therefore at higher churn risk.
- Frequent dropped, blocked, or roaming-related issues may indicate poor experience and increased churn likelihood.
- Longer-tenure customers may be more stable, but tenure alone may not protect against service-driven churn.

## Revenue Hypotheses

- Customers with higher average revenue or recurring charges should be prioritized because their churn has larger business impact.
- Revenue decline indicators such as `change_rev`, `avg3rev`, and `avg6rev` may precede churn.
- Usage contraction and revenue contraction should move together in churn-prone accounts.
- High bill burden may increase churn even when usage is not low.

## Service Quality Hypotheses

- Customers experiencing more dropped or blocked voice/data events are more likely to churn.
- Customer-care calls are a proxy for unresolved service problems and dissatisfaction.
- Poor service quality may matter more than demographics once usage and revenue are controlled.

## Household / Demographic Hypotheses

- Household composition, dwelling characteristics, and income may help explain churn segments.
- Some demographic fields may be weak predictors individually but useful for segmentation.
- Missingness in household fields may itself encode an informative segment or data-collection pattern.

## Churn-Related Hypotheses

- Churn can be predicted using a combination of recent trend, service-quality, and value features.
- Churn is not driven by a single field but by interacting patterns across behavioral and profile variables.
- Customers with both declining engagement and poor service quality are the highest-risk group.
- A ranked churn score will be more useful than a raw churn label for retention operations.

# Feature Groups

## 1. Customer Identity And Join Fields

- `Customer_ID`
- Use only as a merge key and audit check, never as a predictive feature.

## 2. Core Target And Timing

- `churn`
- `months`
- Validate the label definition, timing, and any potential overlap with recency-style variables.

## 3. Customer Profile And Household Context

- `area`, `crclscod`, `prizm_social_one`
- `income`, `adults`, `marital`, `HHstatin`
- `ownrent`, `dwlltype`, `dwllsize`, `lor`
- `numbcars`, `truck`, `rv`, `forgntvl`
- `kid0_2`, `kid3_5`, `kid6_10`, `kid11_15`, `kid16_17`
- `infobase`, `ethnic`

## 4. Device And Subscription Context

- `new_cell`, `asl_flag`, `dualband`, `refurb_new`, `hnd_webcap`
- `hnd_price`, `phones`, `models`, `eqpdays`
- `actvsubs`, `uniqsubs`

## 5. Lifetime Usage And Revenue

- `totcalls`, `totmou`, `totrev`
- `adjrev`, `adjmou`, `adjqty`
- `avgrev`, `avgmou`, `avgqty`
- `avg3mou`, `avg3qty`, `avg3rev`
- `avg6mou`, `avg6qty`, `avg6rev`

## 6. Recent Billing And Revenue Behavior

- `rev_Mean`, `mou_Mean`, `totmrc_Mean`
- `da_Mean`, `ovrmou_Mean`, `ovrrev_Mean`
- `vceovr_Mean`, `datovr_Mean`, `roam_Mean`
- `change_mou`, `change_rev`

## 7. Service Quality And Care

- `drop_vce_Mean`, `drop_dat_Mean`
- `blck_vce_Mean`, `blck_dat_Mean`
- `drop_blk_Mean`
- `custcare_Mean`, `ccrndmou_Mean`, `cc_mou_Mean`

## 8. Traffic Mix And Usage Pattern

- `mou_cvce_Mean`, `mou_cdat_Mean`, `mou_rvce_Mean`
- `mouiwylisv_Mean`, `mouowylisv_Mean`
- `mou_peav_Mean`, `mou_pead_Mean`, `mou_opkv_Mean`, `mou_opkd_Mean`
- `iwylis_vce_Mean`, `recv_sms_Mean`

# Priority Analyses

## Phase 1: Dataset Integrity And Baseline Profiling

- Confirm one-to-one merge behavior on `Customer_ID`.
- Recheck data types, missingness, and target balance after merge.
- Build a baseline profile of churn rate, revenue, tenure, and usage.

## Phase 2: Univariate EDA

- Compare distributions for core numeric fields by churn class.
- Inspect categorical value counts for key segmentation variables.
- Review missingness concentration in household and demographic fields.

## Phase 3: Bivariate EDA

- Compare churn rates across tenure, handset age, revenue, and service-quality bands.
- Test whether `change_mou`, `change_rev`, and recent-average features separate churners from non-churners.
- Compare churn across household, dwelling, and income segments.

## Phase 4: Multivariate EDA

- Check correlations among usage, revenue, and service-quality variables.
- Identify redundant fields and possible feature clusters.
- Compare churn patterns across combinations such as low usage plus poor service, or high revenue plus high tenure.

## Phase 5: Business Prioritization

- Rank variables by business usefulness, interpretability, and operational actionability.
- Identify the customer segments that would be most valuable for a retention campaign.
- Convert EDA findings into a shortlist of model-ready features and likely intervention segments.

# Risk Areas

- `Customer_ID` must remain an identifier only and never enter modeling.
- `churn` must remain isolated as the target and not be mixed into feature engineering.
- `change_mou`, `change_rev`, `avg3mou`, `avg3rev`, `avg6mou`, `avg6rev`, and `months` may contain timing or leakage risk and need careful interpretation.
- Missing household and demographic data may bias results if rows are dropped without review.
- High-cardinality and ambiguous-coded columns may require tailored encoding or simplified presentation.
- Strong correlations among revenue and usage metrics may inflate apparent importance if not reviewed carefully.

# Expected Insights

- A clear picture of which behavior patterns most strongly separate churners from non-churners.
- Identification of high-risk customer segments based on revenue, service quality, tenure, and handset age.
- A view of whether household or demographic variables add material signal beyond usage and service metrics.
- A shortlist of stable, actionable predictors for modeling and business targeting.
- A retention story that can be translated into campaign prioritization and revenue protection.

# Recommended Visualizations

- Churn rate bar chart by key categorical segments.
- Histograms and KDE plots for numeric features split by churn.
- Box plots or violin plots for revenue, usage, tenure, and handset age versus churn.
- Missingness heatmap or missingness bar chart for `Client.csv` fields.
- Correlation heatmap for numeric usage, revenue, and service metrics.
- Trend comparison plots for `change_mou`, `change_rev`, `avg3*`, and `avg6*` features.
- Stacked or grouped bars for household and demographic segments.
- Pairwise scatter plots for the most important revenue, usage, and quality variables.
