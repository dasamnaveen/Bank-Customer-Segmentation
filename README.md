# Retail Banking Risk & Profitability Analytics

![Power BI](https://img.shields.io/badge/PowerBI-F2C811?style=for-the-badge&logo=Power%20BI&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data%20Analysis%20Expressions-blue?style=for-the-badge)

## Project Overview
Despite processing massive volumes of daily transactions, retail banks often lack clear visibility into customer behavior, churn, and financial exposure. This project transforms raw, unstructured transaction data into a dynamic analytical engine. 

The primary objective of this enterprise-grade Business Intelligence solution is to empower executive leadership with a 360-degree view of the customer lifecycle. By engineering advanced DAX metrics, this dashboard identifies high-value customer segments, tracks transaction velocity, and automatically flags high-risk accounts to mitigate financial exposure.

## Live Dashboard


## Dashboard Architecture & Key Features
The dashboard is built on a clean, professional "World Bank" light-blue corporate theme and is divided into four strategic pillars:

### 1. Demographic Intelligence (Page 1)
- **Objective:** Map the customer base.
- **Features:** Total transaction volume and customer counts split by gender, geographic location, and sorted age groups (18-24, 25-34, etc.).

### 2. Transaction Behavior Insights (Page 2)
- **Objective:** Identify capital flow and operational bottlenecks.
- **Features:** Time-series analysis of transaction volumes, horizontal tile slicers for filtering, and an interactive heatmap revealing the busiest days and times of day.

### 3. Customer Segmentation & RFM (Page 3)
- **Objective:** Categorize customers to prevent churn.
- **Features:** A custom-engineered **Recency, Frequency, and Monetary (RFM) model**. It segments customers into *Loyal*, *New*, and *Lost* tiers, visualized in an Executive Matrix showing average revenue and transaction frequency per segment.

### 4. Profitability & Risk Matrix (Page 4)
- **Objective:** Isolate high-risk accounts holding the bank's capital.
- **Features:** A dynamically generated "Simulated Credit Score" driving a Risk/Reward Scatter Plot. Includes a filtered "Threat List" highlighting the Top 10 High-Risk customers with the highest transaction volumes.

## Advanced DAX & Feature Engineering
To solve the business problem, several missing metrics had to be engineered directly within Power BI using DAX:

**1. Simulated Risk Scoring:**
Because the raw data lacked external credit scores, an internal algorithm was developed to simulate risk based on transaction behavior (penalizing high recency and rewarding high frequency).
```dax
Simulated Credit Score = 
VAR BaseScore = 600
VAR FrequencyBonus = 'Customer_Segments'[Frequency] * 15
VAR RecencyPenalty = 'Customer_Segments'[Recency (Days)] * 0.5
VAR CalculatedScore = BaseScore + FrequencyBonus - RecencyPenalty
RETURN MIN(850, MAX(300, ROUND(CalculatedScore, 0)))
```
2. Dynamic Risk Categorization:

Code snippet
```
Risk Level = 
SWITCH(
    TRUE(),
    'Customer_Segments'[Simulated Credit Score] >= 720, "Low Risk",
    'Customer_Segments'[Simulated Credit Score] >= 630, "Medium Risk",
    "High Risk"
)
```

Dataset Information
Source File: raw_bank_transactions.csv

Rows: 1,000,000+ transaction records

Key Columns: TransactionID, CustomerID, CustomerDOB, CustGender, CustLocation, CustAccountBalance, TransactionDate, TransactionTime, TransactionAmount (INR)

💻 Tech Stack
Data Visualization & Modeling: Microsoft Power BI

Data Manipulation: Power Query, DAX

Design/UI: Custom corporate high-contrast palette
