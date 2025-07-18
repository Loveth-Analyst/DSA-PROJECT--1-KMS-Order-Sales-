# DSA-PROJECT 1(KMS Order Sales)

🗃 KMS Inventory Data Analysis with SQL

This repository contains a SQL-based data analysis project on the KMS Inventory Dataset, focused on uncovering business insights from inventory, sales, customer, and shipping records.

 ## Company Overview
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and
furniture. Its customer base includes individual consumers, small businesses (retail), and
large corporate clients (wholesale) across Lagos, Nigeria.

 ## Project Objective
As a Business Intelligence Analyst to support the Abuja division of KMS.I analyze the KMS inventory and sales database with Excel file containing order data from 2009 to 2012 to answer key business questions, identify trends, detect inefficiencies, and support data-driven decision-making.

-- Kultra Mega Stores Inventory key objectives
1. Which product category had the highest sales?
2. What are the Top 3 and Bottom 3 regions in terms of sales?
3. What were the total sales of appliances in Ontario?
4. Advise the management of KMS on what to do to increase the revenue from the bottom
10 customers
5. KMS incurred the most shipping cost using which shipping method?
6. Who are the most valuable customers, and what products or services do they typically
purchase?
7. Which small business customer had the highest sales?
8. Which Corporate Customer placed the most number of orders in 2009 – 2012?
9. Which consumer customer was the most profitable one?
10. Which customer returned items, and what segment do they belong to?
11. If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer

## Tools & Technologies

Microsoft SQL Server 

SQL (Joins,  Aggregations, queries)

## Dataset Description

The project uses multiple tables, including:

orders – order details

customers – customer information and segments

inventory – product stock levels

sales – transaction records

shipping – delivery method and cost

returns – returned items etc

## Analysis Queries 
select *
from [KMS]

--- Which product category that has the highest 

select top 1 [Product_Category],count ([Product_Category])as [Product Count]
from [KMS]
group by Product_Category
order by [Product Count] desc


--- what are the top 3 and buttom 3 region in terms of sales 

select top 3 [Region],sum([sales]) as [Total Sales]
from [KMS]
group by Region
order by [Total Sales] desc

select top 3 [Region],sum([sales]) as [Total Sales]
from [KMS]
group by Region
order by [Total Sales] asc

----- what were  the Total Sales of applicants in ontario?

select Region, SUM(sales) as [Total Sales]
from [KMS]
where Region='ontario'
Group by Region

--------Advice the management of KMS on what to do to increase the revenue from the buttom 10 customer 

Select top 10 [Customer_Name], SUM([Sales]) as [Total Sales]
from [KMS]
group by Customer_Name
order by [Total Sales] asc

------KMS incurred the Most shipping cost using which shipping method ?

Select Top 1 [Ship_Mode], SUM([Shipping_Cost]) as [Total Shipping Cost]
from [KMS]
group by Ship_Mode
order by [Total Shipping Cost] desc

----Who are the most valuable customer, and what products or services did they typically purchase?

select [Customer_Name],Product_Name, SUM(sales) as [Total Sales]
from [KMS]
Group by Customer_Name,Product_Name
order by [Total Sales] desc

-----Which small business customer have the highest sales ?

select top 1 Customer_Name,Customer_Segment, SUM([Sales]) as [Total Sales]
from [KMS]
where Customer_Segment ='small Business'
group by Customer_Name,Customer_Segment
order by [Total Sales] desc

---Which corporate customer placed the most number of orders in 2019 -2012?

select top 1  Customer_Name,Customer_Segment, count([Order_ID]) as [Total order]
from [KMS]
where Customer_Segment ='corporate' and Order_Date between '2009' and '2012'
group by Customer_Name,Customer_Segment
order by [Total order] desc

---  Which consumer customer was the most profitable one?

select top 1 Customer_Name,Customer_Segment, sum([Profit]) as [Total profit]
from [KMS]
where Customer_Segment ='Consumer'
group by Customer_Name,Customer_Segment
order by [Total profit] desc

----Which customer returned items, and what segments do they belong to?
select Customer_Name,Customer_Segment,[Status]
from [KMS]
join [dbo].[Order_Status]
on [KMS].Order_ID = [dbo].[Order_Status].[Order_ID]

/* If the delivery truck is the most economical but the lowest shipping method and express air is the fastest.
but the most expensive one, did you think the company appropriately spent shipping costs based on the order priority */

Select Order_Priority, Ship_Mode,
    COUNT([Order_ID]) AS [order count],
    SUM(sales - profit) AS [Estimated shipping cost],
    AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg ship date]
