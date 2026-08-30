# Sales Analytics Project — Excel, SQL Server & Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi\&logoColor=black)
![SQL Server](https://img.shields.io/badge/SQL%20Server-Analysis-CC2927?logo=microsoftsqlserver\&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-Data%20Cleaning-217346?logo=microsoftexcel\&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Analysis-5B2C83)
![Data Analytics](https://img.shields.io/badge/Data%20Analytics-Portfolio-2E7D32)

## Project Overview

This project is an end-to-end **Sales Analytics solution** built using **Microsoft Excel, SQL Server, and Power BI**.

The project covers the complete analytics workflow, starting with **data preparation and cleaning in Excel**, followed by **data exploration and analysis using SQL Server**, and ending with an interactive **Power BI Sales Analytics Dashboard**.

The analysis focuses on sales performance, product performance, customer behavior, regional sales, payment methods, purchasing patterns, discounts, and sales trends over time.

---

# Data Preparation & Cleaning — Excel

The original sales dataset contains **1,000 records and 13 columns**. Excel was used to review, clean, and prepare the dataset before performing SQL analysis and Power BI visualization.

### Data Quality Checks

During the data preparation stage, the dataset was reviewed for:

* Duplicate records
* Missing values
* Inconsistent text formatting
* Data type consistency
* Invalid age values
* Inconsistent date formats
* Inconsistent payment-method capitalization
* Regional name consistency

### Cleaning Activities

The data preparation process included:

* Identifying and removing duplicate records.
* Reviewing missing values across important fields.
* Standardizing inconsistent text values such as region and payment method names.
* Reviewing invalid/non-numeric values in the `Age` field.
* Standardizing date formats in `Order_Date`.
* Checking numeric fields such as `Quantity`, `Unit_Price`, and `Sales`.
* Preparing the dataset for SQL Server analysis and Power BI reporting.

### Dataset Structure

The dataset contains the following fields:

```text
Order_ID
Customer_Name
Gender
Age
Product
Region
Quantity
Unit_Price
Discount
Sales
Order_Date
Payment_Method
Sales_Channel
```

### Initial Data Quality Findings

| Data Quality Check      | Finding |
| ----------------------- | ------: |
| Total Records           |   1,000 |
| Columns                 |      13 |
| Duplicate Rows          |      14 |
| Missing Customer Names  |      28 |
| Missing Ages            |      23 |
| Missing Products        |      18 |
| Missing Regions         |      20 |
| Missing Quantities      |      17 |
| Missing Unit Prices     |      17 |
| Missing Sales Values    |      26 |
| Missing Order Dates     |      19 |
| Missing Payment Methods |      15 |

> These checks were performed on the uploaded source dataset before/while preparing the data for analysis.

---

# SQL Server Analysis

After data preparation, SQL Server was used to explore the dataset and answer business-focused sales questions.

## SQL Analysis Performed

### 1. Dataset Overview

The dataset was reviewed using row counts and distinct-value analysis.

```sql
SELECT COUNT(*) AS Total_Rows
FROM Sales_customer;

SELECT
    COUNT(*) AS Total_Rows,
    COUNT(DISTINCT Customer_Name) AS Unique_Customers,
    COUNT(DISTINCT Product) AS Unique_Products,
    COUNT(DISTINCT Region) AS Unique_Regions,
    COUNT(DISTINCT Gender) AS Unique_Genders
FROM Sales_customer;
```

### 2. Regional Analysis

Analyzed the number of sales records and total sales by region.

```sql
SELECT
    Region,
    COUNT(*) AS Total
FROM Sales_customer
GROUP BY Region
ORDER BY Region;
```

Total sales by region:

```sql
SELECT
    Region,
    SUM(Sales) AS Total_Sales
FROM Sales_customer
GROUP BY Region
ORDER BY Total_Sales DESC;
```

### 3. Gender Analysis

Reviewed the distribution of sales records by gender.

```sql
SELECT
    Gender,
    COUNT(*) AS Total
FROM Sales_customer
GROUP BY Gender;
```

### 4. Total Sales

Calculated total sales across the dataset.

```sql
SELECT
    SUM(CAST(Sales AS DECIMAL(18,2))) AS Total_Sales
FROM Sales_customer;
```

### 5. Sales by Product

Identified which products generate the highest sales.

```sql
SELECT
    Product,
    SUM(Sales) AS Total_Sales
FROM Sales_customer
GROUP BY Product
ORDER BY Total_Sales DESC;
```

### 6. Quantity Sold by Product

Analyzed product demand based on quantity sold.

```sql
SELECT
    Product,
    SUM(Quantity) AS Total_Quantity
FROM Sales_customer
GROUP BY Product
ORDER BY Total_Quantity DESC;
```

### 7. Customer Sales Analysis

Identified customers contributing the highest sales.

```sql
SELECT
    Customer_Name,
    SUM(Sales) AS Total_Sales
FROM Sales_customer
GROUP BY Customer_Name
ORDER BY Total_Sales DESC;
```

### 8. Payment Method Analysis

Compared order volume and sales across payment methods.

```sql
SELECT
    Payment_Method,
    COUNT(*) AS Total_Orders,
    SUM(Sales) AS Total_Sales
FROM Sales_customer
GROUP BY Payment_Method
ORDER BY Total_Sales DESC;
```

## SQL Skills Demonstrated

* `SELECT`
* `WHERE`
* `GROUP BY`
* `ORDER BY`
* `COUNT()`
* `COUNT(DISTINCT)`
* `SUM()`
* `CAST()`
* Aggregate functions
* Data exploration
* Business-focused SQL analysis

---

# Power BI Dashboard

The prepared dataset was used to build an interactive **Power BI Sales Analytics Dashboard**.

The dashboard contains two analytical pages, moving from an executive overview to deeper product and customer analysis.

## Dashboard Pages

### Page 1 — Sales Analytics Dashboard

**Purpose:** Executive-level overview of sales performance.

Key elements:

* Total Sales
* Total Orders
* Total Quantity
* Average Order Value
* Monthly Sales Trend
* Sales by Product
* Sales by Region
* Sales by Gender
* Sales by Payment Method
* Top 10 Customers by Sales
* Sales vs Quantity by Product
* Interactive Product slicer

### Page 2 — Product & Customer Analytics

**Purpose:** Detailed analysis of product performance and customer contribution.

Key elements:

* Total Sales
* Total Orders
* Average Order Value
* Top Product Sales
* Average Order Value by Product
* Quantity Sold by Product
* Top 10 Customers by Sales
* Sales by Discount Level
* Sales by Product

---

# Business Questions

The project was designed to answer the following questions:

* How is overall sales performance changing over time?
* Which products generate the most sales?
* Which products have the highest average order value?
* Which customers contribute the most revenue?
* How do sales vary across regions?
* Which payment methods are most commonly used?
* Is there a relationship between quantity sold and sales?
* How do different discount levels relate to sales?

---

# Key KPIs

| KPI                 |  Result |
| ------------------- | ------: |
| Total Sales         | 674.52K |
| Total Orders        |     818 |
| Total Quantity      |      4K |
| Average Order Value |  824.60 |
| Top Product Sales   | 217.45K |

---

# Key Insights

Based on the Power BI dashboard:

1. **Total sales reached 674.52K** across 818 orders.
2. **Average Order Value is 824.60**, providing a useful measure of revenue generated per order.
3. **Laptop is the leading product by sales**, contributing approximately 217.45K.
4. Product performance differs depending on the metric; a product with high quantity sold does not necessarily generate the highest revenue.
5. A relatively small group of customers contributes a significant share of sales, making customer-level analysis valuable for understanding revenue concentration.
6. Regional and payment-method analysis provides additional context for understanding how sales are distributed.
7. Discount-level analysis helps evaluate how different discount levels relate to sales performance.
8. Monthly sales analysis provides visibility into changes in sales activity over time.

> **Note:** These insights are based on the current dataset and Power BI dashboard and should be interpreted within the scope of the available data.

---

# Tools & Skills

## Data Preparation

* Microsoft Excel
* Data cleaning and preparation
* Duplicate identification and removal
* Missing-value checks
* Data consistency checks
* Text standardization
* Date-format standardization
* Data type validation

## SQL & Data Analysis

* Microsoft SQL Server
* SQL
* Data exploration
* Aggregation
* Business-focused analysis
* Customer analysis
* Product analysis
* Regional analysis
* Payment-method analysis

## Power BI

* Microsoft Power BI
* Power Query
* DAX
* KPI development
* Interactive slicers
* Data visualization
* Dashboard design
* Business intelligence

---

# Dashboard Screenshots

Use the following screenshot structure:

```text
Screenshots/
├── page1-sales-overview.png
└── page2-product-customer.png
```

## Dashboard Preview

### Page 1 — Sales Analytics Dashboard

![Page 1](Screenshots/page1-sales-overview.png)

### Page 2 — Product & Customer Analytics

![Page 2](Screenshots/page2-product-customer.png)

---

# Repository Structure

```text
sales-analytics-powerbi/
│
├── README.md
│
├── SQL/
│   └── Sales_Analysis.sql
│
├── PowerBI/
│   └── Sales_Analytics_Dashboard.pbix
│
├── Dataset/
│   └── sales_data.csv
│
└── Screenshots/
    ├── page1-sales-overview.png
    └── page2-product-customer.png
```

---

# How to Explore the Project

### Excel Data Preparation

The source sales dataset was reviewed and prepared in Excel. Data quality checks were performed for duplicates, missing values, inconsistent text values, invalid age entries, date formats, and numeric fields.

### SQL Server Analysis

1. Open `SQL/Sales_Analysis.sql` in SQL Server Management Studio.
2. Connect to the database containing the `Sales_customer` table.
3. Run the SQL queries to explore sales, products, customers, regions, and payment methods.

### Power BI Dashboard

1. Open the `.pbix` file in **Power BI Desktop**.
2. Review Page 1 for the executive sales overview.
3. Navigate to Page 2 for product and customer analysis.
4. Use the interactive Product slicer and visual interactions to explore the dataset.
5. Compare KPI cards with the charts to identify sales patterns and business insights.

---

# End-to-End Analytics Workflow

```text
Raw Sales Dataset
       ↓
Excel Data Preparation
       ↓
Data Quality Checks
       ↓
SQL Server Analysis
       ↓
Power BI / DAX
       ↓
Interactive Sales Dashboard
       ↓
Business Insights
```

---

# Portfolio Value

This project demonstrates an end-to-end approach to **Sales Data Analytics**, from raw data preparation to SQL analysis and interactive business intelligence reporting.

It showcases practical ability to:

* Prepare and clean real-world-style sales data
* Identify duplicate and missing records
* Standardize inconsistent data
* Analyze sales data using SQL Server
* Perform customer, product, regional, and payment analysis
* Develop KPIs using Power BI and DAX
* Build interactive dashboards
* Translate analytical results into business insights
* Present data through professional dashboard storytelling

The project demonstrates practical skills across **Excel, SQL Server, Power BI, DAX, data cleaning, data analysis, and business intelligence**.

---

# Author

**Abdisalaam Hassan Ahmed**

**Data Analytics | SQL | Power BI | Excel**
