# Customer Shopping Behavior Analysis

An end-to-end **data analytics project** focused on understanding customer shopping behavior through **Python, Pandas, SQL, and Microsoft Power BI**.

The project starts with a raw customer transaction dataset, performs data exploration and preparation using Python, applies feature engineering and data cleaning, analyzes the prepared data using SQL to answer business questions, and presents the results through an interactive Power BI dashboard.

The main purpose of the project is to identify meaningful patterns in **customer spending, product preferences, discount usage, subscription behavior, customer loyalty, shipping choices, and revenue across age groups**.

---

## 📌 Project Overview

Retail businesses collect large amounts of customer transaction data. However, raw transactional data is difficult to interpret directly and does not immediately provide useful business insights.

This project was created to transform customer shopping data into a structured analytical solution.

The overall workflow is:

```text
Raw Dataset
     ↓
Python & Pandas
     ↓
Data Exploration
     ↓
Data Cleaning & Transformation
     ↓
Feature Engineering
     ↓
SQL Analysis
     ↓
Business Insights
     ↓
Power BI Dashboard
```

The project addresses the following business question:

> **How can consumer shopping data be used to identify trends, understand customer behavior, improve customer engagement, and support marketing and product strategies?**

---

# 🎯 Objectives

The main objectives of this project are:

- Analyze customer shopping and purchasing behavior.
- Understand customer demographics and purchasing patterns.
- Identify products with high average review ratings.
- Analyze customers who use discounts while making relatively high-value purchases.
- Compare spending and revenue across subscription status.
- Analyze the use of discounts across different products.
- Segment customers based on previous purchase history.
- Identify the most purchased products within each category.
- Analyze repeat buyers in relation to subscription status.
- Analyze revenue contribution across different age groups.
- Build an interactive Power BI dashboard to communicate the findings visually.

---

# 🗂️ Dataset

The project uses a customer shopping behavior dataset containing:

- **3,900 records**
- **18 columns**
- Customer demographic information
- Product and purchase information
- Shopping behavior information
- Subscription information
- Shipping information
- Review ratings
- Discount and promotional information

### Dataset Statistics

| Attribute | Value |
|---|---:|
| Total Records | 3,900 |
| Total Columns | 18 |
| Missing Values | 37 |
| Missing Column | Review Rating |

The 37 missing values are present in the `Review Rating` column. :chatgpt-content-reference{index="3"}

---

# 📋 Dataset Columns

| Column | Description |
|---|---|
| Customer ID | Unique identifier for each customer |
| Age | Age of the customer |
| Gender | Gender of the customer |
| Item Purchased | Product purchased by the customer |
| Category | Category of the purchased product |
| Purchase Amount (USD) | Amount spent on the purchase |
| Location | Customer location |
| Size | Size of the purchased product |
| Color | Color of the purchased product |
| Season | Season associated with the purchase |
| Review Rating | Rating given for the purchased product |
| Subscription Status | Indicates whether the customer is subscribed |
| Shipping Type | Shipping method selected by the customer |
| Discount Applied | Indicates whether a discount was applied |
| Promo Code Used | Indicates whether a promotional code was used |
| Previous Purchases | Number of previous purchases |
| Payment Method | Payment method used |
| Frequency of Purchases | Frequency at which the customer makes purchases |

---

# 🐍 Data Analysis and Preparation Using Python

Python was used as the first stage of the project for **data loading, exploration, cleaning, and feature engineering**.

The dataset was loaded using Pandas:

```python
import pandas as pd

df = pd.read_csv("customer_shopping_behavior.csv")
```

Initial data exploration was performed to understand the structure and characteristics of the dataset.

Examples of the exploration process include:

```python
df.head()
df.info()
df.describe()
```

The project documentation describes Python as the main environment for preparing the dataset before SQL analysis. :chatgpt-content-reference{index="4"}

---

# 🧹 Data Cleaning and Transformation

The raw dataset was prepared before performing the business analysis.

## 1. Missing Value Handling

The dataset contains **37 missing values in the Review Rating column**.

Instead of deleting these records, the missing review ratings were filled using the **median review rating of the corresponding product category**.

This allowed the existing records to be retained while using category-specific information to handle the missing values. :chatgpt-content-reference{index="5"}

