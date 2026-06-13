# Project Discovery

## 1. Project Overview
This assignment is a telecom business-proposal task built around Company A's anonymous customer data. The goal is not just to model the data, but to turn EDA and at least one machine learning model into a clear executive proposal with quantified business impact.

The reference notebook frames the work as a consulting-style PoC: understand the dataset, define a business problem, build a model, and translate the results into an actionable recommendation.

## 2. Competition Objective
The core objective is to analyze Company A's customer data and propose a business action supported by data. The official materials emphasize:
- run EDA on the provided dataset,
- build at least one ML or statistical model,
- name the model, evaluation metric, and score,
- explain how the model supports the business proposal,
- deliver a presentation of up to 15 slides plus references and a notebook.

## 3. Target Variable
The tutorial notebook uses `churn` as the worked example target.

From the dataset overview, `churn` is defined as:
- `churn`: instance of churn between 31-60 days after the observation date

This is a binary target and the notebook explicitly notes that other targets could also be justified, but `churn` is the clearest default example in the provided materials.

## 4. Prediction Type
`churn` implies a binary classification task.

The reference notebook uses this to motivate a classifier and evaluates performance on a held-out test split. Because the class balance is close to 50/50, accuracy is considered meaningful in the tutorial.

## 5. Evaluation Metric
The tutorial uses:
- `accuracy` as the main metric
- `confusion matrix` as the companion diagnostic

The notebook's justification is that the target classes are roughly balanced, so accuracy is not misleading in this case.

## 6. Available Files
Files found in the project workspace:

- `prompts/1-project-discovery.md`
- `prompts/2-industry-research.md`
- `prompts/3-business-understanding.md`
- `prompts/4-hypothesis-seed-generation.md`
- `Final Assignment/README.docx`
- `Final Assignment/tutorial.ipynb`
- `Final Assignment/ENG_Company _A_ Dataset Overview.docx`
- `Final Assignment/telecom/Client.csv`
- `Final Assignment/telecom/Record.csv`
- `final_assignment_tutorial.pdf`
- `Sample Slides from Past Outstanding Students/Sample1.pptx`
- `Sample Slides from Past Outstanding Students/Sample2.pptx`

## 7. Dataset Structure
The dataset is split into two linked tables joined by `Customer_ID`.

### `Client.csv`
- 100,000 rows
- 50 columns
- one row per customer
- mostly account, demographic, handset, and household variables

### `Record.csv`
- 100,000 rows
- 51 columns
- one row per customer
- usage, billing, call-quality metrics, plus `churn` and `months`

### Join structure
- Shared key: `Customer_ID`
- The tutorial performs a 1:1 inner merge

### Important observations from the provided materials
- `churn` is nearly balanced: 49,562 churned vs 50,438 stayed
- There are missing values in several columns
- Some columns are categorical/object typed and need encoding for standard ML workflows
- `Customer_ID` is an identifier, not a predictive feature

## 8. Initial Understanding
The problem appears to be customer retention for a telecom provider.

The provided materials suggest a plausible story:
- customers with older equipment may be more likely to churn,
- usage, revenue, and service-quality variables may jointly explain churn risk,
- a model can rank customers by risk so the business can target retention actions more efficiently.

The tutorial also points out that this dataset supports more than one business question. Churn is the default example, but revenue, usage, equipment age, or segment-level behavior could also be viable if they better support the final proposal.

## 9. Questions / Unknowns
- Which business action will actually be proposed for high-risk customers: retention offer, service call, handset upgrade, or plan change?
- Which columns are the most reliable predictors after missingness and redundancy are handled?
- Are any variables leaking future information or too directly tied to the target?
- Which segments matter most for a proposal: geography, plan type, handset age, income, or tenure?
- Is churn the strongest business target, or would revenue retention or usage expansion create a better proposal?
- What cost, revenue, or retention assumptions should be used to quantify impact in the final slides?
