# DataQuest2026 - Interpretable Credit Modelling on Databricks

## Overview
This project is part of **DataQuest2026**, focusing on building interpretable credit risk models for a retail lending company.  
The objective is to design a structured workflow that supports **Exploratory Data Analysis (EDA)**, **feature engineering**, and **logistic regression modelling** to predict loan defaults.

The dataset contains **120 960 simulated loan applications**, including applicant demographics, financial attributes, and default outcomes.  
The emphasis is on **interpretability** — models must be explainable to risk managers, business stakeholders, and regulators.

Key themes:
- Structured data exploration
- Interpretable machine learning
- Feature engineering
- Business decision support
- Using AI as a productivity companion

----------------------------------------------------------------------------------------------------
## Architecture

<img width="1252" height="697" alt="data_architecture" src="https://github.com/user-attachments/assets/c8890ac6-978c-47c1-9ed4-101082706b55" />

### Medallion Layers (Databricks Delta Tables)

1. **Bronze Layer**
   - Raw ingestion of CSV loan-book data.
   - Stored as Delta table with no transformations.
   - Landing zone for operational data.

2. **Silver Layer**
   - Cleans and standardizes data.
   - Transformations: data cleansing.
   - Used for EDA and feature engineering.

3. **Gold Layer**
   - Business-ready tables/views for modelling.
   - Integrations, aggregations, and business logic.
   - Supports model input preparation and dashboard metrics.

4. **Consume Layer**
   - Focused on **Machine Learning** (logistic regression).
   - BI & SQL reporting excluded for this project.

----------------------------------------------------------------------------------------------------
## ETL & Modelling Workflow

All data preparation and modelling are automated using **Databricks notebooks** with Delta Lake.

Execution flow:
- **Data Ingestion:** Load raw CSV into Bronze Delta tables.
- **Data Cleaning:** Apply transformations in Silver layer.
- **Feature Engineering:** Generate WoE, IV, and domain-informed features in Gold layer.
- **Model Training:** Fit logistic regression model with interpretable coefficients.
- **Evaluation:** Compare performance against baseline (AUC 0.68) and LightGBM benchmark (AUC 0.82 ceiling).
- **Dashboard:** Streamlit app embedded in Databricks for business decision simulation.

----------------------------------------------------------------------------------------------------
## Business Decision Dashboard

The dashboard is an **interactive app component** (built in Streamlit) that helps business users understand:
- **Approval strategy:** How thresholds affect approvals.
- **Volume vs Risk trade-off:** How portfolio risk changes with approval volume.
- **Precision vs Recall interpretation:** Business meaning of errors (false approvals vs missed opportunities).

----------------------------------------------------------------------------------------------------
## Security & Roles

### DataEngineer
- Full access to all layers.
- Responsible for ingestion and transformation scripts.

### DataScientist
- Read/write access to Silver and Gold layers.
- Builds models and dashboards.

### BusinessAnalyst
- Read-only access to Gold layer and dashboard outputs.

----------------------------------------------------------------------------------------------------
## Deliverables

- Databricks Notebooks (EDA, ETL, Modelling)
- Delta Tables (Bronze, Silver, Gold)
- Logistic Regression Model Summary
- Streamlit Business Decision Dashboard
- Modelling Report & AI Usage Reflection
