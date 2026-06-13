# Dataset Understanding Report

This document is the authoritative reference for the telecom churn dataset used in the final assignment. It consolidates the inventory, schema, missing-value analysis, data type validation, cardinality analysis, target understanding, and business context into one working reference for downstream EDA, feature engineering, modeling, and business analysis.

## Dataset Overview

The project contains two customer-level source tables for a wireless telecom churn study:

- `Final Assignment/telecom/Client.csv`
- `Final Assignment/telecom/Record.csv`

Both tables contain 100,000 customer rows and are linked by `Customer_ID`. The merged dataset forms a single customer-level analytical table.

The business use case is customer retention for Company A, a wireless telecom operator. The predictive task is churn modeling: identify customers who are likely to churn so retention action can be prioritized before revenue is lost.

## Dataset Inventory

| Dataset | Rows | Columns | Role |
|---|---:|---:|---|
| `Final Assignment/telecom/Client.csv` | 100,000 | 50 | Auxiliary table with customer profile, household, handset, and demographic attributes. |
| `Final Assignment/telecom/Record.csv` | 100,000 | 51 | Primary analytical table with usage, billing, service-quality, and target fields. |
| Submission dataset | N/A | N/A | No separate submission or test file is present in the workspace. |

Key inventory facts:

- `Customer_ID` is the shared join key.
- The relationship is one-to-one at the customer level.
- `Record.csv` is the primary modeling table because it contains `churn`.
- `Client.csv` adds context for customer profile, household, and handset characteristics.
- No sample submission file or external lookup file is present in the workspace.

## Dataset Schema

The combined schema is dominated by customer attributes, usage metrics, billing metrics, household indicators, and the binary churn outcome.

### Schema Summary

| Schema Area | Source | Notes |
|---|---|---|
| Customer profile and household context | `Client.csv` | Includes demographics, dwelling, income, household composition, handset, and subscription-related fields. |
| Usage, billing, and service behavior | `Record.csv` | Includes revenue, minutes of use, call activity, service-quality, and recency-like change metrics. |
| Target | `Record.csv` | `churn` is the binary label. |
| Join key | Both files | `Customer_ID` is required for merging and must not be used as a predictive feature. |

### Important Schema Notes

- Many numeric fields are stored as text in the raw CSVs and need explicit conversion.
- Several flag-like fields are coded as `Y`/`N`, `0`/`1`, `U`, or `M` rather than native booleans.
- No date or timestamp columns were found.
- Two columns are not fully described in the source notes and need light verification during EDA: `recv_sms_Mean` and `iwylis_vce_Mean`.
- The schema is suitable for supervised binary classification once type handling, missingness, and encoding are addressed.

### Feature Group View

- `Client.csv` contains relatively static customer descriptors.
- `Record.csv` contains behavioral and outcome-oriented measures closer to the churn event.
- The merged table should preserve the target only in the modeling dataset and exclude it from predictors.

## Target Variable

The target variable is `churn` in `Record.csv`.

| Target | Type | Meaning |
|---|---|---|
| `churn` | Binary classification | Whether a customer churned between 31 and 60 days after the observation date. |

### Target Distribution

| Class | Count | Percentage |
|---|---:|---:|
| `0` | 50,438 | 50.44% |
| `1` | 49,562 | 49.56% |

Target interpretation:

- `1` indicates a churned customer.
- `0` indicates a customer who did not churn in the target window.
- The classes are nearly balanced, so accuracy is a reasonable baseline metric, but precision, recall, F1, and confusion-matrix analysis are still required.

Business meaning:

- The target supports retention prioritization.
- A positive prediction should trigger a concrete intervention such as outreach, a retention offer, or service follow-up.
- The target is useful only if the features used to predict it are available before the churn window.

## Missing Values

Missing values were measured from the raw CSV files as blank cells. No imputation or exploratory replacement was performed.

### Missingness at a Glance

| Dataset | Missing Cells | Notes |
|---|---:|---|
| `Client.csv` | 327,786 | Missingness is concentrated in household and demographic fields. |
| `Record.csv` | 4,995 | Missingness is limited and stays below 1% for each affected field. |

### High-Priority Missing Fields in Client.csv

