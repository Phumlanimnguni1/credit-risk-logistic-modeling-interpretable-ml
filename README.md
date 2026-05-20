# DataQuest2026 - Interpretable Credit Modelling on Databricks

*Note: This repository contains the Data Engineering (ETL) and Machine Learning pipelines for the FNB DataQuest 2026 project. The interactive Streamlit applications (EDA Tool & Business Value Dashboard) are hosted in a separate sister repository: https://github.com/Phumlanimnguni1/EDA-Tool-Design

## Overview
This project is part of **DataQuest2026**, focusing on building interpretable credit risk models for a retail lending company.  
The objective is to design a structured workflow that supports **Exploratory Data Analysis (EDA)**, **feature engineering**, and **logistic regression modelling** to predict loan defaults within 12 months.

The dataset contains **120 960 simulated loan applications**, including applicant demographics, financial attributes, and default outcomes.  
The strict business constraint is **interpretability** — complex black-box models (like Random Forest or LightGBM) are prohibited. The final model must be a transparent Logistic Regression model explainable to risk managers, business stakeholders, and regulators.

Key themes:
- Structured data exploration and data quality validation
- Interpretable machine learning & Weight of Evidence (WoE) encoding
- Targeted feature engineering derived from visual EDA
- Regulatory compliance and fair lending practices
- Using Generative AI as a paired analytical companion

----------------------------------------------------------------------------------------------------
## Architecture

<img width="891" height="743" alt="data_architecture" src="https://github.com/user-attachments/assets/684adc75-3ca0-4be8-af75-073e94074dfc" />


### Medallion Layers (Databricks Delta Tables)

1. **Bronze Layer (`loan_book_dirty`)**
   - Raw ingestion of the CSV loan-book data.
   - Stored as a Delta table with no transformations to serve as a landing zone for operational data.

2. **Silver Layer (`loan_book_silver`)**
   - Cleans and standardises the data.
   - **Transformations:** Handled missing values, removed duplicate rows, corrected data types, and standardised messy text columns (e.g. `loan_purpose`, `home_ownership`).

3. **Gold Layer (`loan_book_gold_v3`)**
   - Business-ready tables optimised specifically for logistic regression modelling.
   - **Regulatory Compliance:** Explicitly dropped prohibited features (`age`, `region`, and `branch_code_id`) to prevent ageism and geographic redlining (proxy discrimination).
   - **Targeted Feature Engineering:** Engineered 4 new mathematically combined features based on bivariate EDA heatmaps to capture non-linear subgroup risks.

4. **Consume Layer**
   - Focused entirely on **Machine Learning** (logistic regression).
   - BI & SQL reporting are excluded for this specific modelling project.

credit-risk-logistic-modeling/
├── README.md
├── data/
│   ├── production/
│   │   └── loan_book_gold_v3.csv
│   ├── raw/
│   │   └── loan_book.csv
│   └── staging/
│       └── loan_book_silver.csv
├── dataProcessing/
│   ├── bronze_to_silver_transformation.ipynb
│   ├── build_logistic_model.ipynb
│   └── silver_to_gold_transformation.ipynb
├── projectPlanning/
│   └── documenting_thinking_process.md
├── ProjectPresentation/
│   └── modelling_summary_report.text
└── reference/
    ├── projectBrief/
    ├── promptEngineering/
    └── research/
        └── data_description.text
----------------------------------------------------------------------------------------------------
## ETL & Modelling Workflow

All data preparation and modelling are automated using **Databricks notebooks** with Delta Lake.

Execution flow:
1. **Data Ingestion:** Load raw CSV into Bronze Delta tables.
2. **Data Cleaning:** Apply transformations in the Silver layer (deduplication, standardisation).
3. **Feature Engineering:** Calculate and append targeted interaction ratios:
   - *Debt Servicing Stress Index* (`interest_rate` * `dti_ratio`)
   - *Loan-to-Income Ratio* (`loan_amount` / `annual_income`)
   - *Delinquency Concentration* (`num_delinquencies_2yr` / `months_since_oldest_account`)
   - *High Earner / Low Stability Flag* (Binary flag for high income but short employment)
     
4. **Data Transformation:** Apply strict **Weight of Evidence (WoE)** encoding fitted *only* on the 70% training split to prevent data leakage, replacing raw values with log-odds scores. Standard scaling was explicitly avoided to preserve regulatory interpretability.
5. **Model Training:** Fit a Logistic Regression scorecard model.
   
----------------------------------------------------------------------------------------------------
## Model Performance & Results

The business challenge was to push a simple linear model past an older baseline using domain-informed feature engineering.

*   **Baseline Logistic Regression AUC:** 0.6800
*   **LightGBM Ceiling (Benchmark):** 0.8200
*   **Our Final Model AUC:** **0.7799**
*   **Gini Coefficient:** **0.5598** 

By engineering features to penalise specific high-risk subgroups, we successfully pushed a fully interpretable logistic regression model significantly above the baseline, satisfying both predictive power and regulatory transparency constraints.

----------------------------------------------------------------------------------------------------
## Sister Repository: Business Decision & EDA Dashboards

To view the interactive UI components of this project, please visit the **https://github.com/Phumlanimnguni1/EDA-Tool-Design**.
It contains:
- **Interactive EDA Tool:** A Streamlit application built to automatically calculate Information Value (IV) and uncover hidden risks using Bivariate density heatmaps.
- **Business Value Dashboard:** A dynamic decision-support tool that allows risk managers to adjust probability thresholds, visualising the trade-off between loan approval volume and expected portfolio risk, while translating ML metrics (Precision/Recall) into business dollar impact.

----------------------------------------------------------------------------------------------------
## Security & Roles

### DataEngineer
- Full access to all layers.
- Responsible for ingestion and transformation scripts in Databricks.

### DataScientist
- Read/write access to Silver and Gold layers.
- Fits the WoE encoding, trains the logistic regression model, and builds the dashboards.

### BusinessAnalyst / Risk Manager
- Read-only access to the Gold layer and the Streamlit dashboard outputs for policy adjustment.

----------------------------------------------------------------------------------------------------
## Deliverables Summary
- ✅ Databricks ETL & Modelling Notebooks (This Repo)
- ✅ Streamlit EDA Application (Sister Repo)
- ✅ Streamlit Business Decision Dashboard (Sister Repo)
