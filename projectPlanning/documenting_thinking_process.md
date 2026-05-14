# 🏦 DataQuest2026 Project — Interpretable Credit Modelling

## 🧩 Problem Statement

The challenge is to improve how a retail lending company evaluates loan applications. Using a historical loan-book dataset, the goal is to predict whether an applicant will default within 12 months. The solution must be **interpretable**, specifically logistic regression, so that risk managers, business stakeholders, and regulators can trust and understand the decisions.

-----------------------------
### 🛠️ Solution Approach

The solution begins with a mental map of the workflow before any code is written. The steps are:

- Structure the project into **three repositories** — Data, EDA Tool, and Model — to improve reliability and scalability.

- Conduct **Exploratory Data Analysis (EDA)** to uncover risk patterns.

- Apply **feature engineering** (WoE encoding, ratios, binning) to improve logistic regression performance.

- Build an **interactive Streamlit app** for EDA, model evaluation, and business decision support.

- Extend the app with a **business value dashboard** to show how approval thresholds affect risk and profitability.

- Prepare a **PowerPoint presentation** with embedded video and script to communicate findings clearly to judges and stakeholders.

-----------------------------
### 📋 Requirements

To solve the problem, the following are required:

- A **historical loan dataset** (~120k rows × 26 columns).

- Knowledge of **credit modelling concepts** (GLMs, WoE, IV, AUC, Gini, Precision, Recall).

- A structured workflow: cleaning, feature engineering, modelling, evaluation, deployment.

- Tools for **visualization**, **modelling**, and **reproducibility**.

----------------------------
### ⚙️ Tools Selected

- **Databricks:**          for data infrastructure, pipeline management, and modelling.

- **Python:**              for EDA, feature engineering, and building the Streamlit app.

- **Streamlit:**           for interactive dashboards and visualizations.

- **draw.io:**             for diagramming the medallion architecture and project planning.

- **PowerPoint:**          for the final competition submission, combining narrative, visuals, and embedded video.

- **GitHub repositories:** for modular, reproducible code (Data, EDA Tool, Model).

---------------------------
### 🎯 Rationale for Tools

- Databricks ensures scalability, reproducibility, and integration of both data engineering and modelling.

- Python offers rich libraries (Pandas, Scikit-learn, Statsmodels, Streamlit) for credit modelling and visualization.

- Streamlit makes EDA and dashboards interactive, which is essential for business users.

- draw.io provides clarity in communicating architecture and workflow.

- PowerPoint is required by competition rules and ensures findings are communicated in a professional, accessible format.

- GitHub repositories enforce modularity and reduce system-wide risk.

--------------------------
### 🔥 Why Databricks?

- Databricks supports the Medallion architecture (Bronze → Silver → Gold), integrates seamlessly with ML workflows, and allows handling of both data engineering and machine learning in one environment. It also supports reproducibility and collaboration, which are key competition requirements.

--------------------------
### 🐍 Why Python instead of R?
Python was chosen because:

- It integrates directly with Databricks and Streamlit.

--------------------------
### 📐 Why draw.io?
draw.io is:

- Free, lightweight, and easy to use.

- Ideal for creating data architecture diagrams like the Medallion pipeline.

- Helps communicate the mental map of the solution clearly.

--------------------------
### 📊 Why PowerPoint?
PowerPoint was chosen because:

- It is the required submission format for the competition.

- It allows embedding of video presentations and scripts.

- It provides a professional, visual medium to communicate findings to both technical and non-technical audiences.

--------------------------
### 🚧 Constraints

- Model constraint: Final predictive model must be logistic regression.

- Interpretability constraint: Every transformation must be explainable in plain language.

- EDA-driven modelling constraint: Modelling choices must be guided by EDA findings.

- Workflow constraint: Deliverables must include an interactive app, modelling summary report, reproducible workflow, PowerPoint presentationand AI usage reflection.

--------------------------
# 🔍 Detailed ML Workflow
### Phase 1 — Frame

- Collect data: Historical loan-book dataset (~120k rows × 26 columns).

- A bank wants to: Predict loan default within 12 months using logistic regression.

# key Questions to help understand the business problem better

- 1. **Business objectives:** What is the company’s ultimate goal — reducing default rates, increasing loan approvals, balancing risk vs profitability, or regulatory compliance?

