# Supply Chain Management Analytics | End-to-End Data Analytics Project

## 📌 Project Overview

This project presents an end-to-end Supply Chain Analytics solution built using **Python** to analyze a real-world global supply chain dataset containing **180,000+ orders**.

The objective is to uncover operational inefficiencies, identify factors responsible for delivery delays, analyze profitability across different business dimensions, and develop a predictive model to identify orders at risk of late delivery.

The project follows a complete analytics workflow including:

- Business Understanding
- Data Cleaning & Preprocessing
- Feature Engineering
- Exploratory Data Analysis (EDA)
- KPI Development
- Business Insights & Recommendations
- Machine Learning Modeling

---

## 🎯 Business Problem

The company operates a global e-commerce supply chain where delayed deliveries negatively impact customer satisfaction, operational efficiency, and profitability.

The objective is to answer key business questions such as:

- Which regions experience the highest delivery delays?
- Which shipping modes perform poorly?
- Which customer segments contribute the highest revenue?
- How do delivery delays affect profitability?
- Can we predict late deliveries before shipment?

---

## 📂 Dataset

**Source:** [DataCo Global Supply Chain Dataset](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)

### Dataset Summary

- **180,519 Orders**
- **50+ Features**
- Global Supply Chain Operations
- Customer Information
- Product Information
- Shipping Details
- Revenue & Profit Metrics
- Delivery Status

---

## 🛠️ Tech Stack

### Programming

- Python

### Libraries

- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Imbalanced-learn (SMOTE)

### Development Environment

- Jupyter Notebook

---

# 🔄 Project Workflow

```
Business Understanding
        │
        ▼
Data Cleaning
        │
        ▼
Feature Engineering
        │
        ▼
Exploratory Data Analysis
        │
        ▼
Business KPI Development
        │
        ▼
Business Insights
        │
        ▼
Machine Learning Modeling
        │
        ▼
Business Recommendations
```

---

# 🧹 Data Cleaning

Performed multiple preprocessing steps including:

- Removed duplicate records
- Handled missing values
- Removed irrelevant columns
- Removed high-cardinality identifier columns
- Converted date columns to datetime format
- Removed cancelled orders
- Standardized column formats

---

# ⚙️ Feature Engineering

Created new business-driven analytical features:

- Delay (Actual - Scheduled Delivery)
- Order Processing Time
- Late Delivery Flag
- Month
- Day
- Hour
- Delivery Performance Indicators
- Frequency Encoding for categorical variables

---

# 📊 Exploratory Data Analysis

Performed detailed analysis on:

- Delivery Delay Distribution
- Revenue Trends
- Profitability Analysis
- Shipping Mode Performance
- Customer Segment Analysis
- Department-wise Performance
- Regional Performance
- Monthly Delay Trends
- Root Cause Analysis
- Operational Bottlenecks

---

# 📈 Key Performance Indicators (KPIs)

## Delivery Metrics

- Total Orders
- Late Deliveries
- On-Time Delivery Rate
- Late Delivery Rate
- Average Delay
- 90th Percentile Delay
- SLA Compliance

## Financial Metrics

- Total Revenue
- Total Profit
- Profit Margin
- Average Order Value
- Profit Loss due to Delays

## Operational Metrics

- Shipping Mode Performance
- Department Efficiency
- Customer Segment Performance
- Regional Delivery Performance

---

# 🤖 Machine Learning

### Objective

Predict whether an order is likely to experience a late delivery before shipment.

### Target Variable

- **Late_delivery_risk**

### Model Used

- Random Forest Classifier

### Data Preparation

- Frequency Encoding
- Train-Test Split (80:20)
- SMOTE for class balancing

---

# 📊 Model Performance

| Metric | Score |
|---------|------:|
| Accuracy | **74%** |
| Precision | **85%** |
| Recall | **65%** |
| F1 Score | **74%** |
| ROC-AUC | **0.82** |

The model demonstrates strong discriminative ability to distinguish between delayed and on-time deliveries and can serve as a decision-support tool for proactive logistics planning.

---

# 📌 Feature Importance

The Random Forest model identified the most influential factors contributing to late deliveries, enabling better operational decision-making and proactive shipment monitoring.

---

# 💡 Key Business Insights

- Identified regions with consistently high delivery delays.
- Evaluated shipping modes contributing most to delayed deliveries.
- Quantified the financial impact of delivery delays on profitability.
- Identified high-performing product categories and departments.
- Analyzed customer segments generating maximum revenue.
- Discovered operational bottlenecks affecting order fulfillment.
- Built a predictive model capable of identifying high-risk shipments before dispatch.

---

# 🚀 Business Recommendations

- Prioritize orders with high predicted delivery risk.
- Improve logistics planning for high-delay regions.
- Optimize underperforming shipping modes.
- Monitor delivery KPIs continuously.
- Allocate additional operational resources during peak delay periods.
- Use predictive analytics to proactively reduce SLA violations.

---

# 📁 Repository Structure

```
Supply-Chain-Analytics/

│── main.ipynb
│── README.md

---

# 🎯 Future Improvements

- Hyperparameter tuning using GridSearchCV / RandomizedSearchCV
- XGBoost and LightGBM model comparison
- Interactive Power BI dashboard
- Real-time prediction pipeline using Streamlit or Flask

