# Team_ML10

## BUSINESS MOTIVATION

### THE PROBLEM

Banks face a structural problem: term deposits are low‑margin products requiring high‑touch sales. The current approach burns resources on inevitable rejections. We chose this question because it forces three disciplines.

**Revenue operations:** focus labor where probability justifies cost.<br>**Risk management:** prove decisions are explainable and fair before regulators demand it.<br>**Data science:** build models that work in production, not just in training  

Telemarketing remains a primary channel to reach out to clients for term deposit acquisition, but conversion rates hover below 10%. The traditional approach to just call everyone generates three critical failures:

- **Economic waste:** high‑volume telemarketing campaigns represent substantial operational cost with minimal yield  
- **Brand erosion:** repeated unwanted contact hurts customer lifetime value  
- **Regulatory exposure:** OSFI Guideline E‑23 (May 2027) mandates explainable, bias‑free AI  
- **Deployment risk:** Our dataset mixes pre‑campaign features (available before dialing) and post‑campaign outcomes (only known after contact). Models trained on both learn patterns they cannot access in production. We exclude post‑campaign data to ensure the model predicts from the same information a salesperson has when deciding whom to call.  

### THE OPPORTUNITY

Four‑layer system to create a profit‑driven system:

1. **Persona Discovery:** K‑Means segmentation, identify 4 micro‑demographics with differentiated propensity  
2. **Regime Stress Testing:** Random Forest + macro features, detect when Euribor > 3 % degrades reliability, adapt thresholds  
3. **Strategy Layer:** routing by model score – high probability leads to sales calls, medium probability to marketing nurture before contact, low probability to other products  
4. **Governance:** SHAP explainability and fairness audit, E‑23 compliance with documented suitability defense  

### SUCCESS METRICS

- **Model reliability:** AUC ≥ 80 % across economic regimes  
- **Operational efficiency:** 60 % reduction in wasted sales calls  
- **Revenue impact:** value from single campaign cohort through less calls and higher conversion rate  
- **Risk posture:** zero proxy bias findings in automated audit  

#### PRE‑CAMPAIGN VS POST‑CAMPAIGN  

| **Pre‑campaign features** (what we know before dialing) | **Post‑campaign features** (what we learn only after contact) |
|----------------------------------------------------------|---------------------------------------------------------------|
| Client profile: age, job, marital status, education, existing products | Call duration |
| Prior relationship: previous contacts, past campaign outcomes | Final yes/no timing |

**The duration problem:** Call length perfectly predicts success. Longer calls mean engaged clients who buy. But you cannot know duration before picking up the phone. Models trained on duration can show very high accuracy in testing but will fail completely in production.  

**Our constraint: Delete duration.** Delete any feature created during or after the campaign. Build from pre‑campaign information only. This sacrifices training accuracy for deployment reliability.  

### STAKEHOLDER VALUE

#### Chief Distribution Officer  

- **Priority:** revenue per headcount hour  
- **Why they care:** fixed sales team, productivity targets, bonus tied to team output  
- **What they get:** sales cockpit with waterfall plots, top‑3 talking points per lead  

#### Chief Risk Officer  

- **Priority:** audit readiness, personal liability protection  
- **Why they care:** E‑23 enforcement May 2027, career risk, board accountability  
- **What they get:** SHAP‑based adverse action notices, automated bias monitoring  

#### Chief Marketing Officer  

- **Priority:** CAC reduction, brand health  
- **Why they care:** CAC is their KPI, churn hurts retention metrics, complaints damage brand  
- **What they get:** automated lead triage, thousands of low‑propensity leads routed to email or other products instead of expensive outbound calls  

## Risks And Uncertainties  

The analysis of this dataset is subject to several risks and uncertainties:

1. **Data Leakage from Feature Duration:**  
   The 'duration' feature presents a risk of data leakage because the outcome is No for short calls or no answers. This information is unavailable prior to making a call, rendering the feature useless for real‑world predictive modeling.  

2. **Severe Class Imbalance:**  
   The dataset exhibits severe class imbalance, with approximately 89 % of observations classified as No (customers not subscribing to the term deposit). This imbalance makes the model prone to defaulting to the No prediction, thereby failing to accurately identify the behavior of customers who do subscribe.  

3. **Uncertainty in Categorical Feature Encoding:**  
   Several categorical features, including job, marital, education, default, housing, and loan, contain 'unknown' values. Improper handling of these unknowns could lead to issues like high dimensionality or the dummy variable trap.  

4. **Multi‑collinearity among Economic Indicators:**  
   The features emp.var.rate, cons.price.idx, and euribor3m are economic indicators and are expected to move together, leading to multi‑collinearity. This can result in an unstable model that is difficult to interpret, as it struggles to distinguish the independent impact of one feature from another.  

5. **Temporal and Economic Bias:**  
   The data was collected from a Portuguese banking institution between 2008 and 2010, a period encompassing two major financial crises: the collapse of Lehman Brothers and the eurozone sovereign debt crisis. This time frame introduces temporal and economic bias, as customer responses to campaigning during this unstable period may differ significantly from those in a normal market.  





## Methods and Technologies

### Methods
- Explore data: client info, finances, past campaigns, and economic factors.  
- Measure campaign performance with conversion rate.  
- Compare conversion rates by age, job, marital status, loan, and num of Calls.  
- Build prediction models (Logistic Regression, Decision Tree, Random Forest).  
- Identify key factors influencing subscriptions.  
- Check diminishing returns from repeated calls.  
- Analyze economic impact on subscription demand.  
- Create visualizations and dashboards for insights.  

### Technologies
- Python: pandas, numpy, matßplotlib, seaborn, scikit-learn  
- Jupyter Notebook for workflow  
- GitHub for version control  
- Markdown for documentation  
- SQL for structured queries if needed  
- Visualization app for dashboards and interactive charts  