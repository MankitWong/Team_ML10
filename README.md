# ML Project – Team 10

| Section | Description |
|----------|-------------|
| **Business Motivation** | Provides the strategic context of the project, including the industry background, problem definition, core business question, and justification for why solving this problem creates measurable value. |
| **Data** | Introduces the dataset, its origin, structure, and key features. Explains variable categories, target definition, data granularity, and rationale for selecting this dataset for modeling. |
| **Risk** | Identifies modeling, data, operational, and ethical risks (e.g., data leakage, bias, overfitting, deployment risk) and outlines mitigation strategies to ensure real-world validity and robustness. |
| **Methods & Technologies** | Describes the analytical framework, modeling approaches, feature engineering strategy, evaluation metrics, and tools/technologies used (Python, ML libraries, visualization, etc.). |
| **Implementation Strategy** | Explains the step-by-step analytical plan for answering the business question, including preprocessing, modeling pipeline, validation design, and performance benchmarking. |
| **Stakeholder Value** | Defines how insights will be translated into actionable recommendations, tailored communication strategies for technical and non-technical stakeholders, and expected business impact. |
| **Team Roles & Accountability** | Clarifies responsibilities, ownership of deliverables, collaboration workflow, and quality control mechanisms within Team 10. |

# 📁 Project Structure

```bash
.
├── .gitignore
├── pyproject.toml
├── README.md
├── SETUP.md
│
├── analysis_output/
│   ├── campaign_fatigue.png
│   ├── euribor_impact.png
│   ├── feature_importance_proof.png
│   ├── shap_bar.png
│   └── shap_beeswarm.png
│
├── data/
│   └── raw/
│       └── bank-additional/
│           ├── bank-additional-full.csv
│           └── bank-additional-names.txt
│
├── extra/
│   └── initial_data_analysis.pptx
│
│
├── reports/
│   └── Bank_Campaign_Presentation_F.pptx
│
└── src/
    ├── main.ipynb
    └── data-analysis.ipynb
```
## BUSINESS MOTIVATION

### THE PROBLEM

Banks offer term deposits, fixed-term investment products where clients lock their funds for a guaranteed interest rate. While low-risk for customers, these products are low-margin for banks and rely heavily on high-touch sales strategies, primarily telemarketing.However the conversion rates hover below 10% meaning the approach burns resources on inevitable rejections.We therefore aim to answer the strategic question:

### BUSINESS QUESTION

**How can we increase subscription rates to term deposits while reducing telemarketing costs?**

### MOTIVATION

Our motivation forces three disciplines:

**Revenue operations:** focus labor where probability justifies cost.<br>**Risk management:** prove decisions are explainable and fair before regulators demand it.<br>**Data science:** build models that work in production, not just in training  

This is while The traditional approach to just call everyone generates two critical failures:

- **Economic waste:** high‑volume telemarketing campaigns represent substantial operational cost with minimal yield.  
- **Brand erosion:** repeated unwanted contact hurts customer lifetime value.  


## DATASET

