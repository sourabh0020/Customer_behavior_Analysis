# Customer Shopping Behavior Analysis

End-to-end data analytics project analyzing 3,900 retail transactions across the full pipeline: **Python (data cleaning & feature engineering) → SQL Server (business analysis) → Power BI (dashboard)**.

## 📌 Project Overview

A retail dataset of 3,900 customer transactions across 18 attributes — demographics, product categories, purchase amounts, ratings, subscriptions, discounts, and shipping — was processed through a complete analytics pipeline to answer 10 real business questions and deliver a stakeholder-ready dashboard.

**Tech Stack:** Python (Pandas) · SQL Server (T-SQL) · Power BI

## 🗂️ Repository Structure
├── customer_shopping_behavior.csv # Raw dataset (3,900 rows × 18 columns)
├── Customer_Sales_Analysis.ipynb # Data cleaning + feature engineering (Python)
├── cleaned_customers.csv # Cleaned dataset exported for SQL
├── Customer_purchasing_behaviour.sql # 10 business-question SQL queries
├── dashboard_screenshot.png # Power BI dashboard
└── README.md
## 🧾 Dataset

3,900 rows × 18 columns, one row per customer transaction: `customer_id`, `age`, `gender`, `item_purchased`, `category`, `purchase_amount`, `location`, `size`, `color`, `season`, `review_rating`, `subscription_status`, `shipping_type`, `discount_applied`, `promo_code_used`, `previous_purchases`, `payment_method`, `frequency_of_purchases`.

Only `review_rating` had missing values (37 out of 3,900, ~0.95%) — all other columns were complete.

## 🧹 Data Cleaning

- **Category-aware imputation:** Missing review ratings were filled using the **median rating within each product category** (not a single global median), since rating behavior varies by category (e.g., Clothing rated on fit, Footwear on comfort).
- **Column standardization:** All column names converted to lowercase `snake_case` (e.g., `Purchase Amount (USD)` → `purchase_amount`) for SQL compatibility.

## ⚙️ Feature Engineering

| Feature | Description |
|---|---|
| `age_group` | Customers segmented into 4 equal-sized bins (Young Adult, Adult, Middle-aged, Senior) using quantile-based binning (`pd.qcut`) for fair comparisons |
| `purchase_frequency_days` | Categorical purchase frequency (e.g., "Weekly", "Monthly") mapped to a numeric estimate of days between purchases |
| `promo_code_used` (dropped) | Found to be 100% identical to `discount_applied` across all 3,900 rows — removed as redundant |

## 📊 Exploratory Data Analysis

| Metric | Age | Purchase Amount | Review Rating | Previous Purchases |
|---|---|---|---|---|
| Mean | 44.07 | $59.76 | 3.75 | 25.35 |
| Min | 18 | $20 | 2.5 | 1 |
| Max | 70 | $100 | 5.0 | 50 |

## 🗄️ SQL Business Analysis

10 T-SQL queries answered across four themes:

1. **Revenue Analysis** — total revenue by gender (Q1), subscribers vs. non-subscribers (Q5), revenue by age group (Q10)
2. **Customer Segmentation** — New/Returning/Loyal tiers via CTE + CASE logic (Q7); repeat buyers vs. subscription (Q9)
3. **Discount Behavior** — discount users spending above average (Q2); products most dependent on discounting (Q6)
4. **Product Performance** — top-rated products (Q3), shipping type vs. spend (Q4), top 3 products per category via window function (Q8)

See [`Customer_purchasing_behaviour.sql`](./Customer_purchasing_behaviour.sql) for full queries.

## 📈 Power BI Dashboard

![Dashboard](./dashboard_screenshot.png)

**KPIs:** 3.90K customers · ₹233.08K total revenue · $59.76 avg. purchase · 3.75 avg. rating

**Components:**
- Donut chart — subscription status (27% subscribers vs. 73% non-subscribers)
- Bar charts — revenue & sales by category and age group
- Slicers — Subscription Status, Gender, Category, Shipping Type

KPIs match the Python EDA output exactly, confirming consistency across the full pipeline.

## 💡 Key Insights

- **Clothing dominates** both revenue and sales volume — the primary business driver
- **Young Adults lead revenue** among age segments (quantile-based groups confirm this is real behavior, not sample-size bias)
- **Subscription gap:** only 27% of customers subscribe — a high-value minority worth targeting
- Full **pipeline integrity** validated end-to-end (Python → SQL → Power BI) with consistent metrics throughout

## 🎯 Recommendations

1. **Convert non-subscribers** — target high-frequency repeat buyers (5+ purchases) with trial offers or first-order discounts to drive recurring revenue
2. **Diversify beyond Clothing** — bundle Outerwear & Footwear with top Clothing items; run category-specific promos to reduce single-category dependency
3. **Focus & test age segments** — prioritize Young Adult & Middle-aged channels for near-term ROI, while running win-back tests for Adult/Senior segments to assess product-fit gaps

## 🔧 Tools & Skills Demonstrated

`Python` `Pandas` `SQL Server` `T-SQL` `CTEs` `Window Functions` `Power BI` `DAX` `Data Cleaning` `Feature Engineering` `EDA`

## 📬 Contact

**Sourabh Yadav**
- LinkedIn: [linkedin.com/in/sourabhyadav96](https://linkedin.com/in/sourabhyadav96)
- GitHub: [github.com/sourabh0020](https://github.com/sourabh0020)
- Email: sourabhsubh20@gmail.com
