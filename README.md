
# 🍕 Pizza Sales Data Analysis using SQL

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
# 1. Total Revenue:
```sql SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;```

# 2. Average Order Value
```sql SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;```

# 3. Total Pizzas Sold
```sql SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;```

# 4. Total Orders
```sql SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales```

# 5. Average Pizzas Per Order
```sql
 SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_per_order
FROM pizza_sales
```

# A. Daily Trend for Total Orders
```sql
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
```

# B. Hourly Trend for Orders
```sql
SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)
```

# C. % of Sales by Pizza Category
```sql
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
```


# D. % of Sales by Pizza Size
```sql
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size
```

# E. Total Pizzas Sold by Pizza Category
```sql
 SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
```

# F.Top 5 Best Sellers by Total Pizzas Sold
```
sql SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
```

# G.Bottom 5 Best Sellers by Total Pizzas Sold
```
sql SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
```

# How to Use
1. Import the dataset into your SQL database
2. Run the SQL queries provided
3. Analyze the results and visualize if needed

# Conclusion
This project demonstrates how SQL can be used to analyze real-world sales data and generate actionable business insights.

