# Business Understanding

## 1. Business Context
Company A is a wireless telecom operator with historical customer, usage, billing, and handset data. The assignment is framed as a consulting-style PoC: use the data to define a business problem, build a model, and turn the result into a proposal that a business team can act on.

The most natural business setting is customer retention. Telecom is a recurring-revenue business, so losing customers directly reduces future revenue and weakens growth. The provided data includes a labeled `churn` field, which makes churn-risk analysis the clearest starting point.

## 2. Business Problem
The business problem is that Company A likely cannot identify which customers are at risk of leaving early enough to intervene efficiently.

Without a ranking or risk score, retention actions are broad and expensive. The company may spend on customers who would have stayed anyway, while missing customers who are about to churn. The dataset suggests that churn may be related to usage decline, revenue changes, service-quality signals, and handset age, but those signals need to be tested and combined.

## 3. Business Objective
The business objective is to reduce avoidable customer churn and protect recurring revenue.

The intended business outcome is not simply a better model score. It is a more effective retention strategy:
- identify high-risk customers earlier,
- target them with the right retention action,
- reduce revenue loss from churn,
- and concentrate effort on the customers most worth saving.

## 4. AI/ML Objective
The AI/ML objective is to build a binary classification model that predicts whether a customer is likely to churn.

The model should:
- output a churn risk score or class label,
- use features that are available before churn happens,
- provide enough signal to prioritize intervention,
- and support explanation of which factors are associated with churn risk.

This is a prediction problem, not a causal proof. The model will identify risk patterns that are useful for decision-making, but it will not by itself prove which intervention causes retention.

## 5. Stakeholders
- **Executives**: care about revenue retention, customer lifetime value, and campaign ROI.
- **Sales / retention teams**: use the model to choose which customers receive offers or outreach.
- **Customer care teams**: act on service complaints, save offers, and escalation workflows.
- **Marketing teams**: design retention campaigns and segment-specific messaging.
- **Finance teams**: estimate cost, retained revenue, and campaign impact.
- **Data / analytics teams**: build, validate, and monitor the model.
- **Operations / network teams**: may need to fix service issues if they are part of the churn driver set.

## 6. Risks of Wrong Predictions
- **False positives**: customers predicted to churn who would have stayed. This wastes retention budget and can create unnecessary discounting.
- **False negatives**: customers predicted to stay who actually churn. This is usually more expensive because the company loses future revenue and misses the chance to intervene.
- **Misleading feature interpretation**: a feature may be predictive without being actionable, which can lead to poor business decisions.
- **Leakage or unstable signals**: if a feature captures post-churn information or a data artifact, the model may look good in testing but fail in practice.

## 7. Benefits of Correct Predictions
- **Targeted retention**: focus offers and outreach on customers most likely to leave.
- **Higher revenue preservation**: keep more recurring revenue in the base.
- **Lower retention cost**: avoid spending on low-risk customers.
- **Better segmentation**: learn which customer groups or behaviors matter most.
- **Operational prioritization**: route service or care resources to the accounts where intervention is most valuable.

## 8. Success Criteria
The business and modeling work should be considered successful if:
- the churn model performs better than a naive baseline,
- the selected features make business sense and are available before churn,
- the model can rank customers for action,
- the proposal ties model output to a concrete intervention,
- and the final recommendation can be explained in plain business language.

For the final assignment, success also requires a quantified business case, not just a predictive result.

## 9. Expected Business Impact
The expected impact is improved retention and better use of campaign spend.

If the model reliably identifies high-risk customers, Company A can:
- reduce churn-related revenue loss,
- improve retention campaign ROI,
- prioritize valuable customers,
- and potentially improve customer experience by intervening before dissatisfaction becomes churn.

The exact monetary impact will depend on assumptions such as average revenue per customer, the cost of an intervention, the save rate of the intervention, and the share of churners captured by the model. Those assumptions should be made explicit in the later business proposal.

## 10. Open Questions
- What retention action will Company A actually take for a high-risk customer?
- Should the proposal optimize for churn reduction, revenue retention, or customer-value protection?
- Which features are truly available before the decision point, and which should be excluded?
- What campaign cost and save-rate assumptions are reasonable for quantifying impact?
- Should the model prioritize recall, precision, or a balanced metric depending on the cost of misses versus wasted outreach?
- Is churn the best business target, or would a related target like revenue decline better support the final proposal?
