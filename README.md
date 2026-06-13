# Final Assignment

This project is a telecom business-proposal assignment built around anonymous customer data from **Company A**. The goal is to use EDA and at least one model to support a clear business recommendation, not to maximize model accuracy for its own sake.

## Project Summary

We are working with two linked tables:

- `Final Assignment/telecom/Client.csv`
- `Final Assignment/telecom/Record.csv`

They join on `Customer_ID` and describe roughly 100,000 customers with account, usage, billing, service-quality, and handset information.

## Problem Statement

The core problem is customer churn in a wireless telecom setting.

We want to identify customers who are likely to leave early enough to support a targeted retention action. The main working target in the provided materials is `churn`, defined as churn occurring 31-60 days after the observation date. Since the target is binary and close to balanced, this is naturally a classification problem.

The business goal is not just prediction. It is to turn the model output into a practical retention proposal that reduces avoidable churn and protects recurring revenue.

## Domain Context

This is a telecom retention problem. In this domain, churn, ARPU, usage decline, service quality, and handset age are all relevant signals. A brief takeaway from the research is that customers often show behavioral warning signs before they leave, which makes retention modeling useful for prioritizing intervention.

## Project Discovery

Key discovery points from the provided materials:

- Company A is an anonymous wireless telecom operator with historical customer data.
- The assignment expects EDA, at least one model, and a business proposal with quantified impact.
- The tutorial notebook uses churn as the worked example, but other targets could also be justified if they better support the proposal.
- `Customer_ID` is the join key and should not be used as a predictive feature.
- The provided data contains missing values and mixed data types, so preprocessing is required before modeling.
- Accuracy and a confusion matrix are the reference evaluation tools for the churn example because the classes are roughly balanced.

## What This Repo Contains

- `docs/`
  - project discovery notes
  - industry research notes
  - business understanding notes
  - hypothesis seeds
- `Final Assignment/`
  - notebook walkthrough
  - dataset overview
  - source CSV files
- `Sample Slides from Past Outstanding Students/`
  - reference presentation examples
- `final_assignment_tutorial.pdf`
  - exported tutorial reference

## Working Direction

The current working solution is:

- analyze the telecom customer data,
- model churn risk,
- identify the signals most associated with churn,
- and translate those findings into a retention recommendation with business value.

## Reference Materials

- `docs/project_discovery.md`
- `docs/industry_research.md`
- `docs/business_understanding.md`
- `docs/hypothesis_seeds.md`
- `Final Assignment/tutorial.ipynb`
- `Final Assignment/ENG_Company _A_ Dataset Overview.docx`

