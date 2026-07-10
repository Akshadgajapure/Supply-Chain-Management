# Supply Chain Delivery Analytics | End-to-End Data Analytics Project

## 📌 Project Overview

This project presents an end-to-end supply chain analytics solution built in **Python**, analyzing a real-world global e-commerce supply chain dataset of **180,000+ raw orders (172,765 after cleaning)**.

The objective is to uncover operational inefficiencies, quantify the financial impact of delivery delays, identify root causes across regions and shipping modes, and build a validated predictive model to flag at-risk shipments before dispatch.

The project follows a complete analytics workflow:

- Business Understanding
- Data Cleaning & Preprocessing
- Feature Engineering
- Exploratory Data Analysis (EDA)
- KPI Development
- Root Cause & Bottleneck Analysis
- Time-Based Delay Analysis
- Machine Learning Modeling (Multi-Model Comparison with Cross-Validation)
- Business Recommendations

---

## 🎯 Business Problem

A global e-commerce company managing end-to-end order fulfillment faces inconsistent delivery performance — actual shipping time frequently deviates from scheduled timelines, driving late deliveries and unpredictable order profitability.

Key business questions addressed:

- Which regions, shipping modes, and customer segments experience the highest delivery delays?
- How much profit is actually being lost to late deliveries?
- What time-based patterns (month, day, hour) predict higher delay risk?
- Can we reliably predict which orders are at risk of late delivery *before* they ship?

---

## 📂 Dataset

**Source:** [DataCo Global Supply Chain Dataset](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)

### Dataset Summary

- 180,519 raw orders → **172,765 orders after cleaning** (cancelled shipments removed)
- 50+ original features
- Global supply chain operations across multiple regions
- Customer, product, shipping, and financial fields

---

## 🛠️ Tech Stack

**Language:** Python

**Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM, Imbalanced-learn (SMOTE)

**Environment:** Jupyter Notebook

---

## 🔄 Project Workflow

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
Root Cause & Time-Based Analysis
        │
        ▼
Multi-Model ML Comparison (5-Fold CV)
        │
        ▼
Business Recommendations
```

---

## 🧹 Data Cleaning

- Removed cancelled orders (`Delivery Status == 'Shipping canceled'`)
- Dropped 15+ irrelevant / high-cardinality / PII columns (customer email, password, name, zip code, coordinates, etc.)
- Converted order and shipping date columns to proper datetime format
- Verified no missing values or duplicate rows remained after cleaning

---

## ⚙️ Feature Engineering

- **Order Processing Time** — actual days between order and shipment
- **Delay** — actual processing time minus scheduled shipment days
- **Is_Delayed** — binary flag derived from `Delay`
- **Profitability Flag** — Profit / Loss / Break-even, derived from order-level profit
- **order_month, order_day, order_hour** — extracted for time-based trend analysis
- **Frequency Encoding** — applied to categorical fields (Type, Category, Segment, Department, Region, Shipping Mode) for modeling

---

## 📊 Exploratory Data Analysis

- Delivery delay distribution and profitability split (Profit / Loss / Break-even)
- Bottleneck detection: delay % by Region, Customer Segment, Shipping Mode, Order Status, Type, and Department
- Root cause analysis: top delay drivers *within* each region
- Time-based analysis: delay % trends by month, day of week, and hour of day

---

## 📈 Key Performance Indicators (KPIs)

| KPI | Value |
|---|---|
| Total Orders | 172,765 |
| Late Deliveries | 94,523 |
| On-Time Delivery Rate | 45.29% |
| Late Delivery Rate | 54.71% |
| 90th Percentile Delay | 3.0 days |
| Total Profit | $7.5M |
| **Total Profit Lost to Delays** | **$2.1M** |

The **$2.1M in profit lost to delayed orders** is the single most important business figure in this analysis — it reframes delivery delay from an operational annoyance into a quantified, board-level financial problem.

---

## 🤖 Machine Learning

### Objective
Predict whether an order is at risk of late delivery (`Late_delivery_risk`) using information known at order time — not derived from the actual (future) shipping date, avoiding target leakage.

### Data Preparation
- Frequency encoding for categorical features
- Train-test split (80:20)
- **SMOTE** applied to the training set to correct class imbalance

### Models Compared
Rather than relying on a single model, four classifiers were benchmarked head-to-head using **5-fold stratified cross-validation** on the balanced training set, then validated on a held-out test set:

- Logistic Regression (baseline)
- Random Forest
- XGBoost
- LightGBM

---

## 📊 Model Performance

**5-Fold Cross-Validation (mean, balanced training set):**

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.7134 | 0.7875 | 0.5845 | 0.6710 | 0.7098 |
| **Random Forest** | **0.7674** | **0.8513** | **0.6481** | **0.7359** | **0.8630** |
| XGBoost | 0.7587 | — | — | — | — |

**Hold-Out Test Set (final validation):**

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.6971 | 0.8329 | 0.5895 | 0.6904 | 0.7088 |
| **Random Forest** | **0.7356** | **0.8504** | **0.6534** | **0.7390** | **0.8222** |
| XGBoost | 0.7257 | 0.8794 | 0.6040 | — | — |

**Random Forest was the strongest and most consistent performer** across both cross-validation and hold-out evaluation, confirming it generalizes well rather than overfitting to a single split.

---

## 📌 Feature Importance

Top predictors of late delivery risk (Random Forest):

| Feature | Importance |
|---|---|
| Days for shipment (scheduled) | 0.2547 |
| Shipping Mode (frequency-encoded) | 0.2420 |
| Order hour | 0.1674 |
| Order Region (frequency-encoded) | 0.0862 |
| Order month | 0.0723 |
| Category Name (frequency-encoded) | 0.0717 |

Scheduled shipping window and shipping mode dominate the model's predictions — suggesting delay risk is largely set at the point of shipping-method selection, not driven by customer or product category.

---

## 💡 Key Business Insights

- Quantified **$2.1M in profit lost to late deliveries**, out of $7.5M total profit — delays are a material drag on margin, not a minor operational issue.
- Only 45.3% of orders arrive on time; the majority (54.7%) are late.
- Delay risk varies meaningfully by region, shipping mode, and time of day/month — enabling targeted intervention rather than blanket policy changes.
- A validated Random Forest model (ROC-AUC 0.82–0.86) can flag high-risk orders *before* shipment, enabling proactive logistics decisions rather than after-the-fact damage control.

---

## 🚀 Business Recommendations

- Prioritize proactive intervention (expedited handling, customer communication) for orders the model flags as high-risk.
- Investigate and renegotiate SLAs with underperforming shipping modes, which are the second-largest driver of delay risk.
- Target operational fixes at the specific regions and time windows (month/hour) with the highest delay concentration, rather than uniform process changes.
- Track the $2.1M delay-related profit loss as a standing KPI to measure the ROI of any operational changes.
- Integrate the predictive model into order processing to enable real-time risk flagging.

---

## 📁 Repository Structure

```
Supply-Chain-Management/
│── main.ipynb
│── README.md
```

---

## 🎯 Future Improvements

- Hyperparameter tuning via GridSearchCV / RandomizedSearchCV
- Replace frequency encoding with (leakage-safe, CV-aware) target encoding to test for improved signal
- Interactive Power BI / Tableau dashboard for the KPI and root-cause findings
- Real-time prediction pipeline via Streamlit or Flask
- Confirm SMOTE is applied within the cross-validation pipeline (not just once beforehand) to fully eliminate any resampling leakage risk
