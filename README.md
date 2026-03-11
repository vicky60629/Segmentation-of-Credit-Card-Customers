# 💳 Segmentation of Credit Card Customers

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![Unsupervised ML](https://img.shields.io/badge/ML-Clustering%20%7C%20Factor%20Analysis%20%7C%20PCA-orange?style=flat-square)
![Domain](https://img.shields.io/badge/Domain-Banking%20%7C%20Marketing%20Analytics-lightblue?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-9000%20Customers%20%7C%2018%20Variables-green?style=flat-square)
![Stars](https://img.shields.io/github/stars/vicky60629/Segmentation-of-Credit-Card-Customers?style=flat-square)

> **An unsupervised machine learning project that segments ~9,000 active credit card holders into distinct behavioural clusters — enabling banks to design targeted marketing strategies and personalised financial products.**

---

## 📌 Problem Statement

A bank's marketing team needs to understand **who their credit card customers really are** — not just as account holders, but as distinct behavioural groups with different spending habits, payment patterns, and financial needs.

With **9,000 active customers and 18 behavioural variables**, this project applies unsupervised ML techniques to:

1. **Engineer intelligent KPIs** from raw transactional data
2. **Reduce dimensionality** using Factor Analysis to remove multicollinearity
3. **Cluster customers** into meaningful behavioural segments
4. **Profile each segment** with detailed characteristics
5. **Recommend targeted marketing strategies** for each cluster

---

## 🎯 Business Impact

| Stakeholder | Value Delivered |
|-------------|----------------|
| **Marketing Team** | Run personalised campaigns tailored to each customer segment |
| **Product Team** | Design credit products (cashback, travel, premium) for specific segments |
| **Risk Team** | Identify high-risk segments (heavy cash advance users, minimum payment payers) |
| **Operations** | Prioritise service improvements for high-value but low-satisfaction segments |
| **Executive Leadership** | Data-driven strategic insights on customer base composition |

> According to Bain & Company, companies with excellent customer segmentation strategies see up to **10% profit increase** over a 5-year period compared to those without.

---

## 📊 Dataset

- **Source:** [Kaggle — Credit Card Dataset for Clustering](https://www.kaggle.com/datasets/arjunbhasin2013/ccdata)
- **File:** `CC_GENERAL.csv`
- **Size:** ~9,000 active credit card holders
- **Period:** Last 6 months of behavioural data
- **Granularity:** Customer level with 18 behavioural variables

### Data Dictionary

| Variable | Description |
|----------|-------------|
| `CUST_ID` | Unique credit card holder ID |
| `BALANCE` | Monthly average balance (based on daily averages) |
| `BALANCE_FREQUENCY` | Ratio of last 12 months with a balance (0–1) |
| `PURCHASES` | Total purchase amount in last 12 months |
| `ONEOFF_PURCHASES` | Total one-off (single) purchase amount |
| `INSTALLMENTS_PURCHASES` | Total instalment purchase amount |
| `CASH_ADVANCE` | Total cash advance amount taken |
| `PURCHASES_FREQUENCY` | % of months with at least one purchase |
| `ONEOFF_PURCHASES_FREQUENCY` | Frequency of one-off purchases |
| `PURCHASES_INSTALLMENTS_FREQUENCY` | Frequency of instalment purchases |
| `CASH_ADVANCE_FREQUENCY` | Frequency of cash advances |
| `CASH_ADVANCE_TRX` | Average amount per cash advance transaction |
| `PURCHASES_TRX` | Average amount per purchase transaction |
| `CREDIT_LIMIT` | Customer's credit limit |
| `PAYMENTS` | Total payments made to reduce statement balance |
| `MINIMUM_PAYMENTS` | Total minimum payments made |
| `PRC_FULL_PAYMENT` | Percentage of months with full payment |
| `TENURE` | Number of months as a credit card customer |

---

## 🏗️ Project Architecture

```
Segmentation-of-Credit-Card-Customers/
├── CC_GENERAL.csv               # Raw customer behavioural dataset
├── Credit_new_cust.xlsx         # New customer profiles for segment assignment
├── Profiling_output.csv         # Cluster profiling results
├── python_FA.xls                # Factor Analysis output
├── pandas_profiling.html        # Auto-generated EDA report (open in browser)
├── Segmentation of Credit Card Customers.ipynb   # Full pipeline notebook
├── LICENSE
└── README.md
```

---

## 🔍 Full Analytical Pipeline

### Step 1 — Advanced Data Preparation & KPI Engineering

Raw transactional variables alone don't tell the full story. Intelligent KPIs are engineered to capture **customer behaviour ratios** that reveal true financial habits:

| Engineered KPI | Formula | Business Meaning |
|----------------|---------|-----------------|
| `monthly_avg_purchase` | `PURCHASES / TENURE` | Average monthly spending rate |
| `monthly_avg_cash_advance` | `CASH_ADVANCE / TENURE` | Monthly reliance on cash advances |
| `limit_usage_ratio` | `BALANCE / CREDIT_LIMIT` | How much of credit limit is used |
| `payments_to_min_ratio` | `PAYMENTS / MINIMUM_PAYMENTS` | Payment discipline (higher = better) |
| `purchase_type_ratio` | `ONEOFF / INSTALLMENTS` | Spending style — impulsive vs planned |
| `cash_advance_ratio` | `CASH_ADVANCE / PURCHASES` | Reliance on cash vs purchases |

### Step 2 — Exploratory Data Analysis (EDA)

- Generated full statistical profiling report using **pandas-profiling** (`pandas_profiling.html`)
- Analysed distributions of all 18 variables — most spending variables are **highly right-skewed**
- Identified significant **missing values** in `MINIMUM_PAYMENTS` and `CREDIT_LIMIT` — imputed using median
- Correlation analysis revealed **multicollinearity** between purchase frequency variables — motivating Factor Analysis

### Step 3 — Dimensionality Reduction: Factor Analysis

With 18 correlated variables, direct clustering leads to the **Curse of Dimensionality**. Factor Analysis groups correlated variables into **latent factors** that represent underlying behavioural dimensions:

```python
# Factor Analysis for variable reduction
from factor_analyzer import FactorAnalyzer
fa = FactorAnalyzer(n_factors=optimal_factors, rotation='varimax')
fa.fit(scaled_data)
factor_scores = fa.transform(scaled_data)
```

Output saved to `python_FA.xls` for detailed factor loading analysis.

**Identified Latent Factors (example):**
- **Factor 1 — Purchase Activity:** Groups purchase frequency, purchase amount, transaction count
- **Factor 2 — Cash Advance Behaviour:** Groups cash advance amount, frequency, transactions
- **Factor 3 — Payment Discipline:** Groups full payment %, payments to minimum ratio

### Step 4 — Clustering: K-Means Segmentation

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# Scale factor scores
scaler = StandardScaler()
scaled_factors = scaler.fit_transform(factor_scores)

# Optimal k using Elbow Method
inertias = []
for k in range(2, 11):
    km = KMeans(n_clusters=k, random_state=42)
    km.fit(scaled_factors)
    inertias.append(km.inertia_)
```

**Optimal number of clusters: 4** (determined via Elbow Method + Silhouette Score)

### Step 5 — Cluster Profiling & Strategic Insights

Each cluster is profiled on key variables to understand **who they are** and **what they need**:

| Cluster | Profile Name | Characteristics | Recommended Strategy |
|---------|-------------|-----------------|---------------------|
| **0** | 💤 Inactive / Low Engagers | Low balance, low purchases, low cash advance | Re-engagement campaigns, introductory cashback offers |
| **1** | 💰 High Spenders | High purchases, high credit limit, frequent transactions | Premium rewards, travel cards, loyalty programs |
| **2** | 🏧 Cash Advance Reliant | High cash advance, low purchases, high interest burden | Financial wellness programs, personal loan conversion |
| **3** | 📦 Instalment Shoppers | High instalment purchases, consistent payment behaviour | EMI offers, buy-now-pay-later products, retail partnerships |

> **Note:** Exact cluster labels depend on the final model output in the notebook.

---

## 📈 Key Findings

- **~30% of customers** rely heavily on cash advances — a high-risk, high-interest segment that the bank should either convert to personal loans or offer financial planning support
- **High spenders** (Cluster 1) have the highest credit limits but also the highest balance-to-limit ratios — prime candidates for premium card upgrades
- **Full payment behaviour** (`PRC_FULL_PAYMENT`) is the single strongest differentiator between financially healthy and at-risk customer segments
- **Instalment shoppers** show the most consistent, predictable behaviour — lowest churn risk and best candidates for cross-sell

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python 3.8+ |
| Data Processing | Pandas, NumPy |
| EDA | pandas-profiling |
| Visualisation | Matplotlib, Seaborn |
| Dimensionality Reduction | Factor Analyzer, PCA (Scikit-learn) |
| Clustering | Scikit-learn (K-Means) |
| Cluster Validation | Elbow Method, Silhouette Score |
| Output | Excel (openpyxl) for profiling reports |
| Notebook | Jupyter Notebook |

---

## 🚀 Running Locally

```bash
# Clone the repository
git clone https://github.com/vicky60629/Segmentation-of-Credit-Card-Customers.git
cd Segmentation-of-Credit-Card-Customers

# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook "Segmentation of Credit Card Customers.ipynb"

# View the EDA report
open pandas_profiling.html   # or double-click to open in browser
```

---

## 💡 Key Learnings & Future Improvements

**What worked well:**
- Factor Analysis before clustering significantly reduced noise and multicollinearity — clusters are more interpretable than raw K-Means on 18 variables
- Engineering KPI ratios (limit usage, payment discipline) revealed behavioural patterns invisible in raw variables
- Profiling output (`Profiling_output.csv`) makes cluster insights shareable with non-technical stakeholders

**Future enhancements:**
- [ ] Try **DBSCAN** or **Gaussian Mixture Models** for non-spherical cluster shapes
- [ ] Add **Hierarchical Clustering + Dendrogram** for alternative segmentation view
- [ ] Build interactive **Tableau / Plotly Dash** dashboard for cluster exploration
- [ ] Apply **RFM Analysis** (Recency, Frequency, Monetary) alongside behavioural clustering
- [ ] Extend to **real-time segment assignment** for new customers using `Credit_new_cust.xlsx` pipeline
- [ ] Add **SHAP / interpretability layer** to explain individual customer segment assignment
- [ ] Track experiments with **MLflow**

---

## 🧠 Why Unsupervised Learning Here?

Unlike supervised learning, there are **no predefined labels** for customer segments — we don't know upfront how many types of customers exist or what they look like. Unsupervised learning lets the **data speak for itself**, revealing natural groupings that a business analyst might never discover manually from 9,000 rows and 18 columns.

This is exactly the kind of analysis that drives real decisions at banks: product design, marketing spend allocation, and risk management — all informed by who customers actually are rather than assumptions.

---

## 👨‍💻 About the Author

**Vicky Gupta** — Data Engineering Analyst @ Accenture (4.5 years) | Aspiring Data Scientist

Passionate about unsupervised ML, customer analytics, and building data products that drive real business decisions. Experienced in PySpark, ETL pipelines, and end-to-end ML workflows.

🔗 [LinkedIn](https://www.linkedin.com/in/vicky-gupta-583016168/) | [GitHub](https://github.com/vicky60629)

📧 vg60629@gmail.com

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

⭐ **Found this useful? Star the repository — it helps others in the community discover it!**
