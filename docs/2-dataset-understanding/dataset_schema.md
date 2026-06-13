# Dataset Schema

This schema is inferred from `docs/2-dataset-understanding/dataset_inventory.md`, `docs/project_discovery.md`, `docs/business_understanding.md`, and the dataset overview document. Descriptions include the source table so the location is visible inside the column notes.

## Column Classification Table

| Column | Type | Category | Description |
|---|---|---|---|
| `uniqsubs` | Integer | Numeric | Number of unique subscribers in the household (Client.csv) |
| `actvsubs` | Integer | Numeric | Number of active subscribers in the household (Client.csv) |
| `new_cell` | Boolean | Boolean | New cell phone user flag (Client.csv) |
| `crclscod` | String | Categorical | Credit class code (Client.csv) |
| `asl_flag` | Boolean | Boolean | Account spending limit flag (Client.csv) |
| `totcalls` | Integer | Numeric | Total number of calls over the life of the customer (Client.csv) |
| `totmou` | Float | Numeric | Total minutes of use over the life of the customer (Client.csv) |
| `totrev` | Float | Numeric | Total revenue over the life of the customer (Client.csv) |
| `adjrev` | Float | Derived Feature | Billing-adjusted total revenue over the life of the customer (Client.csv) |
| `adjmou` | Float | Derived Feature | Billing-adjusted total minutes of use over the life of the customer (Client.csv) |
| `adjqty` | Float | Derived Feature | Billing-adjusted total number of calls over the life of the customer (Client.csv) |
| `avgrev` | Float | Derived Feature | Average monthly revenue over the life of the customer (Client.csv) |
| `avgmou` | Float | Derived Feature | Average monthly minutes of use over the life of the customer (Client.csv) |
| `avgqty` | Float | Derived Feature | Average monthly number of calls over the life of the customer (Client.csv) |
| `avg3mou` | Float | Derived Feature | Average monthly minutes of use over the previous three months (Client.csv) |
| `avg3qty` | Float | Derived Feature | Average monthly number of calls over the previous three months (Client.csv) |
| `avg3rev` | Float | Derived Feature | Average monthly revenue over the previous three months (Client.csv) |
| `avg6mou` | Float | Derived Feature | Average monthly minutes of use over the previous six months (Client.csv) |
| `avg6qty` | Float | Derived Feature | Average monthly number of calls over the previous six months (Client.csv) |
| `avg6rev` | Float | Derived Feature | Average monthly revenue over the previous six months (Client.csv) |
| `prizm_social_one` | String | Categorical | Social group letter only (Client.csv) |
| `area` | String | Categorical | Geographic area (Client.csv) |
| `dualband` | Boolean | Boolean | Dualband handset indicator (Client.csv) |
| `refurb_new` | String | Categorical | Handset status: refurbished or new (Client.csv) |
| `hnd_price` | Float | Numeric | Current handset price (Client.csv) |
| `phones` | Integer | Numeric | Number of handsets issued (Client.csv) |
| `models` | Integer | Numeric | Number of models issued (Client.csv) |
| `hnd_webcap` | Boolean | Boolean | Handset web capability flag (Client.csv) |
| `truck` | Boolean | Boolean | Truck indicator (Client.csv) |
| `rv` | Boolean | Boolean | RV indicator (Client.csv) |
| `ownrent` | String | Categorical | Home owner or renter status (Client.csv) |
| `lor` | Float | Numeric | Length of residence (Client.csv) |
| `dwlltype` | String | Categorical | Dwelling unit type (Client.csv) |
| `marital` | String | Categorical | Marital status (Client.csv) |
| `adults` | Integer | Numeric | Number of adults in the household (Client.csv) |
| `infobase` | Boolean | Boolean | InfoBase match flag (Client.csv) |
| `income` | Float | Numeric | Estimated income (Client.csv) |
| `numbcars` | Integer | Numeric | Known number of vehicles (Client.csv) |
| `HHstatin` | String | Categorical | Premier household status indicator (Client.csv) |
| `dwllsize` | String | Categorical | Dwelling size (Client.csv) |
| `forgntvl` | Boolean | Boolean | Foreign travel dummy variable (Client.csv) |
| `ethnic` | String | Categorical | Ethnicity roll-up code (Client.csv) |
| `kid0_2` | Boolean | Boolean | Child aged 0 to 2 in household (Client.csv) |
| `kid3_5` | Boolean | Boolean | Child aged 3 to 5 in household (Client.csv) |
| `kid6_10` | Boolean | Boolean | Child aged 6 to 10 in household (Client.csv) |
| `kid11_15` | Boolean | Boolean | Child aged 11 to 15 in household (Client.csv) |
| `kid16_17` | Boolean | Boolean | Child aged 16 to 17 in household (Client.csv) |
| `creditcd` | Boolean | Boolean | Credit card indicator (Client.csv) |
| `eqpdays` | Integer | Numeric | Number of days since current equipment was obtained (Client.csv) |
| `Customer_ID` | String | ID | Unique customer identifier used for joining tables (Client.csv) |
| `rev_Mean` | Float | Derived Feature | Mean monthly revenue (charge amount) (Record.csv) |
| `mou_Mean` | Float | Derived Feature | Mean number of monthly minutes of use (Record.csv) |
| `totmrc_Mean` | Float | Derived Feature | Mean total monthly recurring charge (Record.csv) |
| `da_Mean` | Float | Derived Feature | Mean number of directory-assisted calls (Record.csv) |
| `ovrmou_Mean` | Float | Derived Feature | Mean overage minutes of use (Record.csv) |
| `ovrrev_Mean` | Float | Derived Feature | Mean overage revenue (Record.csv) |
| `vceovr_Mean` | Float | Derived Feature | Mean revenue of voice overage (Record.csv) |
| `datovr_Mean` | Float | Derived Feature | Mean revenue of data overage (Record.csv) |
| `roam_Mean` | Float | Derived Feature | Mean number of roaming calls (Record.csv) |
| `change_mou` | Float | Derived Feature | Percentage change in monthly minutes of use versus previous three-month average (Record.csv) |
| `change_rev` | Float | Derived Feature | Percentage change in monthly revenue versus previous three-month average (Record.csv) |
| `drop_vce_Mean` | Float | Derived Feature | Mean number of dropped voice calls (Record.csv) |
| `drop_dat_Mean` | Float | Derived Feature | Mean number of dropped data calls (Record.csv) |
| `blck_vce_Mean` | Float | Derived Feature | Mean number of blocked voice calls (Record.csv) |
| `blck_dat_Mean` | Float | Derived Feature | Mean number of blocked data calls (Record.csv) |
| `unan_vce_Mean` | Float | Derived Feature | Mean number of unanswered voice calls (Record.csv) |
| `unan_dat_Mean` | Float | Derived Feature | Mean number of unanswered data calls (Record.csv) |
| `plcd_vce_Mean` | Float | Derived Feature | Mean number of attempted voice calls placed (Record.csv) |
| `plcd_dat_Mean` | Float | Derived Feature | Mean number of attempted data calls placed (Record.csv) |
| `recv_vce_Mean` | Float | Derived Feature | Mean number of received voice calls (Record.csv) |
| `recv_sms_Mean` | Unknown | Unknown | Not described in the dataset overview; needs verification (Record.csv) |
| `comp_vce_Mean` | Float | Derived Feature | Mean number of completed voice calls (Record.csv) |
| `comp_dat_Mean` | Float | Derived Feature | Mean number of completed data calls (Record.csv) |
| `custcare_Mean` | Float | Derived Feature | Mean number of customer care calls (Record.csv) |
| `ccrndmou_Mean` | Float | Derived Feature | Mean rounded minutes of customer care calls (Record.csv) |
| `cc_mou_Mean` | Float | Derived Feature | Mean unrounded minutes of customer care calls (Record.csv) |
| `inonemin_Mean` | Float | Derived Feature | Mean number of inbound calls lasting less than one minute (Record.csv) |
| `threeway_Mean` | Float | Derived Feature | Mean number of three-way calls (Record.csv) |
| `mou_cvce_Mean` | Float | Derived Feature | Mean unrounded minutes of completed voice calls (Record.csv) |
| `mou_cdat_Mean` | Float | Derived Feature | Mean unrounded minutes of completed data calls (Record.csv) |
| `mou_rvce_Mean` | Float | Derived Feature | Mean unrounded minutes of received voice calls (Record.csv) |
| `owylis_vce_Mean` | Float | Derived Feature | Mean number of outbound wireless-to-wireless voice calls (Record.csv) |
| `mouowylisv_Mean` | Float | Derived Feature | Mean unrounded minutes of outbound wireless-to-wireless voice calls (Record.csv) |
| `iwylis_vce_Mean` | Unknown | Unknown | Not described in the dataset overview; needs verification (Record.csv) |
| `mouiwylisv_Mean` | Float | Derived Feature | Mean unrounded minutes of inbound wireless-to-wireless voice calls (Record.csv) |
| `peak_vce_Mean` | Float | Derived Feature | Mean number of peak voice calls (Record.csv) |
| `peak_dat_Mean` | Float | Derived Feature | Mean number of peak data calls (Record.csv) |
| `mou_peav_Mean` | Float | Derived Feature | Mean unrounded minutes of peak voice calls (Record.csv) |
| `mou_pead_Mean` | Float | Derived Feature | Mean unrounded minutes of peak data calls (Record.csv) |
| `opk_vce_Mean` | Float | Derived Feature | Mean number of off-peak voice calls (Record.csv) |
| `opk_dat_Mean` | Float | Derived Feature | Mean number of off-peak data calls (Record.csv) |
| `mou_opkv_Mean` | Float | Derived Feature | Mean unrounded minutes of off-peak voice calls (Record.csv) |
| `mou_opkd_Mean` | Float | Derived Feature | Mean unrounded minutes of off-peak data calls (Record.csv) |
| `drop_blk_Mean` | Float | Derived Feature | Mean number of dropped or blocked calls (Record.csv) |
| `attempt_Mean` | Float | Derived Feature | Mean number of attempted calls (Record.csv) |
| `complete_Mean` | Float | Derived Feature | Mean number of completed calls (Record.csv) |
| `callfwdv_Mean` | Float | Derived Feature | Mean number of call-forwarding voice calls (Record.csv) |
| `callwait_Mean` | Float | Derived Feature | Mean number of call-waiting calls (Record.csv) |
| `churn` | Boolean | Target | Binary churn outcome between 31 and 60 days after the observation date (Record.csv) |
| `months` | Integer | Numeric | Total number of months in service (Record.csv) |
| `Customer_ID` | String | ID | Unique customer identifier used for joining tables (Record.csv) |