---

## 2. Column Name Standardization

The original column names were standardized into **snake_case** format.

This makes the columns easier to work with in Python and SQL.

Examples:

```text
Customer ID
        ↓
customer_id

Purchase Amount (USD)
        ↓
purchase_amount

Review Rating
        ↓
review_rating

Subscription Status
        ↓
subscription_status
```

This standardization was performed to improve readability, consistency, and ease of querying. :chatgpt-content-reference{index="6"}

---

## 3. Feature Engineering

Additional analytical columns were created from the existing dataset.

### `age_group`

Customer ages were grouped into broader age categories to make demographic analysis easier.

The project uses age groups such as:

- Young Adult
- Middle-aged
- Adult
- Senior

The new `age_group` column was later used in revenue analysis and Power BI visualizations. :chatgpt-content-reference{index="7"}

### `purchase_frequency_days`

A `purchase_frequency_days` feature was created from the purchase-frequency information to support analysis of customer purchasing behavior. :chatgpt-content-reference{index="8"}

---

## 4. Redundant Data Check

The relationship between:

```text
discount_applied
promo_code_used
```

was examined to determine whether the information was redundant.

After the consistency check, the `promo_code_used` column was removed from the analytical dataset. :chatgpt-content-reference{index="9"}

---

# 🧮 SQL Business Analysis

After preparing the dataset, **SQL** was used to answer business-oriented questions from the customer data.

The project contains **10 analytical SQL queries** covering revenue, customer spending, products, discounts, subscriptions, customer segmentation, repeat purchases, shipping, and age groups. :chatgpt-content-reference{index="10"}

## Business Questions

### 1. Revenue by Gender

Calculate the total revenue generated by male and female customers.

```sql
SELECT gender,
       SUM(purchase_amount) AS revenue
FROM customer
GROUP BY gender;
```

---

### 2. High-Spending Discount Users

Identify customers who used a discount but still spent at or above the average purchase amount.

This helps examine high-value purchases made with discounts.

---

### 3. Top 5 Products by Average Rating

Identify the five products with the highest average review rating.

---

### 4. Shipping Type Comparison

Compare the average purchase amount between:

- Standard Shipping
- Express Shipping

---

### 5. Subscribers vs. Non-Subscribers

Compare subscribed and non-subscribed customers using:

- Total number of customers
- Average purchase amount
- Total revenue

---

### 6. Products with the Highest Discount Rate

Identify the five products that have the highest percentage of purchases with discounts applied.

The discount rate is calculated using discounted purchases relative to total purchases for each product.

---

### 7. Customer Segmentation

Customers are divided into three segments based on their previous purchase count:

```text
New
Returning
Loyal
```

The SQL logic used in the project is:

```sql
CASE
    WHEN previous_purchases = 1 THEN 'New'
    WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
    ELSE 'Loyal'
END
```

---

### 8. Top 3 Products per Category

Identify the three most purchased products within every product category.

A SQL window function using `ROW_NUMBER()` is used to rank products within each category.

---

### 9. Repeat Buyers and Subscription Status

Analyze customers with more than five previous purchases and compare their subscription status.

---

### 10. Revenue by Age Group

Calculate the total revenue contribution of each age group.

These ten questions form the main SQL-based business analysis performed in the project. :chatgpt-content-reference{index="11"}

---

# 📊 Power BI Dashboard

After the data preparation and SQL analysis, **Microsoft Power BI** was used to create an interactive dashboard.

The dashboard was designed to provide a visual overview of customer behavior and allow different dimensions of the data to be explored interactively. :chatgpt-content-reference{index="12"}

## Dashboard Includes

### Key Performance Indicators

- Total Number of Customers
- Average Purchase Amount
- Average Review Rating

### Visualizations

- Customer distribution by subscription status
- Revenue by category
- Sales by category
- Revenue by age group
- Sales by age group

### Interactive Filters

The dashboard allows filtering by:

- Subscription Status
- Gender
- Category
- Shipping Type

This makes it possible to examine different customer groups and purchasing patterns interactively.

---

# 📈 Key Analysis Areas

The project focuses on several important areas of customer behavior.

### Customer Spending

Understanding how much customers spend and identifying relatively high-value purchases.

