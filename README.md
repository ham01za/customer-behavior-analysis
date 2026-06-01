# 🛒 Customer Behavior Analysis — Online Retail II

> **Data Mining project** | K-Means Segmentation · FP-Growth Association Rules · RFM Features

---

## 📌 Overview

This project applies unsupervised machine learning techniques to the **Online Retail II** dataset to understand customer behavior, segment clients into actionable profiles, and extract product association rules.

The analysis is structured in **5 parts**:

1. Data exploration & cleaning
2. Behavioral feature engineering (RFM + basket indicators)
3. Unsupervised customer segmentation (K-Means)
4. Association rule mining (FP-Growth)
5. Segment-level comparison & business recommendations



## 📊 Dataset

**Online Retail II** — UCI Machine Learning Repository  
Transactions from a UK-based e-commerce retailer (2009–2011).

| Field        | Description                          |
|-------------|--------------------------------------|
| Invoice      | Invoice number                       |
| StockCode    | Product code                         |
| Description  | Product name                         |
| Quantity     | Quantity ordered                     |
| InvoiceDate  | Date of transaction                  |
| Price        | Unit price (GBP)                     |
| Customer ID  | Unique customer identifier           |
| Country      | Country of the customer              |

📥 Download: [Kaggle — Online Retail II](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci)




## 🔍 Methodology

### Part 1 — Data Cleaning

- Removed rows with null `Customer ID`
- Dropped duplicates
- Filtered out negative quantities and prices (returns / cancellations)

**Result:** ~397K clean transactions retained from 1,067,371 original rows.

---

### Part 2 — Feature Engineering

Built 5 behavioral indicators per customer:

| Feature           | Description                                         |
|-------------------|-----------------------------------------------------|
| `Recence`         | Days since last purchase                            |
| `Frequence`       | Number of unique invoices                           |
| `Depense`         | Total spending                                      |
| `TailleMoyPanier` | Average number of items per order                   |
| `DiversiteProduits` | Number of distinct products purchased             |

---

### Part 3 — Customer Segmentation (K-Means)

- Normalized features with **MinMaxScaler**
- Tested k = 2, 3, 4 using Silhouette, Davies-Bouldin, and Calinski-Harabasz metrics
- **k = 4 retained** for business interpretability

| Segment | Profile                          |
|---------|----------------------------------|
| 0       | Occasional customers             |
| 1       | Loyal high-spenders              |
| 2       | Lost customers                   |
| 3       | New customers                    |

Visualized with **PCA 2D** projection.

---

### Part 4 — Association Rules (FP-Growth)

- Focused on **United Kingdom** transactions
- Built a binary basket matrix (invoice × product)
- Extracted frequent itemsets with `min_support = 0.02`
- Filtered rules: `support > 0.02`, `confidence > 0.5`, `lift > 2`

---

### Part 5 — Segment-Level Comparison

- Applied FP-Growth per customer segment
- Compared rule counts: global vs. per-segment
- Used **RandomForest feature importances** to identify key segmentation drivers

---

## 💡 Key Business Recommendations

1. **Retain loyal high-spenders** — VIP loyalty program (exclusive discounts, early access)
2. **Reactivate lost customers** — Time-limited reactivation campaigns before 6 months of inactivity
3. **Upgrade occasional customers** — Personalized promotions and automated reminders
4. **Onboard new customers** — Welcome emails, first-purchase offers, personalized recommendations
5. **Segment-based cross-selling** — Use FP-Growth rules per profile for targeted product suggestions

---

## 🛠️ Technologies

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-data--wrangling-lightgrey?logo=pandas)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?logo=scikit-learn)
![mlxtend](https://img.shields.io/badge/mlxtend-FP--Growth-green)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)



## 📄 License

This project is for academic purposes. The dataset is publicly available via the UCI ML Repository.
