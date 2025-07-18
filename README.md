# My_DSA_Data_Analysis_Journey

## Table of Contents
- [Project Topic 1](#Project Topic 1)
- [Project Overview] (#Project Overview)


### Porfolio Building
**On Porfolio Building**

Here at DSA (Digital SKills Africa) was where I began to know and learn about portfolio building. Having had classes with DSA on data analysis. I have learnt to use analytic programmees like Excel, SQL (Structured Query Language) and the Power BI. It was fun learning and an insightful journey.

## Project Topic 1: Amazon Product Review Analysis

### Project Overview
In this project, I will be analysing product and customer review data to generate insight that can guide improvements, marketing strategies and customer engagements

### Data Sources
The primary source of data used here is the Amazon Case Study.xlsx and this data was provided me by the Incubator Hub facilitator. I believe it is an open source data that can be gotten for free from online sites that provides data. Sites such as kaggle, FRED etc


### Tools Used 
- Microsoft Excel for Data Cleaning [Download here](https://www.microsoft.com).
    - For Data Collection
    - For Data Cleaning
    - For Data Analysis

### Dataset Description
The dataset contains information scraped from Amazon product pages, including:
• Product details: name, category, price, discount, and ratings
• Customer engagement: user reviews, titles, and content
• Each row represents a unique product, with aggregated reviewer data stored as comma-separated values
Total Records: 1,465 rows
TotalFields: 16 columns

### Analysis Task
After cleaning the table and thorough transformation of different data types, With the help of the pivot table, charts and different FUNCTIONS, I was able to tackle problems. Some of them were
    1. Calculating the average discount percentage by product category?
    2. Calculating how many products are listed under each category?
    3. Calculating the total number of reviews per category?
    4. Calculating which products have the highest average ratings?
    5. Calculating the average actual price vs the discounted price by category?

    



## Project Topic 2: KUltra Mega Store Inventory

### Project Overview
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in offi ce supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria.

In this project, I was tasked with analyzing data, presenting key insight and findings e.g highest sales by product category, total sales of appliances, most shipping cost incurred by joining data. I was also able to join data which was used to calculate number of person who returned their product after that they had ordered.

All of these and more analysis wer ecarried out

### Data Sources
The primary source of data used here is the KMS SQL Case Study.csv & Order_Status.CSV and this data was provided me by the Incubator Hub team.  


### Tools Used 
- SQL Server Management Studio 20 [Download here]().
    - For Data Querying
    - For Data Integration
    - For Data Analysis

### Project Links
### *Excel*
[the Ogie Daniel Excel DSA Project.xlsx](https://github.com/user-attachments/files/21323534/the.Ogie.Daniel.Excel.DSA.Project.xlsx)

[Uploading tcreate database [Ogie Daniel DSA project.db]
``` SQL

---IMPORTING KMS FILE--------

SELECT *
FROM [KMS Sql Case Study]
  
------1. Highest Salary in product category-------- 
SELECT MAX(Sales) AS [Highest Sales]
FROM [KMS Sql Case Study]
 
 -----2. top 3 and bottom 3 regions in term of sales-----
 --- TOP 3 regions -------
SELECT TOP 3 Region, Sales
FROM [KMS Sql Case Study]
ORDER BY Sales DESC 

------ Bottom 3 regions
SELECT TOP 3 Region, Sales
FROM [KMS Sql Case Study]
ORDER BY Sales ASC

ALTER TABLE [KMS Sql Case Study]
ALTER COLUMN sales DECIMAL(10,2)


SELECT *
FROM [KMS Sql Case Study]

----3. Total Sales of Appliances in Ontario-----
SELECT Province, SUM(sales) AS Total_Sales
FROM [KMS Sql Case Study]
WHERE Province = 'Ontario'
GROUP BY Province

-----4. Advising KMS Managment on bottom 10 customer-------
------ Bottom 10 customer based on revenue ----
SELECT TOP 10 Sales, Customer_Name, Order_Date, Unit_Price, Order_Quantity, Shipping_Cost, Discount, Profit, Ship_Mode, Region
FROM [KMS Sql Case Study]
ORDER BY Sales ASC
 
 ---- Top 10 customer based on revenue---------
SELECT TOP 10 Sales, Customer_Name, Order_Date, Unit_Price, Order_Quantity, Shipping_Cost, Discount, Profit, Ship_Mode, Region
FROM [KMS Sql Case Study]
ORDER BY Sales DESC

------ Advising KMS bottom 10 customer based on revenue--------
--- One of the thing highly noticeable when comparing between top customers and bottom customers is the fact that,
--- top customer ordered more quantity of products with their unit_price relatively higher (in unit-price of thousands) compared to the bottom customers.
---- So bottom cucstomers are advised order high quantity of products, the lower the unit-price, the more the product 

----5. Most shipping cost incurred-----
SELECT Ship_Mode, SUM(Shipping_Cost) AS Shipping_Cost
FROM [KMS Sql Case Study]
GROUP BY Ship_Mode
ORDER BY Shipping_Cost DESC

--- KMS Inventory incurres the most shipping_cost by 'delievery truck'

SELECT *
FROM [KMS Sql Case Study]

----6. Most Valuable Customers ------
SELECT TOP 20 Sales, Customer_Name, Unit_Price, Order_Quantity, Profit, Product_Category
FROM [KMS Sql Case Study]
ORDER BY Sales DESC
---- Most valuable customers are "Emily Phan, Jasper Cacioppo,Craig Carreira, Dennis Kane, Karen Carlisle, Steve Chapman, Nick Crebassa, 
---- Parhena Norris, Deborah Brumfield, Valerie Takahito, Andy Reiter, Sally Matthias, Seth Vernon, Logan Haushalter, Raymond Book, Tony Chapman, Eleni McCrary, Julia West, Dean Percer, Rick Wilson
---- And Products they typically purcahse are under the category of "Technology" or "Furniture"

----7. Small Business Customer with highest Sales
SELECT TOP 10 Customer_Name, Sales, Customer_Segment
FROM [KMS Sql Case Study]
WHERE Customer_Segment = 'Small Business'
ORDER BY sales DESC

----8. Corporate Customer placed the most order in 2009 -2012
SELECT TOP 5 Customer_Name, COUNT(order_id) AS Total_ID
FROM [KMS Sql Case Study]
WHERE Order_Date BETWEEN '2009-01-01' AND '2012-12-31'
		AND Customer_Segment = 'Corporate'
GROUP BY Customer_Name
ORDER BY Total_ID DESC

-----10. Most profitable consumer customer---
SELECT TOP 5 Customer_Name, SUM(profit) AS Most_Profitable_Consumer
FROM [KMS Sql Case Study]
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name
ORDER BY Most_Profitable_Consumer DESC

------ 
SELECT Ship_Mode, COUNT(Order_Quantity) AS Ct_Order_Quantity
FROM [KMS Sql Case Study]
WHERE Order_Priority = 'High'
GROUP BY Ship_Mode
ORDER BY Ct_Order_Quantity DESC

--- Ideally from information gotten from the datas provided, the company did not basically spend shipping cost based on order priority---
--- By order priority, we see that the highest shipping ,method used by order priority is "Regular" of which its margin is far behind both "Delivery Truck" & " Express Air"
---- Shipping cost may have been spent on different shipping method by other factors but not based on order quantity. 


---- IMPORTING ORDER STATUS-----
--- imported ---

SELECT *
FROM Order_Status

SELECT *
FROM [KMS Sql Case Study]

SELECT [KMS Sql Case Study].Order_ID, [KMS Sql Case Study].Order_Date, 
		[KMS Sql Case Study].Customer_Name, [KMS Sql Case Study].Customer_Segment, 
		Order_Status.Order_ID, Order_Status.Status
FROM [KMS Sql Case Study]
JOIN Order_Status
ON [KMS Sql Case Study].Order_ID = Order_Status.Order_ID

----- 10. Customer Returned Item, what segment did they belong to----

SELECT Customer_Segment, COUNT( DISTINCT Customer_Name) AS Customer_Returned_Item
FROM [KMS Sql Case Study]
JOIN Order_Status
ON [KMS Sql Case Study].Order_ID = Order_Status.Order_ID
GROUP BY Customer_Segment

----- Customer Returned Item = 419, Segment = "Corporate", "Home Office", "Consumer", "Small Business"he Ogie Daniel DSA SQL project 1.sql…]()




  
