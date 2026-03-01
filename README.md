## Maryam
🚀 Bank Marketing Prediction & Analysis

Authors: Sean, Armita, Jesse, ManKit, Maryam

📌 Project Overview

This project focuses on predictive modeling for bank marketing campaigns using the Bank Marketing Dataset. Our goal is to identify customers most likely to subscribe to a term deposit, reduce unnecessary calls, and improve campaign efficiency.

We implement an end-to-end machine learning pipeline, including data preprocessing, model development, and model improvement, to provide actionable insights for banking marketing strategy.

🔍 Dataset Information

The dataset contains details from direct marketing campaigns conducted by a Portuguese bank. Campaigns aim to convince clients to subscribe to term deposits via phone calls.

📌 Source: (https://archive.ics.uci.edu/dataset/222/bank+marketing)

📊 Size: 
There are multiple versions of the dataset, including

bank-additional-full.csv (41,188 examples with 20 inputs)

bank-full.csv (with 17 inputs)

Smaller subsets for testing.
🎯 Target Variable:y: indicates whether the client subscribed to a term deposit (yes / no) as the classification goal.

📁 Dataset Features
The dataset includes multiple feature types such as:

Client Information: age, job, marital, education

Financial Status: default, balance, housing, loan

Campaign Interaction: contact type, day, month, call duration, number of contacts

Economic Indicators: employment variation rate, consumer price index, confidence index, Euribor 3‑month rate, number of employees

Target Variable: y (term deposit subscription)

🔍 Business Motivation

Telemarketing is expensive and inefficient when calling every customer. Low conversion rates, wasted labor, and potential brand fatigue require a data-driven strategy.

Project Objectives:

Reduce operational waste by targeting high-probability leads.

Adapt campaigns to macro-economic changes (e.g., Euribor fluctuations).

Provide explainable AI insights to sales advisors using SHAP values.

Ensure regulatory compliance (OSFI E-23) for bias-free predictive models.

Stakeholders & Value:

Chief Distribution Officer (CDO): Maximize revenue per salesperson.

Chief Risk Officer (CRO): Ensure transparency and reduce liability.

Chief Marketing Officer (CMO): Lower acquisition cost and avoid client fatigue.

🔍 Risks & Uncertainties

Data Leakage: duration should not be used in predictive modeling.

Class Imbalance: ~89% of clients do not subscribe, which can bias models.

Unknown Categorical Values: job, education, default contain unknown.

Multi-collinearity: Economic features (e.g., emp.var.rate, euribor3m) may distort model interpretation.

Temporal Bias: Data from 2008–2010 may not reflect current economic conditions.

🏗️ Project Approach
1️⃣ Data Analysis & Preprocessing

Cleaning: Handle missing values and unknowns.

Exploration: Examine ratio vs. frequency, demographic and credit features, economic indicators.

Tasks:

Sean: Define and structure business question; explain campaign goals.

Armita: Analyze demographic and credit data.

Jesse: Analyze campaign interaction and macroeconomic data.

ManKit: Identify risks and potential bias in the dataset.

Maryam: Wrap up, task allocation, and document tools/technologies.

2️⃣ Model Development

Train models: Logistic Regression, Random Forest, XGBoost

Evaluate with accuracy, ROC-AUC, confusion matrix

Select best-performing model for improvement

3️⃣ Model Improvement

Use SHAP values to interpret predictions

Focus on false positives/negatives to improve precision

Identify key factors for subscription at individual and population level

📊 Key Questions to Answer

Which clients are most likely to subscribe to a term deposit?

At what point do additional calls become counterproductive?

How do interest rates and employment affect campaign success?

What are the distinct client personas for targeting?

Can we recommend top 3 reasons for each client for sales outreach?

How can the bank identify new high-value clients efficiently?

📂 Project Structure
📦 Bank-Marketing-Project
 ┣ 📂 data
 ┃ ┣ 📜 bank-additional-full.csv
 ┃ ┗ 📜 bank-additional-imputed.csv
 ┣ 📂 notebooks
 ┃ ┗ 📜 EDA_and_Modeling.ipynb
 ┣ 📜 README.md
 ┗ 📜 requirements.txt
🔥 How to Run the Project

1️⃣ Clone Repository

git clone https://github.com/MankitWong/Team_ML10.git


2️⃣ Install Dependencies

pip install -r requirements.txt

3️⃣ Run Jupyter Notebooks

jupyter notebook notebooks/EDA_and_Modeling.ipynb
🤝 Team Members & Contributions
Name	Role	Contribution
Sean	Business Strategy	Defined business question, motivation
Armita	Data Analysis	Demographics & credit features
Jesse	Data Analysis	Campaign & macroeconomic features
ManKit	Risk Assessment	Identified risks, bias, and uncertainties
Maryam	Project Documentation	Task allocation, methods, README
=======
# Team_ML10
## BUSINESS MOTIVATION
### THE PROBLEM

Banks face a structural problem: term deposits are low-margin products requiring high-touch sales. The current approach burns resources on inevitable rejections. We chose this question because it forces three disciplines:
Revenue operations: focus labor where probability justifies cost
Risk management: prove decisions are explainable and fair before regulators demand it
Data science: build models that work in production, not just in training

Telemarketing remains a primary channel to reach out to clients for term deposit acquisition,but conversion rates hover below 10%. The traditional approach to just call everyone generates three critical failures:

Economic waste: high-volume telemarketing campaigns represent substantial operational cost with minimal yield
Brand erosion: repeated unwanted contact hurts customer lifetime value
Regulatory exposure: OSFI Guideline E-23 (May 2027) mandates explainable, bias-free AI
Deployment risk: Our dataset mixes pre-campaign features (available before dialing) and post-campaign outcomes (only known only after contact). Models trained on both learn patterns they cannot access in production. We exclude post-campaign data to ensure the model predicts from the same information a salesperson has when deciding whom to call.

### THE OPPORTUNITY

Four-layer system to create a profit driven system:

Persona Discovery: K-Means segmentation, identify 4 micro-demographics with differentiated propensity
Regime Stress Testing: Random Forest + macro features, detect when Euribor >3% degrades reliability, adapt thresholds
Strategy Layer: routing by model score: high probability leads to sales calls, medium probability to marketing nurture before contact, low probability to other products
Governance: SHAP explainability and fairness audit, E-23 compliance with documented suitability defense

### SUCCESS METRICS

Model reliability: AUC >= 80% across economic regimes
Operational efficiency: 60% reduction in wasted sales calls
Revenue impact: value from single campaign cohort through less calls and higher conversion rate
Risk posture: zero proxy bias findings in automated audit

PRE-CAMPAIGN VS POST-CAMPAIGN
Pre-campaign features (what we know before dialing):
Client profile: age, job, marital status, education, existing products
Prior relationship: previous contacts, past campaign outcomes
Market conditions: Euribor rate, employment trends, consumer confidence
Post-campaign features (what we learn only after contact):
Call duration	
Final yes/no timing


The duration problem: Call length perfectly predicts success. Longer calls mean engaged clients who buy. But you cannot know duration before picking up the phone. Models trained on duration can show very high accuracy in testing but will fail completely in production.
Our constraint: Delete duration. Delete any feature created during or after the campaign. Build from pre-campaign information only. This sacrifices training accuracy for deployment reliability.	

### STAKEHOLDER VALUE

Chief Distribution Officer

Priority: revenue per headcount hour
Why they care: fixed sales team, productivity targets, bonus tied to team output
What they get: sales cockpit with waterfall plots, top-3 talking points per lead

Chief Risk Officer

Priority: audit readiness, personal liability protection
Why they care: E-23 enforcement May 2027, career risk, board accountability
What they get: SHAP-based adverse action notices, automated bias monitoring

Chief Marketing Officer

Priority: CAC reduction, brand health
Why they care: CAC is their KPI, churn hurts retention metrics, complaints damage brand
What they get: automated lead triage, thousands of low-propensity leads routed to email or other products instead of expensive outbound calls

## Risks And Uncertainties

The analysis of this dataset is subject to several risks and uncertainties:

1. Data Leakage from Feature Duration:
The 'duration' feature presents a risk of data leakage because the outcome is No for short calls or no answers. This information is unavailable prior to making a call, rendering the feature useless for real-world predictive modeling.

2. Severe Class Imbalance:
The dataset exhibits severe class imbalance, with approximately 89% of observations classified as No (customers not subscribing to the term deposit). This imbalance makes the model prone to defaulting to the No prediction, thereby failing to accurately identify the behavior of customers who do subscribe.

3. Uncertainty in Categorical Feature Encoding:
Several categorical features, including job, marital, education, default, housing, and loan, contain 'unknown' values. Improper handling of these unknowns could lead to issues like high dimensionality or the dummy variable trap.

4. Multi-collinearity among Economic Indicators:
The features emp.var.rate, cons.price.idx, and euribor3m are economic indicators and are expected to move together, leading to multi-collinearity. This can result in an unstable model that is difficult to interpret, as it struggles to distinguish the independent impact of one feature from another.

5. Temporal and Economic Bias:
The data was collected from a Portuguese banking institution between 2008 and 2010, a period encompassing two major financial crises: the collapse of Lehman Brothers and the eurozone sovereign debt crisis. This time frame introduces temporal and economic bias, as customer responses to campaigning during this unstable period may differ significantly from those in a normal market.



## Methods and Technologies
Methods
        Explore data: client info, finances, past campaigns, and economic factors.

        Measure campaign performance with conversion rate.

        Compare conversion rates by age, job, marital status, loan, and num of Calls.

        Build prediction models (Logistic Regression, Decision Tree, Random Forest).

        Identify key factors influencing subscriptions.

        Check diminishing returns from repeated calls.

        Analyze economic impact on subscription demand.

        Create visualizations and dashboards for insights.

Technologies

        Python: pandas, numpy, matßplotlib, seaborn, scikit-learn

        Jupyter Notebook for workflow

        GitHub for version control

        Markdown for documentation

        SQL for structured queries if needed

        Visualization app for dashboards and interactive charts main
