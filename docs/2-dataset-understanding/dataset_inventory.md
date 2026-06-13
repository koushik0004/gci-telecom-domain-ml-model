# Dataset Inventory

This project contains two customer-level source tables for a wireless telecom churn study. Both tables join on `Customer_ID` and together form the full analytical dataset for the assignment.

## Dataset Summary Table

| Dataset | Rows | Columns | Purpose |
|---|---:|---:|---|
| `Final Assignment/telecom/Client.csv` | 100,000 | 50 | Customer profile and account attributes such as household, handset, demographic, and subscription fields. |
| `Final Assignment/telecom/Record.csv` | 100,000 | 51 | Usage, revenue, service-quality, and outcome fields, including the churn target. |
| Submission dataset | N/A | N/A | No separate submission file is provided in the project workspace. |

## Dataset Relationships

- `Client.csv` and `Record.csv` are linked by the shared key `Customer_ID`.
- The relationship is one-to-one at the customer level.
- `Record.csv` is the primary analytical table because it contains the target variable `churn`.
- `Client.csv` is the auxiliary table because it adds customer profile and household context.
- A merged customer table is the expected working dataset for EDA and modeling.
- No separate test, sample submission, or lookup table is present in the workspace.

## Initial Observations

- The available data is already organized around a clear customer-level unit of analysis.
- The dataset is split by feature group: `Client.csv` holds profile/account fields, while `Record.csv` holds behavioral and outcome fields.
- `churn` appears only in `Record.csv`, so the modeling task naturally centers on churn prediction.
- Both tables have the same row count, which suggests they are designed to be merged without record loss if `Customer_ID` is unique.
- The feature set appears mixed in type, with numeric, categorical, and identifier-like columns.
- The inventory supports a straightforward supervised learning workflow after merge, cleaning, encoding, and missing-value handling.

## Potential Risks

- `Customer_ID` is an identifier and should not be used as a predictive feature.
- Some columns may contain missing values, which can affect row retention and model performance if not handled carefully.
- Categorical columns may require encoding before modeling.
- There may be redundant or highly correlated features across usage and revenue fields.
- Because the data is already aggregated by customer, there is limited room to validate temporal ordering unless the original notebook or documentation is consulted.
- If the final model uses a merged table, duplicate or non-unique keys would create merge issues, so key integrity should be checked before analysis.
