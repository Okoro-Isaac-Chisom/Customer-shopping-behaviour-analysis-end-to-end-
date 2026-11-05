# Customer-shopping-behaviour-analysis-end-to-end-
End-to-end customer shopping behaviour analysis: Python (Pandas) for cleaning, SQL Server for business queries, and an interactive Power BI dashboard.

# Customer Shopping Behaviour Analysis

End-to-end data analysis project: **Python (Pandas)** for cleaning and feature engineering, **SQL Server** for business queries, and an interactive **Power BI** dashboard for reporting.

![Dashboard](images/customershopping_behaviour_dashboard.jpg)

## Project Overview

This project analyzes the shopping behaviour of 3,900 customers of a retail store. The goal is to understand who buys, what they buy, how they pay and ship, and how discounts and subscriptions affect spending.

The data moves through three tools:

```
CSV  ->  Python (clean + engineer features)  ->  SQL Server (analysis)  ->  Power BI (dashboard)
```

## Business Questions Answered

1. How much revenue do male and female customers generate?
2. Which discount users spent at or above the average purchase amount?
3. Which 5 products have the highest average review rating?
4. How does average spend differ between Standard and Express shipping?
5. How do subscribers compare with non-subscribers (customers, average spend, total revenue)?
6. Which 5 products depend most on discounts?
7. How many customers are New, Returning or Loyal?
8. What are the top 3 most purchased products in each category?
9. Are repeat buyers (more than 5 previous purchases) more likely to be subscribers?
10. How does revenue vary across age groups?

## Tools and Technologies

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy, Seaborn, Matplotlib) | Data cleaning, exploration, feature engineering |
| SQLAlchemy + pyodbc | Loading the cleaned data into SQL Server |
| SQL Server (T-SQL) | Business analysis queries |
| Power BI | Interactive dashboard |

## Workflow

### 1. Data Cleaning and Feature Engineering (Python)
- Checked for missing values and summarized the dataset
- Filled missing `review_rating` values with the **median of each product category**
- Standardized column names to lowercase snake_case (e.g. `purchase_amount_(usd)` became `purchase_amount`)
- Created an `age_group` column (Young_Adult, Adult, Middle_Aged, Senior) using quartile binning (`pd.qcut`)
- Created a `purchase_frequency_days` column by mapping purchase frequency (Weekly, Monthly, Quarterly, etc.) to days
- Dropped the `promo_code_used` column, which duplicated the information in `discount_applied`
- Loaded the cleaned data into SQL Server through SQLAlchemy and pyodbc

### 2. Analysis (SQL Server)
The 10 queries in [`sql/customerbuyingbehaviour_sql2.sql`](sql/customerbuyingbehaviour_sql2.sql) use:
- Aggregations (`SUM`, `AVG`, `COUNT`) with `GROUP BY`
- Subqueries
- CTEs
- Window functions (`ROW_NUMBER() OVER (PARTITION BY ...)`)
- `CASE WHEN` for customer segmentation
- `TOP` and `CAST` for T-SQL-specific ranking and rounding

### 3. Dashboard (Power BI)
The dashboard connects directly to SQL Server and includes:
- **KPI cards:** total revenue, average purchase amount, average review rating, total customers
- **Charts:** customer distribution by subscription status, revenue by gender, revenue by category, revenue by age group, top 10 products by revenue
- **Slicers:** subscription, gender, category, shipping type, payment method

## Key Insights

- Total revenue of **$233,081** from **3,900 customers**, with an average purchase of **$59.76**
- Average review rating of **3.75**
- Revenue split by gender: **67.74% / 32.26%**
- Only about **27%** of customers are subscribers
- **Clothing** is the top-earning category, followed by Accessories, Footwear and Outerwear
- Blouse, Shirt and Dress lead the top 10 products by revenue
- Revenue is spread fairly evenly across age groups, with Young Adults slightly ahead<img width="986" height="585" alt="customershopping behavioursql" src="https://github.com/user-attachments/assets/cc9da28f-f829-4663-a407-a4157cfd2bb2" />


## Repository Structure

```
customer-shopping-behaviour-analysis/
├── data/
│   └── README.md            # link to the dataset source
├── notebooks/
│   └── Customer_Buying_Behaviour.ipynb
├── sql/
│   └── customerbuyingbehaviour_sql2.sql
├── powerbi/
│   └── Chisom_CustomerBehaviour_Analysis.pbix
├── images/
│   └── customershopping_behaviour_dashboard.jpg
└── README.md
```

## How to Run

1. **Get the data:** download the dataset from [ https://drive.google.com/uc?export=do... ] or[Clean Data Link: https://drive.google.com/uc?id=18MAP3...]and save it as `customer_shopping_behavior2.csv` in the notebook's folder.
2. **Install dependencies:**
   ```bash
   pip install pandas numpy seaborn matplotlib sqlalchemy pyodbc
   ```
3. **Run the notebook:** open `notebooks/Customer_Buying_Behaviour.ipynb` and run all cells. Update the connection details (server and database name) to match your SQL Server instance.
4. **Run the SQL:** open `sql/customerbuyingbehaviour_sql2.sql` in SQL Server Management Studio against the `StoreSalesAnalysis` database.
5. **Open the dashboard:** open the `.pbix` file in Power BI Desktop and refresh the data source to point to your SQL Server.

## Author

**Isaac Okoro**
Full-Stack .NET Developer and Data Analyst 

- GitHub: [Okoro-Isaac-Chisom](https://github.com/Okoro-Isaac-Chisom)
- LinkedIn: [https://www.linkedin.com/in/isaac-chisom-okoro/]

If you found this project useful, give it a star.
<img width="937" height="526" alt="customershopping behaviour dashboard" src="https://github.com/user-attachments/assets/ef561e4e-c38f-4bad-997e-ece9e76eb58c" />