The dataset used in this project is the Bank Marketing Dataset, a structured collection of client‑level, economic, and campaign‑interaction variables designed to support predictive modeling of term‑deposit subscription outcomes [http://archive.ics.uci.edu/ml/datasets/Bank+Marketing](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing)

### Core Characteristics  

- **Target variable:**  (yes/no subscription outcome)  

- **Feature types:**  

  - Categorical variables describing personal and campaign attributes.  
  - Numeric variables representing call metrics and macroeconomic indicators.  

- **Structure:** Tabular, with consistent formatting and no nested or unstructured fields.  

- **Source:** Bank marketing campaigns conducted over multiple periods.  

### Why This Dataset Was Selected  

- Rich mix of categorical and numeric features enables testing preprocessing pipelines such as one‑hot encoding and passthrough numeric handling.  

- Real‑world marketing context provides meaningful patterns for model interpretation and feature importance analysis.  

- Balanced complexity makes it appropriate for tree‑based models, logistic regression, and more advanced pipelines.  

- Includes known leakage‑prone variables, allowing exploration of model robustness and ethical modeling considerations.  

- Economic indicators add temporal and macroeconomic depth not found in typical customer datasets.  

### Feature Groups  

- **Demographics:** age, job, marital status, education  
- **Financial status:** housing loan, personal loan, default history  
- **Campaign interactions:** contact type, month, day of week, duration, campaign count, previous contacts  
- **Historical outcomes:** outcome  
- **Macroeconomic context:** employment variation rate, consumer price index, consumer confidence index, Euribor rate, number of employees  

### Suitability for Machine Learning  

- Supports binary classification with interpretable outputs.  
- Works well with Random Forests, Gradient Boosting, and logistic models.  
- Provides enough dimensionality for feature importance, SHAP analysis, and pipeline experimentation.  
- Clean structure reduces preprocessing overhead while still offering meaningful complexity.

## RISK

Dataset contains a structural modeling risk may causing information leakage, it mixes the pre-campaign and post-campaign information. If a model is trained on both categories, it will learn patterns that are not available at decision time, creating unrealistic performance and production failure risk.

To ensure real-world validity, we exclude all post-campaign variables and train the model only on information available at the moment a salesperson decides whom to call. We categorized our features as follow:

### PRE‑CAMPAIGN VS POST‑CAMPAIGN  

| **Pre‑campaign features** (what we know before dialing) | **Post‑campaign features** (what we learn only after contact) |
|----------------------------------------------------------|---------------------------------------------------------------|
| Client profile: age, job, marital status, education, existing products | Call duration |
| Prior relationship: previous contacts, past campaign outcomes | Final yes/no timing |

**The duration problem:** Call length perfectly predicts success. Longer calls mean engaged clients who buy. But you cannot know duration before picking up the phone. Models trained on duration can show very high accuracy in testing but will fail completely in production.  

**Our constraint: Delete duration.** Delete any feature created during or after the campaign. Build from pre‑campaign information only. This sacrifices training accuracy for deployment reliability.  

### Other Risks And Uncertainties  

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

## METHOD AND TECHNOLOGIES

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
- [Orange](https://orangedatamining.com/) for visualization, interactive dashboards and charts  
- Jupyter Notebook for workflow and markdowns 
- GitHub for version control      


## IMPLEMENTATION STRATEGY

We will answer "**How can we increase subscription rates to term deposits while reducing telemarketing costs?**" using pre-campaign analysis through four phases:

**PHASE 1: UNDERSTAND THE DATA**

We used some statistical methods to analyze and learn the data before moving forward with model development.

- Frequency versus ratio analysis: identify how ratio versus frequency matters to identify the segments look attractive by conversion rate but lack volume to scale(e.g high frequency of admin job in dataset due to receiving higher volume of call while extracting the ratio showed us job category of 'student' had higher conversion rate while reciving less colum of call)
- Demographic deep dive: age, job, marital status, education patterns
- Financial profile: existing loans, housing status, default history
- Interaction history: prior campaigns, contact fatigue, channel preferences
- Economic context: Euribor rates, employment trends, consumer confidence

**Key risk:** The duration column creates data leakage. We delete it. The model must predict from information available before dialing, not after.

---

**PHASE 2: BUILD AND COMPARE MODELS**

Start simple, then add complexity:

- **Baseline:** Logistic Regression (interpretable benchmark)
- **Standard:** Random Forest (handles non-linear relationships, feature interactions)
- **Advanced:** XGBoost or feature-engineered improvements (if justified by lift)

Validation: Stratified cross-validation preserving class imbalance
Metric: AUC-ROC (handles imbalance better than accuracy)

**Selection criteria:** Highest AUC with stable performance across economic regimes. Prefer a simpler model if advanced adds minimal lift.

---

**PHASE 3: EXPLAIN AND IMPROVE**

- SHAP global analysis: which features drive predictions across all leads
- Waterfall plots: individual lead explanations for sales cockpit
- Confusion matrix analysis: identify false positive and false negative patterns
- False positives: wasted calls on unlikely buyers
- False negatives: missed opportunities we incorrectly rejected

**Improvement loop:** Re-engineer features or adjust thresholds based on error patterns. Only add complexity if it improves business metrics.

---

**PHASE 4: OPERATIONALIZE**

- Tri-path routing by score: sales calls, marketing nurture, or pivot to other products
- Regime detection: pause or adjust thresholds when macro indicators signal model degradation
- Governance layer: automated fairness audit for E-23 compliance

---

**DELIVERABLE**

A production-ready model with:
- Pre-campaign feature set only
- AUC >= 80% across economic regimes
- SHAP explanations for every prediction
- Automated bias monitoring
- Routing rules that reduce wasted calls while protecting revenue



## STAKEHOLDER VALUE

### Chief Distribution Officer  

- **Priority:** revenue per headcount hour  
- **Why they care:** fixed sales team, productivity targets, bonus tied to team output  
- **What they get:** sales cockpit with waterfall plots, top‑3 talking points per lead  

### Chief Risk Officer  

- **Priority:** audit readiness, personal liability protection  
- **Why they care:** E‑23 enforcement May 2027, career risk, board accountability  
- **What they get:** SHAP‑based adverse action notices, automated bias monitoring  

### Chief Marketing Officer  

- **Priority:** CAC reduction, brand health  
- **Why they care:** CAC is their KPI, churn hurts retention metrics, complaints damage brand  
- **What they get:** automated lead triage, thousands of low‑propensity leads routed to email or other products instead of expensive outbound calls  


***

## TEAM ROLES & ACCOUNTABILITY
To ensure efficient execution and satisfy course requirements, we have divided the project into five distinct functional roles. *Note: Every member is required to create, review, and merge at least one independent Pull Request (PR) during the execution phase.*

*   **[Sean Brennan] – Business Strategy & Governance**
    *   **Focus:** Aligning the model with business ROI and regulatory standards.
    *   **Tasks:** Design the Tri-Path routing logic (Sales vs. Nurture vs. Pivot), execute the OSFI E-23 automated fairness audit, translate confusion matrix results into P&L impact, and coordinate daily Agile standups.
*   **[Armita Kharmandar] – Machine Learning Modeler**
    *   **Focus:** Predictive accuracy and algorithm architecture.
    *   **Tasks:** Develop the baseline Logistic Regression and standard Random Forest models, handle the severe class imbalance (via stratified sampling or SMOTE), and evaluate model performance across different economic regimes using AUC-ROC.
*   **[Man Kit Wong] – Model Explainability (XAI) Specialist**
    *   **Focus:** Model transparency and sales enablement.
    *   **Tasks:** Implement SHAP to extract global feature importance, generate individual Waterfall plots for the "Sales Cockpit," and analyze false-positive/false-negative error patterns to identify model blind spots.
*   **[Jesse Segura] – Exploratory Data Analysis (EDA) Specialist**
    *   **Focus:** Behavioral profiling and visual insights.
    *   **Tasks:** Conduct "Frequency vs. Ratio" analysis, generate visualizations for demographic and financial profiles, and identify baseline conversion fatigue (the 3-strike rule) before modeling begins.
*   **[Maryam Abedinnejad] – Data Engineer**
    *   **Focus:** Data integrity, cleaning, and feature preparation.
    *   **Tasks:** Hard-code the removal of the `duration` column to prevent temporal leakage, map categorical variables, handle `unknown` data points, and engineer features (e.g., converting `pdays` into a binary contact history). 

*** 

## Credits and Personal Links
* [Sean Brennan](https://drive.google.com/file/d/1xTUQjWs94MWE0gM1yqq5Q084nvzp34Zo/view?usp=sharing)
* [Armita Kharmandar](https://drive.google.com/file/d/1jSaBp0NF4m-f02zXtONMbGQR9-uEcKNx/view?usp=drive_link)
* [Man Kit Wong](https://drive.google.com/file/d/18DNRj-pAzUH8VdX5Sw5lgF4EV13gVF3Y/view?usp=share_link)
* [Jesse Segura](https://www.youtube.com/watch?v=qrllMGGGlOA)
* [Maryam Abedinnejad](https://drive.google.com/file/d/1oE5lW3xZPoL5NhqPWPgbnvY7ew75oLk3/view)

***


