# Gold Retail Sales Analysis: Building a MySQL Data Warehouse to Generate Business Insights

A business-focused SQL analysis project simulating a real-world retail sales environment. This project demonstrates how to structure and query transactional and dimensional data to generate actionable insights for decision-making.

## Project Objective
The goal is to extract business intelligence from retail sales data using MySQL:
- Compute key performance metrics: revenue, product performance, and customer trends
- Identify top-performing products and categories to guide inventory and marketing decisions
- Analyze customer behavior and distribution for targeted sales strategies
- Practice data modeling and advanced SQL queries in a realistic retail scenario

## Insight:

1. Revenue is highly concentrated ($6.67M) in the Mountain-200 product line, indicating strong demand but exposing the business to concentration risk, making both optimisation and diversification critical.

2. Revenue is highly concentrated ($6.67M) in the Mountain-200 product line, indicating strong demand but exposing the business to concentration risk, making both optimisation and diversification critical.

3. The top 10 customers generated ₦132,023 in revenue, contributing only 0.41% of total sales, while the remaining customer base accounted for 99.59% of revenue.

Revenue is highly distributed across the customer base, with no significant dependence on a small group of high-value customers.

4. Customers from the United States generated ₦9.16M in revenue, accounting for 28.27% of total sales, making it the strongest performing market. Australia closely follows with ₦9.06M (27.95%), while the UK contributes ₦3.39M (10.47%), indicating a sharp revenue drop after the top two markets. A small portion of revenue (0.70%) is associated with undefined country data (n/a), indicating a need for improved customer location data capture.

Recommendations:
- Focus growth efforts on mid-tier markets such as the UK through targeted campaigns, while sustaining performance in core regions.
- Reduce dependency on the Bikes category by reviewing pricing, availability, and positioning of underperforming categories, and introduce bundling strategies to drive incremental revenue.
- While customer revenue is broadly distributed, overall performance depends on a narrow set of products and one category.

## Dataset Overview
Dataset	Description
- dim_customers.csv	

Customer demographics: name, gender, country, birthdate
- dim_products.csv
   
Product details: category, cost, product line, subcategory
- fact_sales.csv

Sales transactions: quantity, price, revenue, order/shipping dates

## Tables Created
Table
- dim_customers;

Stores customer profiles for segmentation and behavioral analysis
- dim_products;

Stores product and category details for performance tracking
- fact_sales;

Core transactional table for revenue and sales metrics

## Technologies & Techniques
MySQL 8.0 — relational database management

SQL (DDL, DML, joins, aggregation, window functions)

CSV files for raw data ingestion

Data modeling for dimension/fact schema

Analytical queries to generate business insights

Full SQL scripts are available in the sql/ folder

## Key Business Insights

The analysis focuses on actionable metrics and business outcomes:

- Revenue & Sales

Total sales revenue, total quantity sold, and average selling price

Revenue distribution across products, categories, and customers

Identification of the top 5 products generating the highest revenue and underperforming products

- Customer Analysis

Customer distribution by country and gender

Revenue contribution per customer to identify high-value segments

Age demographics for targeted marketing strategies

- Product & Category Performance

Total products sold per category and revenue per category

Average product cost vs. selling price to evaluate profitability

Insights into category-level performance trends for inventory planning
