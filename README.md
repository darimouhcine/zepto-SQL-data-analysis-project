# zepto-SQL-data-analysis-project
A complete SQL data analysis project using Zepto delivery data. Includes data cleaning, business questions, complex SQL queries, KPIs, and insights for decision-making.
🚀 Project Overview

This project simulates how real data analysts work inside fast-paced e-commerce companies like Zepto, Blinkit, or Instamart. Using SQL, we perform a complete data analysis workflow to:

✅ Build and structure a messy, real-world inventory database
✅ Perform EDA (Exploratory Data Analysis) on product availability, categories, and pricing
✅ Clean inconsistent and incorrect data (null values, pricing errors, duplicates)
✅ Convert raw prices from paise to rupees for better reporting
✅ Write business-focused SQL queries to uncover insights on revenue, inventory, discounts, and stock patterns

This project is designed to demonstrate real analyst skills used in the retail, FMCG, and grocery delivery industries.

📁 Dataset Overview

The dataset originates from Kaggle, scraped from Zepto’s live product listings. It closely represents what a real e-commerce inventory system looks like.

Each row represents a unique SKU (Stock Keeping Unit).
Products may appear multiple times because of:

different sizes

different packaging

different discounts

visibility optimization

This mimics the messy catalog structure of real e-commerce databases.

🧾 Columns Description
Column	Description
sku_id	Unique product identifier (Synthetic Primary Key)
name	Product name as shown on the app
category	Category such as Dairy, Snacks, Fruits, Vegetables, Beverages
mrp	Maximum Retail Price (originally in paise, converted to ₹)
discountPercent	Percentage discount on MRP
discountedSellingPrice	Final selling price after discount
availableQuantity	Number of units available in inventory
weightInGms	Weight of the product in grams
outOfStock	TRUE = Out of stock, FALSE = Available
quantity	Number of items per pack — sometimes mixed with grams for loose items
🔧 Project Workflow

A full step-by-step breakdown of the entire SQL workflow:

1️⃣ Database & Table Creation

We start by designing the SQL table structure:

CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);

2️⃣ Data Import

The CSV file is imported using pgAdmin's built-in import tool.

If import causes UTF-8 issues (very common), use the terminal command:

\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');


If UTF-8 error appears:
✔ Open the CSV in Excel → Save As → CSV UTF-8 → Re-import

3️⃣ 🔍 Exploratory Data Analysis (EDA)

We explore the dataset using SQL:

Count total number of products

View a preview of rows

Identify NULL values

Get list of unique categories

Compare in-stock vs out-of-stock products

Detect multiple SKUs for the same product

Check price outliers and weight inconsistencies

4️⃣ 🧹 Data Cleaning

Cleaning tasks include:

✔ Removing rows where MRP = 0 or discounted price = 0
✔ Fixing pricing by converting paise → rupees
✔ Normalizing inconsistent quantities
✔ Handling incorrect category labels
✔ Removing extremely invalid values (negative weights, invalid discounts)

5️⃣ 📊 Business Insights Using SQL

We answer real business questions, including:

🔟 Top 10 best-value products by discount

🚫 High-MRP products currently out of stock

💰 Potential revenue per category

🏷️ Expensive products (MRP > ₹500) with low discounts

🥇 Categories with highest average discount

⚖️ Price-per-gram ranking for value comparison

📦 Grouping products by weight (Low / Medium / Bulk)

🏋️ Total inventory weight per category

These insights help e-commerce teams make pricing, stocking, and marketing decisions.

🛠️ How to Use This Project
1️⃣ Clone the repository
git clone https://github.com/YOUR-USERNAME/zepto-SQL-data-analysis-project.git
cd zepto-SQL-data-analysis-project

2️⃣ Open the main SQL file
zepto_SQL_data_analysis.sql


This file contains:

Table creation

EDA

Cleaning steps

Business queries

Insight generation

3️⃣ Load the dataset

Use pgAdmin, DBeaver, or PostgreSQL CLI.

Steps:

Create database

Run the SQL script

Import the dataset (UTF-8 recommended)

📜 License

MIT License — You are free to use, modify, and share this project.
Attribution is appreciated but not required.
