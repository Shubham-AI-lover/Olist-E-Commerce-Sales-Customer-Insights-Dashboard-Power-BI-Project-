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


#### **olist orders**
<img width="1794" height="773" alt="Olist_orders" src="https://github.com/user-attachments/assets/bc55f8cd-837e-4950-9e85-d0a3833c9a48" />  

#### **olist order items**  
<img width="1802" height="820" alt="Olist_order_items" src="https://github.com/user-attachments/assets/c44ddfd5-0f86-4224-8b91-4a187c94f378" />  

#### **olist customers**  
<img width="1526" height="759" alt="Olist_customers" src="https://github.com/user-attachments/assets/253e092e-b55e-417f-af33-8b17bfa705a4" />  

#### **olist geolocation**  
<img width="1252" height="757" alt="olist_geolocation" src="https://github.com/user-attachments/assets/f5afdefc-dd38-41e3-8a58-30337680569e" />  

#### **olist order payments**
<img width="1220" height="813" alt="olist_order_payments" src="https://github.com/user-attachments/assets/3c555073-951f-42b5-afa0-fb3932f6588a" />  

#### **olist order reviews**
<img width="1746" height="785" alt="Olist_order_reviews" src="https://github.com/user-attachments/assets/d6e84153-dc73-409e-9c9c-ae2190b0a92a" />  

#### **olist products**
<img width="1805" height="771" alt="Olist_products" src="https://github.com/user-attachments/assets/d6c3c173-5dcb-4710-a2e7-5fa0aac36a89" />  

#### **olist sellers**
<img width="1001" height="758" alt="olist_sellers" src="https://github.com/user-attachments/assets/77be897e-de1f-4a29-984e-b81b80028f8c" />


## **Data Modeling**

To enable meaningful analysis, the dataset was modeled into a Star Schema using Power BI. Since the source data was normalized (spread across multiple related tables), data modeling was crucial to establish proper relationships and support efficient querying.  

The final model consists of:  

#### **Fact Table**  
###### olist_order_items  
Serves as the central fact table containing the most granular transactional data. It includes measurable, quantitative fields such as product price and freight value, which can be aggregated for analysis.  

#### **Factless Fact Table**  
###### olist_orders  
This table acts as a bridge table containing key timestamp columns (e.g., purchase, approval, delivery dates) and foreign keys to other dimension tables. It does not include any numeric measures itself, hence classified as a factless fact table.

#### **Dimension Tables**  
###### olist_customers –Customer details like location and state 
###### olist_geolocation –Latitude/longitude and ZIP-code-based location info  
###### olist_order_payments –Payment type and amount 
###### olist_order_reviews –Customer feedback and ratings
###### olist_products –Product categories and metadata
###### olist_sellers –Seller’s location and state info  


### Date Dimension
To support time-based analysis, a custom DimDate table was created using DAX in Power BI. The table spans from January 1, 2016 to December 30, 2018 and includes both calendar and fiscal attributes to enable dynamic filtering, grouping, and time intelligence calculations.

The following columns were added:
#### Calendar Columns:
Year – Extracted using YEAR()  
Month – Full month name using FORMAT('Date'[Date], "MMMM")  
Month Number – Numeric month using MONTH()  
Quarter – Quarter extracted as "Q" & QUARTER()  
Week Number – Week of the year using WEEKNUM()  
Day of the Week – Name of the weekday using FORMAT(WEEKDAY(), "dddd")  

#### Fiscal Calendar Columns:    
Fiscal Year= YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) >= 4, 1, 0)  
Fiscal Quarter= SWITCH(  
    TRUE(),  
    MONTH('Date'[Date]) IN {4, 5, 6}, "Q1",  
    MONTH('Date'[Date]) IN {7, 8, 9}, "Q2",  
    MONTH('Date'[Date]) IN {10, 11, 12}, "Q3",  
    MONTH('Date'[Date]) IN {1, 2, 3}, "Q4"  
)  
Fiscal Month Number= MOD(MONTH('Date'[Date]) + 8, 12) + 1     
Fiscal Month = FORMAT('Date'[Date], "MMMM")  

These DAX formulas were written manually in Power BI using calculated columns to build a robust and reusable date dimension for business analysis.  


<img width="1364" height="686" alt="Data Modelling" src="https://github.com/user-attachments/assets/43be279c-3936-4e19-a4db-2c96673b0c9b" />  

ThReport Pages Overviewe project follows a Star Schema design with olist_order_items as the central Fact Table, surrounded by related Dimension Tables such as customers, products, sellers, payments, reviews, and a custom date dimension. The model enables efficient slicing, dicing, and filtering across time, geography, and product-related metrics.  

## Report Pages & Visualizations  

The Power BI dashboard is structured into multiple report pages, each focusing on a key area of e-commerce business analysis. These pages are designed to help stakeholders gain actionable insights through interactive and dynamic visuals.  

### Report Pages Overview  

**Business Snapshot**  
A high-level overview of key business metrics, such as total sales, orders, revenue, and customer trends.  

