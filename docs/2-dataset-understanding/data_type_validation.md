# Data Type Validation

The raw CSV files store every field as text on ingestion, so validation here is about semantic typing rather than file-format typing. No dates were found in either dataset.

## Detected Issues

### Numeric stored as text

All numeric fields are encoded as text in the raw CSVs and should be cast before analysis.

- `Client.csv`: `uniqsubs`, `actvsubs`, `totcalls`, `totmou`, `totrev`, `adjrev`, `adjmou`, `adjqty`, `avgrev`, `avgmou`, `avgqty`, `avg3mou`, `avg3qty`, `avg3rev`, `avg6mou`, `avg6qty`, `avg6rev`, `hnd_price`, `phones`, `models`, `lor`, `adults`, `income`, `numbcars`, `eqpdays`
- `Record.csv`: `rev_Mean`, `mou_Mean`, `totmrc_Mean`, `da_Mean`, `ovrmou_Mean`, `ovrrev_Mean`, `vceovr_Mean`, `datovr_Mean`, `roam_Mean`, `change_mou`, `change_rev`, and all remaining `_Mean` metrics, plus `months`

### IDs stored as numeric-like text

- `Customer_ID` in both files is stored as digits-only text.
- It should remain a string or identifier type, not be converted to a numeric field, to avoid accidental interpretation as a measurable value.

### Columns whose raw codes do not behave like clean booleans

Several schema-level flag fields are not represented as native booleans in the CSV and need explicit mapping.

- `new_cell` uses values such as `Y`, `N`, and `U`
- `asl_flag` uses values such as `Y` and `N`
- `dualband` uses `Y` and `N`
- `truck`, `rv`, `forgntvl`, and `churn` use `0` and `1`
- `creditcd` uses `Y` and `N`
- `kid0_2`, `kid3_5`, `kid6_10`, `kid11_15`, `kid16_17` use coded values such as `U` and `Y`
- `infobase` uses `M`, which does not read as a direct boolean value

### Categorical codes stored as text

These are not type errors, but they should stay categorical rather than being coerced into numeric fields.

- `crclscod`, `prizm_social_one`, `area`, `refurb_new`, `ownrent`, `dwlltype`, `marital`, `HHstatin`, `dwllsize`, `ethnic`, `hnd_webcap`

### Mixed-type columns

- No true mixed-type columns were detected in the raw CSV structure.
- The only variation observed is between empty cells and coded values, which is a missing-value issue rather than a mixed-type problem.

### Dates stored as strings

- No date or timestamp columns were found in the dataset.

## Recommended Type Conversions

- Convert all numeric measurement columns to `int64`, `float64`, or nullable numeric types depending on whether decimals are present.
- Keep `Customer_ID` as a string identifier in both tables.
- Convert `churn` to a binary target representation only after confirming the intended label mapping.
- Convert flag-like fields to consistent binary or categorical encodings based on their business meaning:
  - `new_cell`, `asl_flag`, `dualband`, `creditcd`
  - `truck`, `rv`, `forgntvl`
  - `kid0_2`, `kid3_5`, `kid6_10`, `kid11_15`, `kid16_17`
- Keep code-based demographic and household fields as categorical/string values:
  - `crclscod`, `prizm_social_one`, `area`, `refurb_new`, `ownrent`, `dwlltype`, `marital`, `HHstatin`, `dwllsize`, `ethnic`, `hnd_webcap`
- Validate `infobase` separately before deciding whether it is a flag, a coded category, or a special lookup value.

## Data Quality Risks

- If numeric fields stay as strings, downstream aggregations, scaling, and model training will fail or behave incorrectly.
- If `Customer_ID` is converted to numeric, future joins and exports can become fragile and the field may be treated as predictive noise.
- If coded flags are misread as booleans without mapping, categories such as `U`, `M`, or `NA` can be collapsed incorrectly.
- If `infobase` and `hnd_webcap` are forced into boolean form too early, business meaning may be lost.
- Any silent coercion of malformed text to numeric `NaN` could hide data quality problems.

## Preparation Requirements for EDA

- Load both CSVs with explicit dtype handling instead of relying on automatic inference.
- Standardize blank cells to missing values before conversion.
- Cast numeric columns to numeric dtypes and verify that no unexpected text tokens appear.
- Preserve `Customer_ID` as a string key and confirm uniqueness before merging.
- Recode target and flag columns with a documented mapping table.
- Keep ambiguous coded fields as categorical until the codebook is confirmed.
- Separate the target column `churn` from feature preparation so it is not accidentally transformed with predictors.