from  [KMS] 
group by Order_Priority,Ship_Mode
order by  Order_Priority,Ship_Mode desc       
     
/* No, KMS did not appropriately spend shipping costs based on the order of  priority.
They overused delivery trucks, which are best for bulk or non-urgent orders and 
underused express air, which is meant for urgent deliveries. 
This shows a misalignment between shipping cost,speed and order priority leading to inefficient spending and wasted cost .*/


select Customer_Segment, SUM(sales) as [total sales]
from [KMS]
group by Customer_Segment
order by [total sales] desc


select *
from [KMS Sql Case Study1]


--- Which product category that has the highest 

select top 1 [Product_Category],count ([Product_Category])as [Product Count]
from [KMS]
group by Product_Category
order by [Product Count] desc


--- what are the top 3 and buttom 3 region in terms of sales 

select top 3 [Region],sum([sales]) as [Total Sales]
from [KMS]
group by Region
order by [Total Sales] desc

select top 3 [Region],sum([sales]) as [Total Sales]
from [KMS]
group by Region
order by [Total Sales] asc

----- what were  the Total Sales of applicants in ontario?

select Region, SUM(sales) as [Total Sales]
from [KMS]
where Region='ontario'
Group by Region

--------Advice the management of KMS on what to do to increase the revenue from the buttom 10 customer 

Select top 10 [Customer_Name], SUM([Sales]) as [Total Sales]
from [KMS]
group by Customer_Name
order by [Total Sales] asc
/* To boost sales from the bottom 10 customers, the company should focus on strengthening relationships 
through customized promotions, puchasing behaviours, Reaching out directly through calls or emails to their customers to understand their past experience,
Give discounts on their most viewed or previously purchased products, Upsell and Cross-sell Offers,
Offer faster delivery, better after-sales support, or dedicated account managers for small businesses and  Survey to Understand 
the Needs of the customers, what would make them again and why they havent been coming frequently*/

------KMS incurred the Most shipping cost using which shipping method ?

Select Top 1 [Ship_Mode], SUM([Shipping_Cost]) as [Total Shipping Cost]
from [KMS]
group by Ship_Mode
order by [Total Shipping Cost] desc

----Who are the most valuable customer, and what products or services did they typically purchase?

select [Customer_Name],Product_Name, SUM(sales) as [Total Sales]
from [KMS]
Group by Customer_Name,Product_Name
order by [Total Sales] desc

-----Which small business customer have the highest sales ?

select top 1 Customer_Name,Customer_Segment, SUM([Sales]) as [Total Sales]
from [KMS]
where Customer_Segment ='small Business'
group by Customer_Name,Customer_Segment
order by [Total Sales] desc

---Which corporate customer placed the most number of orders in 2019 -2012?

select top 1  Customer_Name,Customer_Segment, count([Order_ID]) as [Total order]
from [KMS]
where Customer_Segment ='corporate' and Order_Date between '2009' and '2012'
group by Customer_Name,Customer_Segment
order by [Total order] desc

---  Which consumer customer was the most profitable one?

select top 1 Customer_Name,Customer_Segment, sum([Profit]) as [Total profit]
from [KMS]
where Customer_Segment ='Consumer'
group by Customer_Name,Customer_Segment
order by [Total profit] desc

----Which customer returned items, and what segments do they belong to?
select Customer_Name,Customer_Segment,[Status]
from [KMS]
join [dbo].[Order_Status]
on [KMS].Order_ID = [dbo].[Order_Status].[Order_ID]

/* If the delivery truck is the most economical but the lowest shipping method and express air is the fastest.
but the most expensive one, did you think the company appropriately spent shipping costs based on the order priority */

Select Order_Priority, Ship_Mode,
    COUNT([Order_ID]) AS [order count],
    SUM(sales - profit) AS [Estimated shipping cost],
    AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg ship date]
from  [KMS] 
group by Order_Priority,Ship_Mode
order by  Order_Priority,Ship_Mode desc

## Key Analysis Performed

Identified top-selling and low-performing products

Analyzed returned items by customer and segment

Investigated shipping costs vs. delivery speed

Evaluated revenue contribution by region and order priority

Joined multiple tables to track full order lifecycle


## Business Insights

Express Air is the fastest but most expensive shipping method

Delivery Truck is the most economical but slowest

Certain customers consistently return products – further investigation is recommended

Bottom 10 customers generate the least revenue – targeted marketing may help

Order priority influences shipping method choice and cost efficiency


## Reflection

This project strengthened my ability to write complex SQL queries, join large tables, and interpret business insights from structured datasets.
