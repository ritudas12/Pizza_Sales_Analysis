
#  Pizza Sales Data Analysis using SQL

# Project Overview
This project focuses on analyzing pizza sales data using SQL to generate meaningful business insights. It helps understand sales performance, customer ordering behavior, and product popularity.

![image](https://github.com/ritudas12/Pizza_Sales_Analysis/blob/1576245bf095475cf945763fb8284f22eea522e5/Dashboard_img.jpeg)
# Objective
To analyze pizza sales data and extract key insights such as revenue, order patterns, and best-selling pizzas.

# Tools & Technologies
* SQL (MySQL / SQL Server)
* Excel (for dataset)

# Key Analysis Performed

1. Revenue Analysis
* Total Revenue generated
* Average Order Value

 2. Sales Performance
* Total Pizzas Sold
* Total Orders
* Average Pizzas per Order

 3. Time-Based Analysis
* Daily trend of total orders
* Hourly order trends

 4. Category & Size Insights
* % of sales by pizza category
* % of sales by pizza size
* Quantity sold by category

 5. Product Insights
* Top 5 best-selling pizzas
* Bottom 5 least-selling pizzas
  
# Key Insights
* Identified peak order hours and days
* Found most popular pizza categories and sizes
* Determined top-performing and low-performing products

# Project Structure
* `Pizza_sale.xlsx` → Dataset used for analysis
* `pizza_sale_sql_query.sql` → SQL queries for analysis

# PIZZA SALES SQL QUERIES
**1. Total Revenue:**
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
<img width="140" height="41" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/c9bad624-57ac-4de5-a064-4b96f3f42172" />




**2. Average Order Value:**
```sql
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;
```
<img width="181" height="91" alt="Screenshot (10)" src="https://github.com/user-attachments/assets/fd93b894-70fe-405f-bd9d-e1942adbbedc" />


**3. Total Pizzas Sold:**
```sql 
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```
<img width="173" height="84" alt="Screenshot (12)" src="https://github.com/user-attachments/assets/388f6332-0d48-47ce-a4bb-ec709987c8e4" />


**4. Total Orders:**
```sql
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
```
<img width="164" height="79" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/4ef380c9-a100-4d5f-8f0b-80fc00cd7112" />


**5. Average Pizzas Per Order:**
```sql
 SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_per_order
FROM pizza_sales;
```
<img width="181" height="108" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/9e7bf250-1d83-4940-b9d7-35556920839a" />


**A. Daily Trend for Total Orders:**
```sql
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
```

<img width="199" height="202" alt="Screenshot (25)" src="https://github.com/user-attachments/assets/4431a261-211c-4939-8e71-4bfe85799e09" />


**B. Hourly Trend for Orders:**
```sql
SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time);
```
<img width="217" height="352" alt="Screenshot (19)" src="https://github.com/user-attachments/assets/cf271917-e4f6-4b00-a1b1-b6b840fb8a37" />


**C. % of Sales by Pizza Category:**
```sql
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
```
<img width="263" height="110" alt="Screenshot (20)" src="https://github.com/user-attachments/assets/0b739f04-a438-4fec-ac6e-74e4432f0616" />


**D. % of Sales by Pizza Size:**
```sql
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
<img width="249" height="155" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/1ac2288f-d4e3-47de-a2e3-53721e89d2db" />

**E. Total Pizzas Sold by Pizza Category:**
```sql
 SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
<img width="244" height="138" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/2810197e-1893-42b5-b77d-50b3eb3e4de2" />


**F.Top 5 Best Sellers by Total Pizzas Sold:**
```sql
 SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;
```
<img width="315" height="135" alt="Screenshot (23)" src="https://github.com/user-attachments/assets/ac3602d0-4cf9-4773-a050-e3dc6c07349c" />


**G.Bottom 5 Best Sellers by Total Pizzas Sold:**
```sql
 SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
```
<img width="312" height="155" alt="Screenshot (24)" src="https://github.com/user-attachments/assets/cc018b4d-416b-4f5c-ac82-671175ffbef6" />


# Conclusion
This project demonstrates how SQL can be used to analyze real-world sales data and generate actionable business insights.

