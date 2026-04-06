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
