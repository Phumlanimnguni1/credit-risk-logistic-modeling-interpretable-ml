# 🏦 DataQuest2026 Project — Interpretable Credit Modelling

## 🧩 Problem Statement

The challenge is to improve how a retail lending company evaluates loan applications. Using a historical loan-book dataset, the goal is to predict whether an applicant will default within 12 months. The solution must be **interpretable**, specifically logistic regression, so that risk managers, business stakeholders, and regulators can trust and understand the decisions.

-----------------------------
# 🔍 Detailed ML Workflow
### Phase 1 — Frame

- Collect data: Historical loan-book dataset (~120k rows × 26 columns).

- A bank wants to: Predict loan default within 12 months using logistic regression.

# key Questions to help understand the business problem better

- 1. **How can we make better loan approval decisions?** 

Answer: We can improve lending decisions by investigating the historical data of past applicants to uncover hidden risk patterns and subgroup effects. By translating these exploratory insights into engineered features, we can build a highly interpretable logistic regression model that accurately predicts whether a consumer will default within 12 months of taking a loan.

- 2. **How do we balance loan volume against portfolio risk?**

Answer: This can be answered by building an interactive business value dashboard that allows stakeholders to explore lending workflows and policy-level trade-offs. By adjusting decision thresholds, we can see exactly how many customers are approved and monitor how the overall risk of the portfolio changes as loan volume increases.

- 3. **What is the business cost of our prediction errors?**

Answer: We must evaluate our machine learning metrics—specifically precision and recall—in real-world financial terms to determine which mistakes are more expensive to the lender, We need to define what precision means in the context of approved loans and what recall means in terms of missed opportunities to decide whether rejecting a good customer or approving a bad loan is more costly.

- 4. **How do we maintain transparency and regulatory compliance?**

Answer: We ensure compliance by strictly avoiding non-linear "black box" machine learning models (such as Random Forests or Neural Networks) and relying solely on a logistic regression model that can be clearly explained to regulators, business stakeholders, and risk managers. Additionally, we must research and identify specific features in our dataset that a regulator might disapprove of, ensuring we do not use variables that could lead to unfair lending practices.

---------------------------
### Phase 2 — Prepare

- Clean data        : Remove duplicates, fix missing values, correct errors, standardize formats.

- Explore data (EDA): Identify risk patterns, distributions, WoE/IV values, subgroup effects.

- Split data        : 70/30 training/testing split to ensure generalization.

- Prepare data      : Feature engineering (ratios, binning, WoE encoding)

                    - ❌ Age (age discrimination - ECOA violation)
                    - ❌ Region (potential proxy for race/national origin redlining concerns)
                    - ❌ Email domain type (could proxy for demographics)
                    - ❌ Branch code (geographic discrimination)
                                  
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
------------------------------
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

- **vscode**               code editor

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
### ✅ Results and findings 
Insights:

- **Baseline logistic regression AUC:** 0.68.

- **Improved logistic regression AUC:** Target >0.75 through feature engineering.

- **Business dashboard insights:** Approval thresholds directly affect risk vs profitability trade-offs.

- **Interpretability maintained:** Every transformation explained in plain language.

- **Deliverables ready:** Interactive app, modelling summary, reproducible workflow, PowerPoint with embedded video and script.
