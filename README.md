# 🛍️ Customer Behavior Data Analysis

![Project Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Tools](https://img.shields.io/badge/Tools-Python%20%7C%20SQL%20%7C%20Power%20BI%20%7C%20Gamma-blue)
![Dataset](https://img.shields.io/badge/Dataset-3900%20Records-orange)

---

## 📌 Overview

This end-to-end data analytics project explores customer shopping behavior to uncover patterns in purchasing habits, preferences, and demographics. The goal is to help businesses better understand their customers and make data-driven decisions around marketing, inventory, and customer retention.

The project covers the full analytics pipeline — from raw data ingestion and cleaning to SQL-based analysis, interactive dashboards, and a professional presentation.

---

## 📂 Dataset

- **File:** `customer_shopping_behavior.csv`
- **Records:** 3,900 rows | 18 columns
- **Source:** Publicly available shopping behavior dataset

### Key Columns

| Column | Description |
|--------|-------------|
| `Customer ID` | Unique identifier for each customer |
| `Age` | Age of the customer |
| `Gender` | Male / Female |
| `Item Purchased` | Name of the product bought |
| `Category` | Product category (Clothing, Footwear, Accessories, etc.) |
| `Purchase Amount (USD)` | Transaction value in USD |
| `Season` | Season of purchase |
| `Review Rating` | Customer rating (out of 5) |
| `Subscription Status` | Whether the customer is subscribed (Yes/No) |
| `Shipping Type` | Shipping method used |
| `Discount Applied` | Whether a discount was applied |
| `Previous Purchases` | Number of prior purchases |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Python (Pandas, Matplotlib, Seaborn)** | Data loading, EDA, and cleaning |
| **Jupyter Notebook** | Interactive analysis environment |
| **PostgreSQL / pgAdmin 4** | SQL querying and data analysis |
| **Power BI** | Interactive dashboard and visualizations |
| **Gamma** | Final presentation / report |
| **GitHub** | Version control and project sharing |

---

## 🔄 Project Steps

### Step 1 — Data Loading & Exploration (Python)
- Loaded the dataset using `pandas`
- Explored shape, data types, null values, and basic statistics using `df.info()`, `df.describe()`
- Identified categorical vs. numerical columns

### Step 2 — Exploratory Data Analysis (EDA)
- Analyzed distributions of age, purchase amount, and review ratings
- Visualized category-wise and gender-wise purchase trends
- Explored seasonal buying patterns and shipping preferences
- Used `matplotlib` and `seaborn` for charts and heatmaps

### Step 3 — Data Cleaning
- Handled missing values and corrected data types
- Standardized inconsistent text entries (e.g., category names)
- Removed duplicates and validated key columns

### Step 4 — SQL Analysis (PostgreSQL)
Imported the cleaned dataset into PostgreSQL and ran analytical queries to answer business questions:

```sql
-- Q1. Total revenue by gender
SELECT gender, SUM(purchase_amount) AS revenue
FROM customer
GROUP BY gender;

-- Q2. Customers who used a discount but spent above average
SELECT customer_id, purchase_amount FROM customer
WHERE discount_applied = 'Yes'
  AND purchase_amount >= (SELECT AVG(purchase_amount) FROM customer);

-- Q3. Top 5 products by average review rating
SELECT item_purchased, ROUND(AVG(review_rating::numeric), 2) AS "Average Product Rating"
FROM customer
GROUP BY item_purchased
ORDER BY avg(review_rating) DESC LIMIT 5;

-- Q4. Average purchase amount: Standard vs Express shipping
SELECT shipping_type, ROUND(AVG(purchase_amount), 2)
FROM customer
WHERE shipping_type IN ('Standard', 'Express')
GROUP BY shipping_type;

-- Q5. Subscribed vs non-subscribed customer spend comparison
SELECT subscription_status,
       COUNT(customer_id) AS "total_customer",
       ROUND(AVG(purchase_amount), 2) AS "avg_spend",
       ROUND(SUM(purchase_amount), 2) AS "total_revenue"
FROM customer
GROUP BY subscription_status;
```

### Step 5 — Power BI Dashboard
- Connected Power BI to the cleaned dataset
- Built interactive visuals with slicers for Subscription Status, Gender, Category, and Shipping Type
- Published key KPIs and trend charts

### Step 6 — Report & Presentation
- Generated a written report summarizing findings and recommendations
- Built a professional presentation using **Gamma AI**

---

## 📊 Power BI Dashboard

The dashboard includes:

- **KPI Cards** — Total Customers, Average Purchase Amount, Average Review Rating
- **Donut Chart** — % of Customers by Subscription Status
- **Bar Charts** — Revenue by Category, Sales by Category
- **Horizontal Bar Charts** — Revenue by Age Group, Sales by Age Group
- **Slicers** — Filter by Subscription Status, Gender, Category, and Shipping Type

> 📸 Dashboard Preview

![Dashboard Preview](dashboard_preview.png)

**Key Filters Applied in Sample View:**
- Subscription: **Yes** | Gender: **Male** | Category: **Footwear** | Shipping: **Standard**
- Result: 27 customers | Avg. Purchase $59.70 | Avg. Rating 4.07

---

## 📈 Key Results & Insights

- 🔵 **Subscribed customers** spend significantly more on average than non-subscribers
- 👟 **Footwear** is the top-performing category by both revenue and number of sales
- 👨 **Male customers** account for a higher share of total revenue in the filtered segment
- 🧑 **Young Adults and Middle-aged** groups drive the most revenue across categories
- 🚚 Customers using **Standard shipping** make up the largest shipping segment
- ⭐ Average review rating of **4.07** indicates strong overall customer satisfaction
- 💸 Customers who used **discounts** still spent above average, showing healthy price sensitivity

---

## 🚀 How to Run This Project

### Prerequisites
Make sure you have the following installed:
- Python 3.8+
- Jupyter Notebook or JupyterLab
- PostgreSQL + pgAdmin 4
- Power BI Desktop (Windows)

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/Customer_behavior_data_analysis.git
cd Customer_behavior_data_analysis
```

### 2. Install Python Dependencies
```bash
pip install pandas matplotlib seaborn jupyter
```

### 3. Run the Jupyter Notebook
```bash
jupyter notebook customer_shopping_behavior_analysis.ipynb
```

### 4. Set Up the Database
- Open **pgAdmin 4**
- Create a new database: `customer_behavior`
- Import the cleaned CSV file into a table named `customer`
- Open `Data analytics.sql` and run the queries

### 5. Open the Power BI Dashboard
- Open `Customer_Behavior_Dashboard.pbix` in Power BI Desktop
- Refresh the data source if needed

---

## 📁 Project Structure

```
Customer_behavior_data_analysis/
│
├── 📓 customer_shopping_behavior_analysis.ipynb   # Python EDA & Cleaning
├── 🗄️ Data analytics.sql                          # SQL Queries (PostgreSQL)
├── 📊 Customer_Behavior_Dashboard.pbix            # Power BI Dashboard
├── 📄 customer_shopping_behavior.csv              # Raw Dataset
├── 📑 Report.pdf                                  # Final Report
├── 🎨 Presentation.pdf                            # Gamma Presentation
└── 📋 README.md                                   # Project Documentation
```

## 📃 License

This project is open-source and available under the [MIT License](LICENSE).

---

> ⭐ *If you found this project useful, feel free to star the repository!*