## Target Variable Analysis

- `churn` is the target variable and is defined as churn occurring between 31 and 60 days after the observation date.
- The target is binary, so this is a supervised classification problem.
- The project notebook notes that the classes are close to balanced, which makes accuracy a reasonable first metric.
- Because the target is already present in `Record.csv`, that table is the primary modeling table.

## ID Columns

- `Customer_ID` in `Client.csv`
- `Customer_ID` in `Record.csv`
- The ID is required for merging but should not be used as a predictive feature.

## Potential Leakage Candidates

- No direct leakage feature is obvious from the column names alone.
- Recent-history fields such as `change_mou`, `change_rev`, `avg3mou`, and `avg3rev` should be checked to confirm they are measured strictly before the churn window.
- `months` should also be validated against the observation date so it is not acting as a post-outcome artifact.
- `Customer_ID` is not leakage, but it must be excluded from modeling because it is an identifier.

## Ambiguous Columns

- `recv_sms_Mean` and `iwylis_vce_Mean` were not explained in the dataset overview and need confirmation from EDA or source notes.
- `income` may be a numeric estimate or an ordinal bucket depending on source coding.
- `asl_flag`, `infobase`, `hnd_webcap`, `dualband`, and `creditcd` may be binary indicators even if they arrive as strings in the raw CSV.
- `dwllsize`, `HHstatin`, `crclscod`, and `prizm_social_one` are categorical, but their original code meanings may need light decoding for presentation.
