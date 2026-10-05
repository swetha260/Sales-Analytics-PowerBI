# 📊 Sales Insights – Brick & Mortar Business

## 📌 Project Overview

This is an end-to-end sales analytics project built using **MySQL, SQL, Power Query, DAX, and Power BI**.

The goal was to transform raw transactional sales data into an interactive business intelligence dashboard that helps analyze performance across **markets, products, customers, and time periods**.

### 🔄 Project Workflow

**Raw MySQL Database → SQL Exploration → Power Query Cleaning → Data Modeling → DAX Measures → Power BI Dashboard → Business Insights**

---

## 📈 Key KPIs

- **Total Sales:** ₹987M
- **Total Quantity Sold:** 2M units
- **Transactions:** 150K
- **Latest YoY Growth:** -15.37%

---

## 🛠️ Tools & Technologies

- MySQL
- MySQL Workbench
- SQL
- Power BI Desktop
- Power Query
- DAX

---

## 🗂️ Dataset

The database contains the following main tables:

- `transactions`
- `customers`
- `products`
- `markets`
- `date`

The `transactions` table acts as the main fact table, while the remaining tables provide customer, product, market, and date information.

---

## 🔍 SQL Data Exploration

SQL was used to inspect the raw data and perform initial data-quality checks.

The analysis included:

- Product-wise sales analysis
- Customer-wise sales analysis
- Market-wise sales analysis
- Monthly and yearly sales analysis
- Missing-value checks
- Duplicate checks
- Invalid sales record detection
- Currency-value investigation
- Referential-integrity checks

### Example SQL Query

```sql
SELECT
    product_code,
    COUNT(*) AS transaction_count,
    SUM(sales_qty) AS total_quantity_sold,
    SUM(sales_amount) AS total_sales_amount
FROM transactions
GROUP BY product_code
ORDER BY product_code ASC;
```

---

## 🧹 Data Cleaning & Transformation

Data cleaning was performed using **Power Query** while keeping the original MySQL database unchanged.

### Currency Standardization

The `currency` column contained visually identical values stored differently because of hidden carriage-return characters.

Examples included:

- `INR`
- `INR\r`
- `USD`
- `USD\r`

These were identified during SQL exploration and standardized in Power Query using:

- **Clean**
- **Trim**

This ensured consistent currency values for reporting.

### Invalid Sales Records

Some rows contained zero or negative values in:

- `sales_qty`
- `sales_amount`

These records were excluded from the reporting dataset during transformation.

### Unmatched Product Codes

A referential-integrity check identified **60 product codes** present in the transaction table but missing from the product master table.

This caused Power BI to group valid sales under `(Blank)`.

To preserve those transactions, product-level analysis used:

`transactions[product_code]`

instead of relying only on the product dimension table.

---

## 🧩 Data Modeling

A relational data model was created in Power BI.

Main relationships included:

- `transactions[customer_code]` → `customers[customer_code]`
- `transactions[product_code]` → `products[product_code]`
- `transactions[market_code]` → `markets[markets_code]`
- `transactions[order_date]` → `date[date]`

Most relationships were configured as:

- **Many-to-One**
- **Single-direction filtering**

The transactions table acts as the central fact table in the model.

---

## 🧮 DAX Measures

Several DAX measures were created to support KPI reporting and time-based analysis.

### Total Sales

```DAX
Total Sales =
CALCULATE(
    SUM(transactions[sales_amount]),
    transactions[currency] = "INR"
)
```

### Total Quantity Sold

```DAX
Total Quantity Sold =
SUM(transactions[sales_qty])
```

### INR Transaction Count

```DAX
INR Transaction Count =
CALCULATE(
    COUNTROWS(transactions),
    transactions[currency] = "INR"
)
```

### Previous Year Sales

```DAX
Previous Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('date'[date])
)
```

### YoY Growth %

```DAX
YoY Growth % =
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    BLANK()
)
```

### Latest YoY Growth

```DAX
YoY Growth KPI =
VAR LatestYear =
    MAX('date'[year])
RETURN
    CALCULATE(
        [YoY Growth %],
        KEEPFILTERS('date'[year] = LatestYear)
    )
```

### Revenue Contribution %

```DAX
Revenue Contribution % =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        REMOVEFILTERS('sales markets'[markets_name])
    ),
    0
)
```



---

## 📊 Dashboard Pages

### 1. Sales Overview

The Sales Overview page includes:

- Total Sales
- Total Quantity Sold
- Transaction Count
- Latest YoY Growth
- Monthly Sales Trend
- Top Products by Sales
- Sales by Market
- Year filter
- Market Location filter

### 2. Performance Analysis

The Performance Analysis page includes:

- Sales vs Previous Year
- YoY Growth Trend
- Revenue Contribution %
- Top Customers
- Market Comparison Table

The market comparison table includes:

- Market
- Total Sales
- Revenue Contribution %
- Previous Year Sales
- YoY Growth %

---

## 💡 Key Business Insights

- Sales increased significantly in **2018**, with YoY growth of approximately **342.79%**.
- Sales declined by approximately **18.79% in 2019** compared with 2018.
- The latest available reporting period showed approximately **-15.37% YoY growth**.
- **Delhi NCR** generated the highest sales among all markets.
- **Mumbai and Ahmedabad** were also major contributors to overall revenue.
- A relatively small group of products contributed a significant share of sales.
- Monthly sales showed noticeable fluctuations, including a dip around September followed by recovery in the following months.

> Note: 2020 contains only the available reporting period in the source dataset, so YoY calculations compare it with the corresponding prior-year period.

---

## 🎯 Skills Demonstrated

- SQL Data Analysis
- SQL Joins
- Aggregations
- Data Exploration
- Data Profiling
- Data Cleaning
- Data Transformation
- Power Query
- Power BI
- DAX
- Data Modeling
- Fact and Dimension Tables
- KPI Reporting
- Time Intelligence
- Year-over-Year Analysis
- Revenue Contribution Analysis
- Sales Analytics
- Trend Analysis
- Top-N Analysis
- Referential-Integrity Analysis
- Data Visualization
- Interactive Dashboard Development
- Business Intelligence

---

## ✅ Project Outcome

This project demonstrates an end-to-end analytics workflow, from raw transactional data in MySQL to a cleaned, modeled, and interactive Power BI dashboard.

It highlights practical experience in **SQL analysis, data cleaning, Power Query, DAX, data modeling, KPI development, and business reporting**.

---