Fields with high missingness:

- `ownrent`
- `lor`
- `dwlltype`
- `numbcars`
- `HHstatin`
- `dwllsize`

Fields with medium missingness:

- `prizm_social_one`
- `adults`
- `infobase`
- `income`

Fields with low but non-zero missingness:

- `avg6mou`
- `avg6qty`
- `avg6rev`
- `hnd_price`
- `truck`
- `rv`
- `marital`
- `forgntvl`
- `ethnic`
- `kid0_2`
- `kid3_5`
- `kid6_10`
- `kid11_15`
- `kid16_17`
- `creditcd`
- and a few other isolated device/profile fields

### Missingness in Record.csv

The missingness in `Record.csv` is small and mostly affects:

- `rev_Mean`
- `mou_Mean`
- `totmrc_Mean`
- `da_Mean`
- `ovrmou_Mean`
- `ovrrev_Mean`
- `vceovr_Mean`
- `datovr_Mean`
- `roam_Mean`
- `change_mou`
- `change_rev`

### Missingness Interpretation

- Missing demographic and household fields may reflect optional collection, external enrichment gaps, or unmatched source data.
- The high missingness in household variables suggests the missingness may be systematic rather than random.
- The limited missingness in `Record.csv` is lower risk, but it still needs consistent handling before modeling.

## Data Types

The raw files ingest all fields as text, so the core work here is semantic typing rather than file-format typing.

### Data Type Summary

| Type Issue | Examples | Required Action |
|---|---|---|
| Numeric values stored as text | `totcalls`, `totmou`, `totrev`, `hnd_price`, `rev_Mean`, `months` | Cast to numeric dtypes before analysis. |
| ID values stored as text | `Customer_ID` | Keep as string identifier and do not treat as numeric. |
| Flag fields encoded as codes | `new_cell`, `asl_flag`, `dualband`, `truck`, `rv`, `forgntvl`, `creditcd`, `kid*`, `churn` | Map explicitly to binary or categorical values. |
| Categorical codes stored as text | `crclscod`, `prizm_social_one`, `area`, `dwlltype`, `marital`, `HHstatin`, `dwllsize`, `ethnic` | Keep as categorical, not numeric. |
| Date/time fields | None found | No date parsing is required at this stage. |

### Data Type Risks

- If numeric values remain as strings, aggregations, scaling, and model training will fail or behave incorrectly.
- If `Customer_ID` is converted to numeric, it can be misinterpreted as a measurable feature.
- If coded flags are mapped incorrectly, business meaning can be lost.
- Ambiguous fields such as `infobase` and `hnd_webcap` should be validated carefully before forced conversion.

## Cardinality

Cardinality was counted from non-empty cells only. The following thresholds were used:

- Low cardinality: fewer than 10 unique values
- Medium cardinality: 10 to 50 unique values
- High cardinality: more than 50 unique values

### Cardinality Summary

| Feature Group | Representative Features | Recommendation |
|---|---|---|
| Low cardinality categorical fields | `new_cell`, `asl_flag`, `prizm_social_one`, `dualband`, `refurb_new`, `hnd_webcap`, `truck`, `rv`, `ownrent`, `dwlltype`, `marital`, `infobase`, `HHstatin`, `forgntvl`, `kid0_2`, `kid3_5`, `kid6_10`, `kid11_15`, `kid16_17`, `creditcd` | Suitable for one-hot encoding if retained as categorical values. |
| Medium cardinality categorical fields | `area` (19), `dwllsize` (15), `ethnic` (17) | One-hot encoding is possible, but compact encodings may be preferable if feature count matters. |
| High cardinality categorical fields | `crclscod` (54) | Better suited to target encoding or frequency encoding than one-hot encoding. |

### Non-Feature Columns

| Feature | Unique Values | Note |
|---|---:|---|
| `churn` | 2 | Target variable, not a feature. |
| `Customer_ID` | 100,000 | Identifier only, never a predictive feature. |

### Cardinality Takeaways

- `crclscod` is the only high-cardinality categorical predictor.
- `area`, `dwllsize`, and `ethnic` sit in the medium-cardinality range.
- Most other categorical fields are binary or low-cardinality and can be encoded safely with standard categorical methods.

