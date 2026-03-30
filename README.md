# HCL-HACKATHON-TEAM-DELTA-UNIT
# Retail Sales Analytics Pipeline 🛒 Data Engineering Project

## 📌 Project Overview
This project demonstrates an end-to-end ETL/ELT pipeline designed to transform raw, multi-source retail data into actionable business intelligence. Using Informatica Intelligent Cloud Services (IICS) and Oracle PL/SQL, the pipeline cleanses "dirty" source data and implements a Star Schema to enable high-performance retail reporting.

## 🏗️ Architecture: The Medallion Approach
The data flows through three distinct logical layers to ensure data quality and historical accuracy:

- **Bronze (Staging):** Raw ingestion of Orders, products, customers from CSV.
- **Silver (Cleansing):** Data validation, Null handling, data cleaning and MD5 Checksum generation for Change Data Capture (CDC).
- **Gold (Analytics/DWH):** Dimensional modeling featuring SCD Type 2 for Customers and an optimized Fact_Orders table.

## 🛠️ Tech Stack
- **ETL Tool:** Informatica Intelligent Cloud Services (IICS)
- **Database:** Oracle 21c (PL/SQL)
- **Modeling:** Star Schema (Kimball Methodology)
- **Visualization:** Power BI
- **Version Control:** Git / GitHub

## 🧬 Data Transformations & Logic

### 1. Data Quality Validations
To ensure the "Gold" layer remains a "Single Source of Truth," the following IICS transformations were applied:

- **Standardization:** Date formats unified using TO_DATE and REPLACESTR.
- **Integrity Checks:** Filters applied to remove negative Unit_Price and Quantity.
- **Deduplication:** Sorter (Distinct) utilized to remove source-level duplicates.

### 2. Dimensional Modeling
- **SCD Type 2:** Implemented on dim_customers using Dynamic Lookup Cache and Update Strategy to track historical changes (e.g., Customer moves to a new City).
- **SCD Type 1:** Implemented on dim_products using the Lookup and update strategy (e.g., Product name or category changes).
- **Surrogate Keys:** Generated to decouple the warehouse from source system business keys.

### 3. Change Data Capture (CDC)
- **MD5 Hashing:** Used to create a unique "data fingerprint" for each record. This ensures we only perform updates in the target when a meaningful attribute has changed, significantly optimizing performance.

## 📊 Key Performance Indicators (KPIs)

| KPI | Logic |
| :--- | :--- |
| Total Revenue | Sum(Quantity * Unit_Price - Discount) |
| Customer Lifetime Value | Aggregated revenue per unique customer across history. |
| Top 5 Products | Ranked sales volume using IICS Rank Transformation. |
| Repeat Customer Rate | Count of customers with Order_Count > 1. |