**Answer:** To improve loan approval decisions by balancing risk and profitability. The objective is not just higher accuracy, but ensuring fewer defaults while still approving enough loans to grow the business. Regulatory compliance and transparency are equally critical.

- 2. **Decision context:** How are loan approval decisions currently made, and what pain points exist in the current process?

**Answer:** Currently, relies on traditional scorecards and manual rules for loan approvals. These methods can be rigid and may miss subtle risk patterns. The challenge is to modernize this process with a data-driven logistic regression model that still remains interpretable.

- 3. **Stakeholder needs:** What do risk managers, business stakeholders, and regulators specifically need to see in the model outputs to trust them?

**Answer:** 
        - Risk managers: need clear explanations of why a loan was approved or rejected.
        - Business stakeholders: want to see how approval thresholds affect profitability and customer growth.
        - Regulators: require transparency — every transformation and decision must be explainable in plain language.

- 4. **Interpretability requirements:** What level of explanation is required — plain-language descriptions of features, scorecard-style outputs, or visual dashboards?

**Answer:** The model must avoid “black box” methods. Expects scorecard-style outputs, WoE/IV explanations, and dashboards that show how features contribute to risk. This ensures decisions can be defended in audits.

- 5. **Success metrics:** How will success be measured — AUC improvement, Gini coefficient, business KPIs like reduced default volume, or regulator approval?

**Answer:** 
            - **Beat Baseline AUC:** 0.68 (older model).
            - **Target AUC       :** >0.75 through feature engineering.
            - **Ceiling benchmark:** LightGBM AUC of 0.82 (not allowed as final model, but used for comparison).
            - **Business KPIs    :** reduced default volume, improved profitability, and regulator approval.

- 6. **Business impact:** How do different approval thresholds affect profitability and risk? What trade-offs are most important to highlight in the dashboard?

**Answer:** The **Business Value Dashboard** will show how different approval thresholds affect:
             - **Loan volumes** (how many customers approved).
             - **Portfolio risk** (default rates).
             - **Profitability trade-offs** (higher volume vs higher risk).
             - This helps bank's executives make **policy-level decisions.**

- 7. **Monitoring expectations:** How often should the model be retrained or monitored for drift, and who is responsible for ongoing oversight?

**Answer:** This bank expects the model to be monitored for drift. Customer behavior changes over time (e.g. economic downturns, new credit policies). The model must be retrained periodically and audited for fairness and compliance.

- 8. **Constraints:** Beyond logistic regression, are there restrictions on data usage, feature types (e.g., no post-outcome features), or regulatory disallowed variables?

**Answer:** 
            - Final model must be logistic regression.
            - No automated feature selection without explanation.
            - Features that regulators may disapprove of (e.g. race, religion, post-outcome variables) must be excluded.
            - EDA must guide modelling choices, not trial-and-error.

---------------------------
### Phase 2 — Prepare

- Clean data: Remove duplicates, fix missing values, correct errors, standardize formats.

- Explore data (EDA): Identify risk patterns, distributions, WoE/IV values, subgroup effects.

- Prepare data: Feature engineering (ratios, binning, WoE encoding).

- Split data: 70/30 training/testing split to ensure generalization.

---------------------------
### Phase 3 — Model

- Choose algorithm: Logistic regression (classification).

- Train model: Fit logistic regression on training data, adjusting coefficients iteratively.

- Evaluate model: Metrics include Accuracy, Precision, Recall, F1, AUC, Gini.

- Improve model: Iterative feature engineering, WoE refinements, binning strategies.

------------------------------
### Phase 4 — Operate

- Deploy model: Streamlit app with EDA, evaluation, and business dashboard.

- Monitor model: Track drift, retrain periodically, ensure regulatory compliance.

------------------------------
### ✅ Results and findings 
Insights:

- **Baseline logistic regression AUC:** 0.68.

- **Improved logistic regression AUC:** Target >0.75 through feature engineering.

- **Business dashboard insights:** Approval thresholds directly affect risk vs profitability trade-offs.

- **Interpretability maintained:** Every transformation explained in plain language.

- **Deliverables ready:** Interactive app, modelling summary, reproducible workflow, PowerPoint with embedded video and script.
