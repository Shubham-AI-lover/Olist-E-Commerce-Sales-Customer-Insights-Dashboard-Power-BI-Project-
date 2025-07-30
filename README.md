# Olist-E-Commerce-Sales-Customer-Insights-Dashboard-Power-BI-Project-

![olist logo 2](https://github.com/user-attachments/assets/dd9d5ebd-faac-420b-ac59-99ba7f37ed5c)  

Report Pages Link - https://app.powerbi.com/links/Tw4gO2Vv-G?ctid=de48c0a9-b273-4256-bf3f-a462f226476a&pbi_source=linkShare  

Dashboard Link - https://app.powerbi.com/groups/me/dashboards/bcfd1760-daa0-469a-8c1e-fe0ece197fd3?ctid=de48c0a9-b273-4256-bf3f-a462f226476a&pbi_source=linkShare

## **Introduction**
This Power BI project is built using the Olist e-commerce dataset, focusing on key business insights for sales performance, customer behavior, seller performance, payment analysis, and order cancellations. The dashboard helps business users and stakeholders understand sales trends, customer loyalty, product performance, and other KPIs that influence strategic decisions.
### **Note**: The currency used in this dashboard remains in US Dollars (USD) as per the original dataset. It has not been converted to Brazilian Real (R$) for consistency and clarity.

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
The data used in this project is sourced from **Kaggle**, specifically the **Brazilian E-Commerce Public Dataset by Olist**. It contains real-world transactions made between 2016 and 2018 on Olist — a large B2C marketplace in Brazil.  
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


## (2) Category & Product Insights  

<img width="1247" height="696" alt="Category_ _Product_Insights" src="https://github.com/user-attachments/assets/0faa282c-0af9-41a6-8d87-ce5f486b985f" />  

 **Product Popularity vs Sales Volume**
Top 3 product categories by total orders:  
Bed_Bath_Table  
Health_Beauty  
Sports_Leisure  
While "Bed_Bath_Table" had the highest number of orders, the top categories by total revenue (sales volume) are:  

Health_Beauty – $1,419,509.89  
Watches_Gifts – $1,269,684.96  
Bed_Bath_Table – $1,249,411.56  

This indicates that although Bed_Bath_Table is the most frequently ordered category, Health_Beauty and Watches_Gifts are more profitable, suggesting high-value purchases in those categories.  

**Average Order Value by Payment Type**
Credit Card is the most used and generates the highest average order value: $162.86 (30.12%)  
Other common methods:  
Boleto: $144.34 (26.69%)  
Debit Card: $140.35 (25.9%)  
Voucher: $93.24 (17.24%)  

#### Business Insights  
**High-Order Categories Aren’t Always High Revenue**
While Bed_Bath_Table, Health_Beauty, and Sports_Leisure have the highest number of orders, they don’t generate the most revenue. This indicates these are low-ticket, high-frequency categories.

**High-Value Categories Drive Revenue Despite Fewer Orders**
Categories like Computers and Small_Appliances have fewer orders but much higher average order values, contributing disproportionately to overall revenue.

**Credit Cards Are the Preferred Payment Method for High-Value Orders**
Credit cards not only lead in payment frequency but also result in the highest average order value, making them crucial for customer monetization.  

**Steady Year-on-Year Revenue Growth**
Total revenue has shown a sharp increase from 2016 to 2018, indicating successful customer acquisition, product diversification, and marketplace expansion.  

## (3) Customer Behavior & Loyalty  

<img width="1295" height="710" alt="Customer_Behavior_ _Loyalty" src="https://github.com/user-attachments/assets/9a38a375-12d2-4e98-9d6a-b57750091067" />  

**Low Customer Loyalty / Repeat Purchase Rate**
Only 2,979 customers (just 5.84% of total revenue) are repeat buyers, contributing around $0.90M in sales.  
Insight: The business is heavily dependent on new customers. There's a significant opportunity to build customer retention strategies like loyalty programs or personalized offers.  

**Average Product Rating is Strong**
The overall average rating is 4.09, suggesting good customer satisfaction.  
Insight: Maintain product/service quality and encourage more reviews to build trust with potential buyers. 
Based on the resulting visual shown above, the product with the highest sales amount has a rating of 4.21, which is above the overall average rating.

**Higher Ratings = Higher Revenue**
Products with ratings of 5 contribute the highest revenue ($8.88M) and most orders (56,817).  
Insight: Focus on products with high customer satisfaction for promotion and bundling. Use reviews as a signal to identify and scale successful products.  
  
**Low-Rated Products Still Have Sales**
Even 1-star products generated $1.81M in revenue from 9,381 orders, showing customers are still buying poorly rated products.
Insight: Investigate low-rated products that sell well — this might indicate mismatched expectations or misleading product listings.  

**Ratings Strongly Correlate With Revenue and Orders**
As customer review scores increase, so do order volume and revenue, seen in both the bar and scatter plots.  
Insight: Encourage satisfied customers to leave reviews; it clearly influences future customer behavior and revenue generation. 


## (4) Customer Location & Retention 

<img width="1254" height="694" alt="Customer_Location_ _Retention" src="https://github.com/user-attachments/assets/736267f6-8308-400f-ad67-268d9ee61db3" />  

**Urban Hubs Drive the Majority of Sales**
The highest customer density is observed in São Paulo, Rio de Janeiro, and Minas Gerais, accounting for a large portion of the total 99,441 customers over the 3-year period.
Insight: These major cities are key revenue drivers and should be targeted with efficient logistics, faster delivery, and location-based marketing campaigns to enhance the customer experience.  

**High Retention in Low-Density Regions**
States like Acre, Rondônia, and Mato Grosso have the highest customer retention rates, even though they are among the least populated in terms of customers.  
Insight: This suggests that customers in these less saturated regions are more loyal and satisfied. The company can study these regions to uncover what’s working (e.g., less competition, better delivery experience) and replicate the same strategy in other areas.  

**Retention Opportunities Through Regional Strategies**  
The overall retention rate is low (3%), indicating a need for focused efforts in customer loyalty programs, regional promotions, or even localized customer support.  

## (5) Seller Performance  

<img width="1283" height="704" alt="Seller_Performance" src="https://github.com/user-attachments/assets/39496cd1-b7e9-4c2f-bf34-20bebb98eca8" />  

**Active Seller Growth**: The number of active sellers steadily increased over time, reaching 2,970 sellers, indicating strong platform adoption.  
**Sales Not Solely Dependent on Ratings**: Sellers with ratings between 3.5–5 generally perform better, but some low-rated sellers still generate high revenue.  
**Top Sellers Drive Most Revenue**: A small group of sellers contributes disproportionately to total sales, reflecting a typical 80/20 revenue distribution.  
**Improvement Opportunity**: Many sellers have low ratings, highlighting a need for seller support programs to improve customer satisfaction and retention.  

## (6) Orders & Payments Analytics  

<img width="1251" height="693" alt="Order_ _Payment_Analytics" src="https://github.com/user-attachments/assets/59e47277-56fb-4a91-b8a5-bc3be2417210" />  

**Credit Card Dominates Payments**:  
Credit cards are the most popular payment method, used in over 75,000 orders, far surpassing other options like boleto and voucher.  
Indicates customer trust in credit systems and preference for postpaid purchases.  

**Payment Type vs Product Variety**:  
Products bought via credit cards span across the highest number of categories.  
Shows that credit cards offer flexibility and are preferred across a wide product range.  

**Geographical Payment Trends**:  
Sao Paulo, Rio de Janeiro, and Minas Gerais lead in total payment volume, with credit card again being the most used method.  
Regional preferences matter: for example, boleto is more commonly used in some other states.  

**Limited Use of Debit & Vouchers**:  
Very low usage of debit cards and vouchers suggests limited consumer behavior adoption or possible system limitations.  
Opportunity to promote or incentivize other payment methods. 


## (7) Order Cancellations Analysis  

<img width="1257" height="684" alt="Order_Cancellation_Analysis" src="https://github.com/user-attachments/assets/aba77d48-d338-4d8d-80d9-7e43a9be7123" />  

**Very Low Overall Cancellation Rate**:
The average order cancellation rate is just 0.63%, showing **strong operational efficiency and high customer trust**.

**High Ratings → Lower Cancellations**:
There’s a negative correlation between product ratings and cancellations—products with higher average ratings tend to have fewer cancellations.
This highlights the importance of **product quality and customer satisfaction**.

**Initial Spike in Cancellations (Oct 2016)**:
A sharp spike in cancellation rate occurred during **October 2016**, possibly due to platform onboarding issues or seasonal demand mismatch.

**Ratings Stabilize Over Time**:
From early 2017 onward, average product ratings hover around **4.0–4.5**, indicating **consistent customer satisfaction**.  

## (8) Profitability & Marketing  

<img width="1270" height="701" alt="Profitabillity_ _Marketing" src="https://github.com/user-attachments/assets/88372021-45ec-45b4-9e4d-3e9d759b8881" />  

**High Overall Profitability**:  
The overall Gross Profit Margin is 85.73%, indicating strong profitability across product categories.  

**Top-Performing Product Categories**:  
Computers lead with the highest profit margin (95.71%) and the highest average order value, making them the most lucrative category.  

**Other high-margin categories include**:  
Small Appliances (94.56%)  
Portable Kitchen & Food (93.04%)  
Agro Industry & Commerce (92.60%)  
Fixed Telephony (92.31%)  

**Marketing Focus Recommendation**:  
Focus marketing on categories with both high margins and high order value, such as:  

Computers  
Small Appliances (Home & Kitchen)  
Home Appliances 2  
Agro Industry & Commerce  

**Watch for Lower Margins**:  
Categories like Health & Beauty (86.87%) and Cool Stuff (86.90%) are at the lower end of the top 20, which may require cost or pricing adjustments. 


# Key Business Insights – Olist E-Commerce Store  

## Revenue & Sales Trends
Olist generated **$15.42** million in total revenue over 3 years.  
**Black Friday 2017** drove 16.66% of the year’s November revenue, reflecting strong promotional performance and seasonal buying behavior.  
Despite high order volume in some categories, high-ticket items (e.g., Computers) contributed more to total revenue, highlighting value over volume in revenue generation.  
The **Average Order Value (AOV)** stands at **$159.85**, suggesting customers often purchase mid to high-value products.  

## Fulfillment & Platform Performance
**97% delivery success rate** indicates a robust logistics and order fulfillment system.  
0.63% average order cancellation rate suggests strong customer satisfaction, though R$143K revenue was lost due to cancellations.  
Key factors behind cancellations include low product ratings and minimum pricing issues.  

## Customer Behavior & Retention
Repeat buyers contributed 5.84% to total revenue—small in number but valuable, pointing to potential for loyalty programs.  
Credit Cards are the dominant payment method, followed by Boletos. Debit cards are least used, likely due to limited acceptance and user preference.  
Ratings above average (4.09+) are correlated with high seller/product performance. However, a perfect 5 rating does not guarantee high sales, suggesting price sensitivity outweighs ratings.  

## Sellers & Category Insights
96% of sellers are active, indicating a healthy marketplace ecosystem and seller satisfaction.  
Revenue follows an 80/20 distribution, where a small group of sellers generate the majority of sales.  
Product category leadership changes annually, indicating a dynamic market and shifting customer preferences.  
Categories like Computers and Small Appliances showed both high gross profit margins (up to 95.71%) and top order values.  

## Geographic Insights
Top 3 customer density locations: São Paulo, Rio de Janeiro, Minas Gerais.  
Top 3 retention rate locations: Acre, Rondônia, Mato Grosso.  
Interestingly, Acre has the highest customer retention rate despite having one of the lowest customer volumes, showing potential in under-tapped markets.  
High-density areas also show above-average retention, suggesting scope to deepen engagement in large markets.  

## Profitability
Gross Profit Margin is 85.73%, indicating efficient cost management and strong pricing strategies.  
High-value product categories like Computers not only generate top revenue but also contribute significantly to overall profitability.  


# Recommendations  
Olist can drive further growth by implementing seasonal or quarterly promotional events similar to Black Friday, which have proven successful in boosting sales. Maintaining high product quality and competitive pricing will help reduce cancellations and enhance customer satisfaction. Introducing loyalty programs—such as exclusive discounts for repeat buyers and free shipping in key regions like São Paulo and Acre—can improve customer retention and attract new users. Given the platform’s strong revenue and high profit margins, Olist is also well-positioned to invest in expanding its product range and entering new markets to stay competitive and grow its customer base.  

# Conclusion  
In conclusion, Olist has established itself as a profitable and customer-centric e-commerce platform with strong sales performance, high customer satisfaction, and efficient   operations. By leveraging its strengths and implementing targeted strategies, Olist is well-positioned for sustained growth and market expansion in the Brazilian e-commerce landscape.  


<img width="360" height="217" alt="Thank you" src="https://github.com/user-attachments/assets/0ad5643f-26b7-414a-9c7b-0b84f52b6b9e" />

















  