**Category & Product Insights**  
Understand product performance, category trends, and customer preferences across different product types.  

**Customer Behavior & Loyalty**  
Analyze customer purchase frequency, retention rates, and identify loyal vs. one-time buyers.  

**Customer Location & Retention**  
Visualize geographical distribution of customers and track customer churn and repeat behavior across regions.  

**Seller Performance**  
Evaluate seller contributions, order fulfillment efficiency, and delivery performance.  

**Orders & Payments Analytics**  
Dive into payment types, transaction values, and patterns of installment-based purchases.  

**Order Cancellations Analysis**  
Identify the causes and trends of cancellations to improve fulfillment processes and customer satisfaction.  

**Profitability & Marketing**  
Explore profit margins, marketing efforts, and campaign performance to support strategic decision-making.  


### Key Measures & KPIs Used  
Below are the main DAX measures calculated and used in the report:  

**(1)**  
``` DAX  
Total Revenue = 
CALCULATE(
    SUM('olist_order_payments_dataset'[payment_value]),
    'olist_orders_dataset'[order_status] = "delivered"
)
```

**(2)**
``` DAX
 Total orders Placed = COUNT(olist_orders_dataset[order_id])
```
**(3)**
``` DAX
Total Orders(Delivered) = CALCULATE(
    COUNT(olist_orders_dataset[order_id]),
    olist_orders_dataset[order_status]="delivered"
)
```

**(4)**  
``` DAX
Average Rating = 
CALCULATE(
    AVERAGE('olist_order_reviews_dataset'[review_score])
)
```

**(5)**  
``` DAX
Active Sellers = 
CALCULATE(
    DISTINCTCOUNT(olist_order_items_dataset[seller_id]),
    olist_orders_dataset[order_status]="delivered",
    'olist_orders_dataset'[order_purchase_timestamp]>= MIN(olist_orders_dataset[order_purchase_timestamp])-30,
    olist_orders_dataset[order_purchase_timestamp]<=MAX(olist_orders_dataset[order_purchase_timestamp]))
```

**(6)**
``` DAX
Repeat Purchase Customers = CALCULATE(
     DISTINCTCOUNT(olist_customers_dataset[customer_unique_id]),
     olist_customers_dataset[Repeat Purchase]=1,
     olist_orders_dataset[order_status]="delivered"
)
```
**(7)**
``` DAX
Gross Profit Margin = DIVIDE(
    CALCULATE(SUM(olist_order_items_dataset[price]),
    olist_orders_dataset[order_status]="delivered"),
    [Total Revenue])
```

**(8)**  
``` DAX
Average Order Value = 
DIVIDE([Total Revenue],
CALCULATE(COUNT(olist_orders_dataset[order_id]),
olist_orders_dataset[order_status]="delivered")
)
```

**(9)**
``` DAX
Aov by Product Category = 
DIVIDE([Total Revenue],
    CALCULATE([Total Orders(Delivered)]
    )
)
```

**(10)**
``` DAX
Average Order Cancellation Rate = 
DIVIDE(
    CALCULATE(COUNTROWS(olist_orders_dataset),
    olist_orders_dataset[order_status]="canceled"),
    COUNTROWS(olist_orders_dataset)
)
```
**(11)**
```DAX
Customer Retention Rate% = 
 DIVIDE([Repeat Purchase Customers],
 COUNTROWS('olist_customers_dataset'))
 *100
```

**(12)**
```DAX
Number of Products = CALCULATE(
    DISTINCTCOUNT('olist_order_items_dataset'[product_id]),
    olist_orders_dataset[order_status]="delivered"
)
```

## (1) Business Snapshot  
<img width="1297" height="702" alt="Business_Snapshot" src="https://github.com/user-attachments/assets/67d28c0e-2a82-4a47-8a26-47e953f86242" />  

The Business Snapshot page provides a high-level overview of key performance indicators for the Olist e-commerce dataset, helping stakeholders quickly understand business health and trends.

**Total Revenue**:
The total revenue generated from delivered orders is approximately $15.42M, showing strong sales performance over the dataset period (2016–2018).  
**Total Orders Placed**:
Around 96,478 orders were successfully placed, reflecting healthy customer activity.  
**Average Order Value**:
The average value per order is $159.85, which indicates moderate to high-value purchases by customers.  
**Active Sellers**:
The platform had 2,970 active sellers, showcasing a wide seller network contributing to the marketplace.
#### Visual Trend Analysis:  
**Revenue by Year**:
A consistent upward trend is observed from 2016 to 2018, demonstrating growing business performance year-over-year.

**Revenue by Date**:
Daily revenue insights show fluctuations with a few noticeable peaks, suggesting promotional periods or high-demand days.

**Order Variation (Year & Month)**:
Monthly order trends reveal seasonality, with peaks in late 2017 and early 2018 — useful for marketing and inventory planning.  

#### Business Insight:
This snapshot enables quick decision-making by combining key metrics with trend visuals. It helps identify business growth patterns, active seller engagement, and order behaviors over time.



  