### Product Performance

Identifying highly rated products and frequently purchased products.

### Discount Behavior

Understanding which products have a higher proportion of discounted purchases.

### Subscription Behavior

Comparing subscribed and non-subscribed customers in terms of customer count, average spending, and total revenue.

### Customer Loyalty

Segmenting customers according to previous purchase history into New, Returning, and Loyal groups.

### Shipping Behavior

Comparing customer purchase amounts across different shipping options.

### Demographic Revenue

Analyzing how revenue is distributed across different age groups.

---

# 💡 Business Insights and Recommendations

The analysis can support the following business actions:

### Subscription Strategy

Promote useful and exclusive subscriber benefits to encourage subscription adoption.

### Customer Loyalty Programs

Reward repeat customers and encourage customers to move toward higher loyalty levels.

### Discount Strategy

Review discount usage to balance sales stimulation with profitability and margin considerations.

### Product Marketing

Highlight highly rated and frequently purchased products in promotional campaigns.

### Targeted Marketing

Use customer and demographic insights to target high-revenue groups with relevant campaigns.

These recommendations are based on the documented analysis of subscriptions, customer loyalty, discounts, product performance, and age-group revenue. :chatgpt-content-reference{index="13"}

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Python** | Data preparation and analysis |
| **Pandas** | Data loading, exploration, and transformation |
| **Jupyter Notebook** | Interactive Python analysis |
| **SQL** | Business queries and analytical processing |
| **Microsoft Power BI** | Dashboard and data visualization |
| **CSV** | Source dataset |
| **Git & GitHub** | Version control and project hosting |

---

# 📁 Project Structure

```text
Customer-_Behavior_Analysis/
│
├── customer_shopping_behavior.csv
│
├── Customer_Shopping_Behaviour_Analysis.ipynb
│
├── customer_behavior_sql_queries.sql
│
├── customer_behavior_dashboard.pbix
│
├── LICENSE
│
└── README.md
```

---

# ⚙️ How to Use the Project

## Step 1 — Dataset

The project uses:

```text
customer_shopping_behavior.csv
```

This is the source customer shopping dataset.

---

## Step 2 — Python Notebook

Open:

```text
Customer_Shopping_Behaviour_Analysis.ipynb
```

The notebook is used for loading and exploring the dataset and for the documented data-preparation workflow.

The dataset can be loaded using:

```python
import pandas as pd

df = pd.read_csv("customer_shopping_behavior.csv")
```

---

## Step 3 — SQL Analysis

Open:

```text
customer_behavior_sql_queries.sql
```

The SQL file contains the business analysis queries used in the project.

Execute the queries in your SQL environment after making the prepared customer data available to the SQL table used by the queries.

---

## Step 4 — Power BI Dashboard

Open:

```text
customer_behavior_dashboard.pbix
```

using **Microsoft Power BI Desktop**.

The dashboard provides the visual analysis of the customer shopping data.

---

# 📌 Project Deliverables

The project contains:

- Raw customer shopping dataset
- Python/Jupyter Notebook
- Data preparation and feature engineering workflow
- SQL business-analysis queries
- Power BI dashboard
- Business insights
- Business recommendations
- Project documentation

The overall deliverables follow the intended workflow of data preparation, SQL analysis, visualization, reporting, and repository documentation. :chatgpt-content-reference{index="14"}

---

# 🚀 Skills Demonstrated

This project demonstrates practical knowledge of:

```text
Python
Pandas
Data Cleaning
Data Transformation
Exploratory Data Analysis
Feature Engineering
SQL
Business Analysis
Customer Segmentation
Data Visualization
Power BI
Dashboard Development
Git
GitHub
```

---

# 🎓 Conclusion

The **Customer Shopping Behavior Analysis** project demonstrates how raw customer transaction data can be transformed into useful business insights through a structured analytics workflow.

Python and Pandas are used for data exploration and preparation, including missing-value handling, column standardization, and feature engineering. SQL is then used to answer business questions related to customer spending, products, discounts, subscriptions, loyalty, shipping, and demographics. Finally, Power BI is used to present the results through an interactive dashboard.

The project provides a practical example of using multiple data analytics tools together to move from **raw data to analysis, visualization, and business recommendations**.

---

