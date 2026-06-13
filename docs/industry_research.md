# Industry Research

## 1. Industry Overview
The discovered domain is **telecommunications**, specifically a wireless/mobile operator context.

Telecom operators run subscriber-facing businesses on top of large operational stacks: customer management, product and service design, billing, fulfillment, assurance, analytics, and network operations. TM Forum describes Open Digital Architecture (ODA) as a blueprint for flexible, cloud-based telecom and enterprise IT systems that helps operators simplify architecture, automate operations, and reduce cost. TM Forum also frames the telecom business around business leaders, enterprise architects, software developers, and IT operations teams. [TM Forum ODA](https://www.tmforum.org/oda/)

For this assignment, the data looks like a typical operator customer table: usage, billing, service quality, handset age, demographics, and churn history. That makes it suitable for retention, revenue, or customer-value modeling.

## 2. Important Industry Concepts
- **Churn**: customers terminating service within a defined period. In telecom, churn is one of the core retention metrics because switching costs are low and competition is intense. [Churn prediction paper](https://arxiv.org/abs/1911.00558)
- **ARPU**: average revenue per user. Telecom companies use it to track revenue generated per subscriber over a period, usually monthly. It is widely treated as a key telecom KPI. [ARPU definition](https://www.investopedia.com/terms/a/arpu.asp)
- **BSS / OSS**: business support systems and operations support systems. These are the systems used for customer management, billing, charging, service fulfillment, and network/service operations. TM Forum’s ODA separates business architecture, information systems, implementation, and deployment/runtime concerns. [TM Forum ODA](https://www.tmforum.org/oda/)
- **QoE / service experience**: customer experience and perceived service quality. Recent telecom churn research shows quality-of-experience indicators can be strong churn signals. [Subscriber retention framework](https://arxiv.org/abs/2606.04838)

## 3. Business Workflow
A practical telecom workflow usually looks like this:
1. Acquire the customer through sales or marketing.
2. Configure the offer and activate the service.
3. Deliver service through network and platform operations.
4. Bill, rate, and collect revenue.
5. Monitor usage, complaints, and service quality.
6. Trigger retention actions when risk rises.
7. Win back or close the account if churn happens.

That flow aligns with TM Forum’s process and architecture framing: business architecture, information systems, implementation, and deployment/runtime, plus the business process framework (eTOM). Telecom BI work also often treats order-to-payment as an end-to-end process for reporting and decision support. [TM Forum ODA](https://www.tmforum.org/oda/) [Order-to-payment paper](https://arxiv.org/abs/1401.0534)

## 4. Key Stakeholders
- **Executives / strategy leaders** who care about revenue growth, retention, and operating cost.
- **Sales and marketing teams** who choose offers, bundles, and retention campaigns.
- **Customer care teams** who handle complaints, service issues, and save offers.
- **Network and operations teams** who affect service quality and downtime.
- **Billing / finance teams** who track charges, collections, and ARPU.
- **Data / analytics teams** who build the model and monitor segment behavior.
- **IT architects and platform teams** who maintain BSS/OSS and customer-data systems.
- **Regulators and competitors** who shape pricing, portability, and market pressure.

TM Forum explicitly positions ODA for business leaders, enterprise architects, software developers, and IT operations teams, which matches the stakeholder mix above. [TM Forum ODA](https://www.tmforum.org/oda/)

## 5. Industry KPIs
The most relevant telecom KPIs for this project are:
- **Churn rate**: percentage of customers leaving in a period.
- **ARPU**: average revenue per user.
- **Subscriber growth / net additions**: whether the base is expanding.
- **Retention rate**: how many at-risk customers are saved.
- **Customer experience / QoE**: service quality as felt by the customer.
- **Billing and collection performance**: revenue realization and payment health.

Investopedia identifies ARPU, churn rate, and subscriber growth as core telecom evaluation metrics. Telecom research also shows churn modeling remains an operationally important task, and QoE features can be strong predictors. [Investopedia telecom metrics](https://www.investopedia.com/ask/answers/122414/what-are-best-metrics-evaluate-telecommunication-company.asp) [Subscriber retention framework](https://arxiv.org/abs/2606.04838)

## 6. Common Drivers of Success
- **High service quality** and low drop-off in customer experience.
- **Competitive pricing and useful bundles** that keep subscribers engaged.
- **Strong retention capability** for high-value customers.
- **Reliable billing and support** that reduces friction and complaints.
- **Automation and modern IT architecture** that lower cost and speed up change.
- **Data-driven segmentation** that lets teams target the right customers with the right action.

TM Forum emphasizes that composable software, autonomous operations, and AI/data adoption improve customer experience, business velocity, profitability, and operating cost. Telecom churn research also shows that usage and service-quality signals can be more predictive than simple demographic labels. [TM Forum ODA](https://www.tmforum.org/oda/) [Subscriber retention framework](https://arxiv.org/abs/2606.04838)

## 7. Why This Prediction Matters
Predicting churn matters because telecom is a recurring-revenue business. Losing a customer reduces future revenue, and winning a new customer is usually more expensive than keeping an existing one. Churn prediction gives the business a way to prioritize retention offers, service interventions, or handset upgrades before revenue is lost.

For this dataset, the `churn` target is especially useful because it is already labeled and nearly balanced, which makes the classification task straightforward and the model output easy to convert into an operational retention list. Telecom churn papers consistently treat churn prediction as a practical business intelligence problem in a competitive market. [Churn prediction paper](https://arxiv.org/abs/1911.00558) [Telecom churn comparison paper](https://arxiv.org/abs/1607.07792)

## Assumptions
- I am assuming Company A is a **mobile/wireless telecom operator**, not a fixed-line-only provider.
- I am assuming the business goal is **retention-focused** rather than a pure network engineering problem.
- I am assuming the final proposal will need a **customer ranking or risk score** that a sales, care, or retention team can act on.
- I am assuming telecom market structure and workflow are broadly similar to other subscriber-based wireless operators, even though the company is anonymous.

## References
- TM Forum. *About Open Digital Architecture (ODA)*. https://www.tmforum.org/oda/
- Investopedia. *ARPU: Definition, Calculation, and Application in Telecom and Media*. https://www.investopedia.com/terms/a/arpu.asp
- Investopedia. *What Are the Best Metrics to Evaluate a Telecommunications Company?* https://www.investopedia.com/ask/answers/122414/what-are-best-metrics-evaluate-telecommunication-company.asp
- Yang, L., Li, D., & Lu, Y. (2019). *Prediction Modeling and Analysis for Telecom Customer Churn in Two Months*. https://arxiv.org/abs/1911.00558
- Hassouna, M., Tarhini, A., Elyas, T., & AbouTrab, M. S. (2016). *Customer Churn in Mobile Markets: A Comparison of Techniques*. https://arxiv.org/abs/1607.07792
- Benhima, M., Reilly, J. P., Naamane, Z., Kharbat, M., Kabbaj, M. I., & Esqalli, O. (2014). *Design and implementation of the Customer Experience Data Mart in the Telecommunication Industry: Application Order-To-Payment end to end process*. https://arxiv.org/abs/1401.0534
- Mismar, F. B., Saleh, A., Pasaribu, I. M. P., & Syaifuddin, S. (2026). *From Network Experience to Subscriber Retention: An Explainable AI Framework for Mobile Operators*. https://arxiv.org/abs/2606.04838
