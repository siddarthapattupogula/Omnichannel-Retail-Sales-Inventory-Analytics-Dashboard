# Omnichannel-Retail-Sales-Inventory-Analytics-Dashboard
Built an Omnichannel Retail Sales Analytics Dashboard using Python, SQL, and Power BI to clean, analyze, and visualize retail transaction data, uncovering sales trends, top products, regional performance, and peak purchasing times for better business decisions.

week 1 -- Data Collection, Environment Setup & Data Cleaning
Objective

The goal of Week-1 is to prepare raw retail transaction data for analysis by cleaning, transforming, and structuring the dataset using Python and Pandas.

Tools & Technologies
Python
Pandas
NumPy
Jupyter Notebook
GitHub
1. Dataset Creation

An example retail dataset was created using Python dictionaries and converted into a Pandas DataFrame.

2. Data Exploration

Initial exploration was performed to understand the dataset.

Tasks performed:

Checked dataset shape
Reviewed column names
Verified data types

Functions used:

df.shape
df.columns
df.dtypes
3. Missing Value Detection

Missing values were identified using:

df.isnull().sum()

Columns with missing values:

quantity
city
4. Handling Missing Values

Two strategies were applied:

Quantity

Missing quantity values were filled using the median value.

df["quantity"] = df["quantity"].fillna(df["quantity"].median())

City

Missing city values were replaced with "Unknown".

df["city"] = df["city"].fillna("Unknown")
5. Removing Duplicate Records

Duplicate transactions were detected and removed.

df = df.drop_duplicates()

This ensures accurate sales calculations.

6. Date Format Conversion

The order_date column was converted into datetime format for time-based analysis.

df["order_date"] = pd.to_datetime(df["order_date"])
7. Feature Engineering

New columns were created to improve analysis.

Revenue Calculation

Revenue was calculated as:

Revenue = Quantity × Price
df["revenue"] = df["quantity"] * df["price"]
8. Time Feature Extraction

Additional columns were created from the order date:

df["year"] = df["order_date"].dt.year
df["month"] = df["order_date"].dt.month
df["day"] = df["order_date"].dt.day
df["hour"] = df["order_date"].dt.hour

These features help analyze:

Monthly sales trends
Daily order patterns
Peak purchasing hours
9. Text Standardization

Product names were standardized to maintain consistency.

df["product"] = df["product"].str.lower().str.strip()

week -- 2

Relational Database Design & SQL Data Analysis

Database Setup
1. Create Database

A dedicated database was created to store retail sales data.

CREATE DATABASE retail_analytics;
USE retail_analytics;

Purpose:

Organize retail transaction data
Enable efficient querying and analysis
Table Design
2. Create Sales Table

The cleaned dataset was stored in a structured table called sales_data.

CREATE TABLE sales_data (
    order_id INT,
    product VARCHAR(50),
    category VARCHAR(50),
    quantity INT,
    price DECIMAL(10,2),
    revenue DECIMAL(12,2),
    city VARCHAR(50),
    order_date DATETIME,
    year INT,
    month INT,

    Data Verification

After importing the cleaned dataset, the table was verified using:

SELECT * FROM sales_data;

Purpose:

Confirm successful data import
Validate dataset structure
SQL Business Analysis

Several SQL queries were written to extract important business metrics.

1. Total Revenue
SELECT SUM(revenue) AS total_revenue
FROM sales_data;

Purpose:

Calculate overall business revenue
Measure total sales performance
2. Total Orders
SELECT COUNT(order_id) AS total_orders
FROM sales_data;

Purpose:

Determine the number of transactions
3. Average Revenue per Order
SELECT AVG(revenue) AS avg_revenue_per_order
FROM sales_data;

Purpose:

Identify average order value
4. Best-Selling Products
SELECT product, SUM(quantity) AS total_quantity_sold
FROM sales_data
GROUP BY product
ORDER BY total_quantity_sold DESC;

Purpose:

Identify most popular products
Help businesses prioritize inventory
5. Revenue by Product Category
SELECT category, SUM(revenue) AS category_revenue
FROM sales_data
GROUP BY category
ORDER BY category_revenue DESC;

Purpose:

Determine top-performing product categories
6. Sales by City
SELECT city, SUM(revenue) AS city_revenue
FROM sales_data
GROUP BY city
ORDER BY city_revenue DESC;

Purpose:

Compare sales performance across different cities
7. Monthly Sales Trend
SELECT month, SUM(revenue) AS monthly_sales
FROM sales_data
GROUP BY month
ORDER BY month;

Purpose:

Identify seasonal sales patterns
8. Yearly Sales Performance
SELECT year, SUM(revenue) AS yearly_sales
FROM sales_data
GROUP BY year
ORDER BY year;

Purpose:

Track year-to-year business growth
9. Peak Sales Hours
SELECT hour, SUM(revenue) AS hourly_sales
FROM sales_data
GROUP BY hour
ORDER BY hourly_sales DESC;

Purpose:

Identify highest purchasing hours
Optimize store staffing and marketing campaigns
10. Top Revenue Generating Products
SELECT product, SUM(revenue) AS product_revenue
FROM sales_data
GROUP BY product
ORDER BY product_revenue DESC
LIMIT 5;

Purpose:

Identify highest revenue generating products
11. Average Order Value by City
SELECT city, AVG(revenue) AS avg_order_value
FROM sales_data
GROUP BY city
ORDER BY avg_order_value DESC;

Purpose:

Analyze customer spending patterns across cities
12. Weekday Sales Performance
SELECT DAYNAME(order_date) AS weekday, SUM(revenue) AS total_sales
FROM sales_data
GROUP BY weekday
ORDER BY total_sales DESC;

Purpose:

Identify best performing weekdays
13. Highest Revenue Day
SELECT order_date, SUM(revenue) AS daily_sales
FROM sales_data
GROUP BY order_date
ORDER BY daily_sales DESC
LIMIT 1;

Purpose:

Identify the single highest revenue day
