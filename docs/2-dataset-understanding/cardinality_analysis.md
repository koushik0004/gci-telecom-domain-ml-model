# Cardinality Analysis

Unique values were counted directly from the raw CSV files using non-empty cells only. Cardinality is classified as:

- Low Cardinality: fewer than 10 unique values
- Medium Cardinality: 10 to 50 unique values
- High Cardinality: more than 50 unique values

This analysis focuses on categorical predictor fields. `Customer_ID` and `churn` are listed separately because they are an identifier and the target variable, not encoding candidates.

## Cardinality Table

| Feature | Unique Values | Classification |
| --- | ---: | --- |
| new_cell | 3 | Low Cardinality |
| crclscod | 54 | High Cardinality |
| asl_flag | 2 | Low Cardinality |
| prizm_social_one | 5 | Low Cardinality |
| area | 19 | Medium Cardinality |
| dualband | 4 | Low Cardinality |
| refurb_new | 2 | Low Cardinality |
| hnd_webcap | 4 | Low Cardinality |
| truck | 2 | Low Cardinality |
| rv | 2 | Low Cardinality |
| ownrent | 2 | Low Cardinality |
| dwlltype | 2 | Low Cardinality |
| marital | 5 | Low Cardinality |
| infobase | 2 | Low Cardinality |
| HHstatin | 6 | Low Cardinality |
| dwllsize | 15 | Medium Cardinality |
| forgntvl | 2 | Low Cardinality |
| ethnic | 17 | Medium Cardinality |
| kid0_2 | 2 | Low Cardinality |
| kid3_5 | 2 | Low Cardinality |
| kid6_10 | 2 | Low Cardinality |
| kid11_15 | 2 | Low Cardinality |
| kid16_17 | 2 | Low Cardinality |
| creditcd | 2 | Low Cardinality |

## Encoding Candidates

### Potential One-Hot Encoding Candidates

These fields are small enough to expand safely with one-hot encoding:

- `new_cell`
- `asl_flag`
- `prizm_social_one`
- `dualband`
- `refurb_new`
- `hnd_webcap`
- `truck`
- `rv`
- `ownrent`
- `dwlltype`
- `marital`
- `infobase`
- `HHstatin`
- `forgntvl`
- `kid0_2`
- `kid3_5`
- `kid6_10`
- `kid11_15`
- `kid16_17`
- `creditcd`

### Potential Target Encoding Candidates

These fields have enough categories that one-hot encoding may start adding avoidable sparsity:

- `crclscod`
- `area`
- `dwllsize`
- `ethnic`

### Potential Frequency Encoding Candidates

These fields can also be represented by category frequency when a compact signal is preferred:

- `crclscod`
- `area`
- `dwllsize`
- `ethnic`

## Non-Feature Categorical Columns

| Feature | Unique Values | Classification | Note |
| --- | ---: | --- | --- |
| churn | 2 | Low Cardinality | Target variable, not a feature |
| Customer_ID | 100000 | High Cardinality | Identifier used for joins, not a feature |

## Interpretation Notes

- `crclscod` is the clearest high-cardinality category in the dataset and is the most likely candidate for target or frequency encoding.
- `area`, `dwllsize`, and `ethnic` are medium-cardinality categories. One-hot encoding is still possible, but compact encodings may be easier to manage if the final feature matrix needs to stay small.
- The many binary or near-binary household and device flags are straightforward one-hot candidates if they are retained as categorical values.
- `Customer_ID` should never be encoded as a predictive feature.
