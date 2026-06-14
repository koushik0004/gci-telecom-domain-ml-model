# NOTEBOOK INVENTORY

## Scope

- Target notebook inspected: `Final Assignment/matsuo_final_assignment.ipynb`
- Reference notebook used for the inventory: `Final Assignment/tutorial.ipynb`

## Target Notebook Status

- The target notebook file is empty at the time of inspection.
- No existing cells were present to summarize in-place.

## Inventory From The Reference Notebook

### Dataframe Names

- `client`
- `record`
- `df`
- `df_clean`
- `X`
- `y`
- `X_train`
- `X_test`
- `y_train`
- `y_test`
- `model`

### Dataframe Shapes

- `client`: `(100000, 50)`
- `record`: `(100000, 51)`
- `df` after merge: `(100000, 100)`
- `df_clean` after dropping `Customer_ID`: `(100000, 99)`
- `X` used for modeling: `(100000, 98)`
- `y` target vector: `100000` rows

### Target Column

- `churn`

### Feature Count

- Features used for modeling after dropping `Customer_ID` and `churn`: `98`

### Preprocessing Sections

- Section `5.Preprocessing`
- Drop `Customer_ID`
- Identify `object`-dtype columns
- Apply `LabelEncoder` column by column

### Feature Engineering Sections

- No training-set feature engineering is persisted in the modeling pipeline.
- The only feature transformation outside preprocessing is the temporary log transform used for the pairplot in Section `3.5`.
- The modeling dataframe itself is not expanded with engineered features in the reference notebook.

### Train/Validation Split Logic

- `train_test_split(X, y, test_size=0.3, random_state=42, stratify=y)`
- The split is stratified by `churn`
- This creates a 70/30 train-test split

### Modeling Sections

- Section `6.Model Building (XGBoost)`
- `XGBClassifier` with:
  - `n_estimators=300`
  - `learning_rate=0.05`
  - `max_depth=6`
  - `eval_metric='logloss'`
  - `random_state=42`
- Evaluation uses:
  - `accuracy_score`
  - `confusion_matrix`
- Interpretation uses:
  - `plot_importance(..., importance_type='gain')`

## Validation Summary

- Modeling dataframe name used in the reference workflow: `df_clean`
- Target column: `churn`
- Current modeled row/column count before split: `(100000, 99)`
