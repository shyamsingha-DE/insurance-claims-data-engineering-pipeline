# iInsurance Claims Data Engineering Pipeline
📌 Project Overview

This project demonstrates an end-to-end Insurance Claims Data Engineering Pipeline built using PySpark, Delta Lake, and the Medallion Architecture.

The pipeline processes raw insurance claims data, performs data cleaning and validation, handles invalid records through dedicated quarantine datasets, and produces a clean, business-ready Gold layer for analytics.

The project focuses on practical ETL development, data quality, data validation, transformation, and exception handling using PySpark.

🏗️ Architecture

The pipeline follows the Medallion Architecture:

             Raw Insurance Claims Data
                       │
                       ▼
                ┌─────────────┐
                │   BRONZE    │
                │ Raw Dataset │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │   SILVER    │
                │ Clean + DQ  │
                │ Validation  │
                └──────┬──────┘
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
       Quarantine            Valid Data
       Records                   │
                                 ▼
                          ┌─────────────┐
                          │    GOLD     │
                          │ Analytics-  │
                          │ Ready Data  │
                          └─────────────┘
🛠️ Technologies Used
Python
PySpark
Delta Lake
Spark SQL
Databricks / Apache Spark
Pandas
📂 Dataset

The insurance claims dataset contains fields such as:

Claim_ID
Customer_ID
Claim_Type
Claim_Amount
Claim_Date
Claim_Status
Doctor_Name
Patient_ID

The source data intentionally contains inconsistent and invalid values to demonstrate real-world data-quality processing.

🥉 Bronze Layer

The Bronze layer stores the raw claims data with minimal transformation.

Key principles:

Preserve source data
Maintain original values
Avoid destructive transformations
Provide a reliable starting point for downstream processing
🥈 Silver Layer

The Silver layer performs data cleaning, standardization, and validation.

Data Quality Rules
Rule ID	Column	Validation
DQ001	Claim_ID	Validate Claim ID format
DQ002	Customer_ID	Validate Customer ID format
DQ003	Claim_Type	Validate and standardize claim type
DQ004	Claim_Amount	Clean and validate claim amount
DQ005	Claim_Date	Validate claim date
DQ006	Claim_Status	Validate claim status
DQ007	Patient_ID	Validate Patient ID

The pipeline creates validation flags such as:

valid_Claim_ID
valid_Customer_ID
valid_Claim_Type
valid_Claim_Amount
valid_Claim_Date
valid_Claim_Status
valid_Patient_ID

A consolidated:

validation_failed

flag identifies records containing one or more data-quality failures.

🚨 Quarantine Processing

Invalid values are separated into quarantine datasets instead of being silently discarded.

The quarantine structure contains:

Claim_ID
Column_Name
Invalid_Value
Rule_ID
Failure_Reason

This approach provides:

Data-quality traceability
Easier debugging
Auditability
Visibility into source-data problems
Controlled handling of invalid records
🥇 Gold Layer

The Gold layer contains cleaned and business-ready claims data.

It can be used for:

Business reporting
Claims analysis
Power BI dashboards
KPI reporting
Trend analysis
Further analytical workloads

Example analytical metrics include:

Total number of claims
Total claim amount
Claims by type
Claims by status
Claims by customer
Monthly claim trends
📁 Project Structure
insurance-claims-data-engineering-pipeline/
│
├── Insurance_Claims_Data_Engineering_Pipeline.ipynb
├── requirements.txt
└── README.md
▶️ How to Run
1. Clone the repository
git clone <repository-url>
cd insurance-claims-data-engineering-pipeline
2. Install dependencies
pip install -r requirements.txt
3. Open the notebook

Open:

Insurance_Claims_Data_Engineering_Pipeline.ipynb

Run the notebook sequentially from the Bronze layer through the Silver, Quarantine, and Gold processing stages.

The notebook can be executed in a compatible PySpark / Databricks / Spark environment.

🎯 Key Learning Outcomes

This project demonstrates practical experience with:

PySpark DataFrame transformations
Data cleaning and standardization
Data validation
Regular expressions
Conditional transformations
Type conversion and error handling
Data-quality flags
Quarantine processing
Medallion Architecture
Bronze → Silver → Gold pipelines
Delta Lake concepts
Analytics-ready data preparation
👨‍💻 Author

Shyam

QA Lead / Testing Professional transitioning into Data Engineering and Analytics, with experience in software testing, payments, API validation, SQL, and data quality.

Core Interests

PySpark · Databricks · SQL · Data Engineering · Data Quality · Power BI · Data Analytics
