# Olist-E-Commerce-Sales-Customer-Insights-Dashboard-Power-BI-Project-

![olist logo 2](https://github.com/user-attachments/assets/dd9d5ebd-faac-420b-ac59-99ba7f37ed5c)

## **Introduction**
This Power BI project is built using the Olist e-commerce dataset, focusing on key business insights for sales performance, customer behavior, seller performance, payment analysis, and order cancellations. The dashboard helps business users and stakeholders understand sales trends, customer loyalty, product performance, and other KPIs that influence strategic decisions.

## **Power BI Skills / Concepts Applied**
•	Data Cleaning & Transformation in Power Query (e.g., handling nulls, changing data types, column splitting)  
•	 Data Modeling (Star schema: relationships between orders, customers, sellers, products, etc.)  
•	 DAX Measures (e.g., Total Sales, Average Rating, Profit Margin, Order Cancellation Rate, AOV)  
•	 Custom Date Hierarchies (for time-based analysis by Year-Month)  
•	 KPI Cards & Visual Indicators (e.g., Total Revenue, Repeat Customers)  
•	 Drill-through & Tooltips for page-level filtering  
•	 Bookmarks & Page Navigation  
•	 Scatter Plots, Combo Charts, Maps for geo and trend analysis  
•	 Key Influencer Visual (Optional) for understanding cancellation patterns  

## **About the Data**
The data used in this project is sourced from Kaggle, specifically the Brazilian E-Commerce Public Dataset by Olist. It contains real-world transactions made between 2016 and 2018 on Olist — a large B2C marketplace in Brazil.  
This dataset provides a comprehensive view of the entire e-commerce process, from order placement to customer delivery and reviews. It includes:  

olist_orders_dataset.csv – order lifecycle and statuses  
olist_order_items_dataset.csv – product-level order data  
olist_customers_dataset.csv – customer IDs and locations  
olist_sellers_dataset.csv – seller IDs and locations  
olist_products_dataset.csv – product metadata and categories  
olist_order_reviews_dataset.csv – customer reviews and ratings  
olist_order_payments_dataset.csv – payment types and values  
product_category_name_translation.csv – English translations for category names  

This rich, multi-table dataset enabled robust data modeling, KPI analysis, and insight generation in a realistic e-commerce setting.  

## **Data Transformation in Power Query**
The dataset was imported into Power BI's Power Query Editor for thorough data validation and cleaning. To ensure accurate profiling, the setting was adjusted from "Based on top 1000 rows" to "Based on entire dataset", and features like Column Quality, Column Distribution, and Column Profile were enabled to inspect and validate each column.  

Below is a summary of the key transformation steps applied:  

 Applied "Use First Row as Headers" to tables where needed.  
 Verified and corrected data types across all columns.  
 Converted monetary values (e.g., price, payment_value) to Fixed Decimal Number for consistency in calculations.  
 Formatted text columns to Proper Case where appropriate (e.g., city names).  
 Standardized special characters (e.g., "são paulo" was cleaned to "sao paulo").  
 Replaced abbreviated names with full names for better readability.  
 Extracted Date from datetime columns to support date-based analysis (e.g., from order_purchase_timestamp).  
 Merged the product_category_name_translation table with the products table for English product categories.  
 Removed duplicate entries where applicable (e.g., in customer and seller tables).  
 Dropped redundant or irrelevant columns to streamline the model.  

These transformations ensured a clean, reliable dataset ready for advanced modeling and insight generation in Power BI.  
The dataset had 8 tables after validation and cleaning. Details of cleaning per table can be found [here](Data_Transformation_Summary.pdf). Below are snapshots of the transformed tables.

