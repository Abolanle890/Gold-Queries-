# Gold Retail Sales Analysis: Building a MySQL Data Warehouse to Generate Business Insights

A business-focused SQL analysis project simulating a real-world retail sales environment. This project demonstrates how to structure and query transactional and dimensional data to generate actionable insights for decision-making.

## Project Objective
The goal is to extract business intelligence from retail sales data using MySQL:
- Compute key performance metrics: revenue, product performance, and customer trends
- Identify top-performing products and categories to guide inventory and marketing decisions
- Analyze customer behavior and distribution for targeted sales strategies
- Practice data modeling and advanced SQL queries in a realistic retail scenario

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

Example Insight:

The top 5 products generate over 60% of total revenue, highlighting critical revenue drivers. Customers in Country X contribute the highest sales, revealing a key market segment for targeted campaigns.

