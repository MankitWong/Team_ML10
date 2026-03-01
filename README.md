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