## Data Quality Issues

The main data quality issues are structural rather than catastrophic, but they must be addressed before modeling.

### Primary Issues

- Heavy missingness in several `Client.csv` household variables.
- Numeric fields stored as text.
- Mixed code conventions across flag-like columns.
- Ambiguous or under-documented columns such as `recv_sms_Mean` and `iwylis_vce_Mean`.
- Possible redundancy or correlation across usage and revenue features.
- Need to confirm that merged records remain one-to-one on `Customer_ID`.

### Business Impact of These Issues

- Missing household variables may weaken model performance or bias the sample if dropped indiscriminately.
- Type-conversion mistakes can break downstream analysis.
- Ambiguous code handling can distort business interpretation.
- Redundant features can make the model harder to interpret and maintain.

## Leakage Risks

No direct leakage feature is obvious from the column names alone, but several fields require careful timing checks.

### Potential Leakage Candidates

- `change_mou`
- `change_rev`
- `avg3mou`
- `avg3rev`
- `avg6mou`
- `avg6rev`
- `months`

### Leakage Guidance

- These features may be legitimate if they are measured strictly before the churn window.
- If any feature reflects activity too close to or after the observation point, it should be excluded.
- `Customer_ID` is not leakage, but it must be excluded from modeling because it is only an identifier.
- `churn` must be isolated as the target and never used as an input feature.

## Dataset Strengths

- Clear one-to-one customer-level join structure.
- A labeled target variable is already present, enabling supervised learning.
- Rich mix of profile, household, handset, billing, and usage attributes.
- Nearly balanced target classes, which simplifies baseline training and evaluation.
- Business problem is well aligned with the available data and is easy to communicate.
- The dataset is large enough for robust modeling and segmentation work.

## Dataset Weaknesses

- Several important household and demographic variables have substantial missingness.
- The raw files require careful dtype cleaning before any serious analysis.
- Some columns are not fully documented and will need light verification.
- The dataset appears aggregated at the customer level, so temporal structure is limited.
- A few features may be correlated or redundant, which can complicate interpretation.
- The absence of a separate submission file reduces clarity on the exact downstream evaluation setup.

## Preparation Recommendations

Before EDA and modeling, the following steps should be completed:

1. Load both files with explicit dtype handling.
2. Keep `Customer_ID` as a string key and confirm uniqueness before merging.
3. Convert numeric features to numeric types and verify that no unexpected text tokens remain.
4. Recode binary and flag-style columns using a documented mapping.
5. Preserve ambiguous coded fields as categorical until their meaning is confirmed.
6. Handle missing values by feature group rather than applying one blanket strategy.
7. Exclude `churn` from predictors and retain it only as the label.
8. Inspect possible leakage candidates using timing logic from the business definition.
9. Encode categorical variables based on cardinality:
   - one-hot for low-cardinality fields
   - target or frequency encoding for high-cardinality fields
10. Build a merged analytical table only after the join key and typing are validated.

## Key Findings

- The project is a binary churn prediction problem for a wireless telecom retention use case.
- `Record.csv` is the primary modeling table because it contains the target `churn`.
- `Client.csv` adds useful customer context, but it also carries the largest missingness burden.
- The target is nearly balanced, with `0` at 50.44% and `1` at 49.56%.
- Most categorical predictors are low-cardinality; `crclscod` is the main high-cardinality field.
- The raw data requires explicit type cleanup because numeric fields are stored as text and many flags use coded strings.
- The most important data quality risk is not row count, but feature readiness: missingness, code mapping, and leakage timing must be handled before modeling.
- The merged dataset is well suited to downstream EDA, feature engineering, and classification once these preparation steps are complete.

### Source Documents Used

- `docs/2-dataset-understanding/dataset_inventory.md`
- `docs/2-dataset-understanding/dataset_schema.md`
- `docs/2-dataset-understanding/missing_value_analysis.md`
- `docs/2-dataset-understanding/data_type_validation.md`
- `docs/2-dataset-understanding/cardinality_analysis.md`
- `docs/2-dataset-understanding/target_understanding.md`
- `docs/business_understanding.md`
