# Gold-Queries-

LOAD DATA INFILE 'C:\Users\HomePC\Documents\ABOLANLE\sql-data-analytics-project\datasets\csv-files/to/gold.dim_customers.csv'
INTO TABLE gold.dim_customers
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

SHOW VARIABLES LIKE 'secure_file_priv';

SET sql_mode = '';

CREATE TABLE dim_customers (
    customer_key INT PRIMARY KEY,
    customer_id INT,
    customer_number VARCHAR(20), 
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    country VARCHAR(50),
    marital_status VARCHAR(20),
    gender VARCHAR(10),
    birthdate DATE,
    create_date DATETIME
);


LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/gold.dim_customers.csv'
INTO TABLE dim_customers
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

SELECT * FROM dim_customers;

CREATE TABLE dim_products (
    product_key INT PRIMARY KEY,
    product_id INT,
    product_number VARCHAR(20), 
	product_name VARCHAR(50),
    category_id VARCHAR(50),
    category VARCHAR(50),
    subcategory VARCHAR(20),
    maintenance VARCHAR(10),
    cost INT,
    product_line VARCHAR(20),
    start_date DATETIME
);

SET sql_mode = '';

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/gold.dim_products.csv'
INTO TABLE dim_products
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

CREATE TABLE fact_sales (
	order_number VARCHAR (50),
	product_key INT,
	customer_key INT,
	order_date DATETIME,
	shipping_date DATETIME,
	due_date DATETIME,
	sales_amount INT,
	quantity INT,
	price INT
);

SET sql_mode = '';

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/gold.fact_sales.csv'
INTO TABLE fact_sales
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS;

-- Expore all table--
SELECT * FROM INFORMATION_SCHEMA.TABLES;

-- Explore all columns --
SELECT * FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'dim_customers';

-- Explore all countries our customer come from --

SELECT DISTINCT 
country 
FROM dim_customers;

-- Explore all category "The Major Division" --

SELECT DISTINCT 
category,
subcategory,
product_id
FROM dim_products
ORDER BY 1,2,3;

-- Find the date of the first and last order --
-- How many years of sales are available --

SELECT 
MIN(order_date) AS first_order_date,
MAX(order_date) AS last_order_date,
 TIMESTAMPDIFF(year,MIN(order_date),MAX(order_date))
FROM fact_sales;

-- Find the youngest and oldest customer --
SELECT MIN(birthdate) AS youngest_customer,
MAX(birthdate) AS oldest_customer
FROM dim_customers;

-- find the total sales
SELECT SUM(sales_amount)
FROM fact_sales;

-- find how many category are sold
SELECT COUNT(*) category 
FROM dim_products;

-- find how many products are sold
SELECT SUM(quantity) 
FROM fact_sales;

-- find the average selling price
SELECT AVG(price) 
FROM fact_sales;

-- find the total number of orders
SELECT COUNT(order_number)
FROM fact_sales;

SELECT COUNT(DISTINCT order_number)
FROM fact_sales;

-- find the total number of customers that placed an order
SELECT COUNT(customer_key)
FROM dim_customers;

SELECT COUNT(DISTINCT customer_key)
FROM dim_customers;

-- Generate a report that shows all key metrics
SELECT 'Total Sales' AS measure_name, SUM(sales_amount) AS measure_value FROM fact_sales
 UNION ALL
SELECT 'Total Category' AS measure_name, COUNT(category) AS measure_value FROM dim_products
UNION ALL
SELECT 'Total Quantity' AS measure_name, SUM(quantity) AS measure_value FROM fact_sales
UNION ALL 
SELECT 'Total Price' AS measure_name, AVG(price) AS measure_value FROM fact_sales
UNION ALL
SELECT 'Total Order' AS measure_name, COUNT( DISTINCT order_number) AS measure_value FROM fact_sales
UNION ALL
SELECT 'Total NO Customers' AS measure_value, COUNT(customer_key) AS measure_name FROM dim_customers;

-- find the total customer by country
SELECT country, COUNT(customer_key) AS total_customer
FROM dim_customers
GROUP BY country
ORDER BY total_customer DESC;

-- find the total customer by gender
SELECT gender, COUNT(customer_key) AS total_customer
FROM dim_customers
GROUP BY gender
ORDER BY total_customer DESC;

-- find total products by category
SELECT category, COUNT(product_key) AS total_product
FROM dim_products
GROUP BY category
ORDER BY total_product DESC;

-- what is the average cost in each category
SELECT category, AVG(cost) AS average_cost
FROM dim_products
GROUP BY category
ORDER BY average_cost DESC;

-- what is the total revenue generated for each category
SELECT 
p.category,
SUM(f.sales_amount) total_revenue 
FROM fact_sales f
LEFT JOIN dim_products p
ON
p.product_key = f.product_key
GROUP BY p.category
ORDER BY total_revenue DESC;


-- what is the total revenue generated for each customer
SELECT 
c.customer_key,
c.first_name,
c.last_name,
SUM(f.sales_amount) total_revenue 
FROM fact_sales f
LEFT JOIN dim_customers c
ON 
c.customer_key = f.customer_key
GROUP BY 
c.customer_key,
c.first_name,
c.last_name
ORDER BY total_revenue DESC;

-- What is the distribution of sold items access countries 
SELECT 
c.country,
COUNT(f.order_number) total_distribution
FROM dim_customers c
LEFT JOIN fact_sales f
ON
c.customer_key = f.customer_key
LEFT JOIN dim_products p
ON
p.product_key = f.product_key
GROUP BY c.country
ORDER BY total_distribution DESC;

-- which 5 products generate the top revenue 
SELECT
p.product_name,
SUM(f.sales_amount) total_revenue 
FROM fact_sales f
LEFT JOIN dim_products p
ON
p.product_key = f.product_key
GROUP BY p.product_name
ORDER BY total_revenue DESC
LIMIT 5;

-- which 5 products generate the lowest revenue
SELECT *
FROM (
SELECT
p.product_name,
SUM(f.sales_amount) total_revenue,
ROW_NUMBER() OVER(ORDER BY SUM(f.sales_amount)) AS rank_products 
FROM fact_sales f
LEFT JOIN dim_products p
ON
p.product_key = f.product_key
GROUP BY p.product_name) a
WHERE rank_products  >= 5;
