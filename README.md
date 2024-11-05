# Capstone_Project
This project analyzes Sales and Customer Data to uncover insights for better business decisions. Key tasks include data cleaning, exploration, and visualization of sales trends and customer segments. Using Excel, SQL, and Power BI, it provides a clear view of essential metrics to boost business intelligence.

### Project Title: Capstone Project 

### Outline

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and Preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis for Sales Data](#data-analysis-for-sales-data)

[Insights from Sales Data Analysis](#insights-from-sales-data-analysis)

[Recommendations](#recommendations)





### Project Overview
---
 This Capstone project analyzes Sales and Customer Data to uncover insights for better business decisions. Key tasks include data cleaning, exploration, and visualization of sales trends and customer segments. Using Excel, SQL, and Power BI, it provides a clear view of essential metrics to boost business intelligence.

 ### Data Sources
 ---
The primary source of Data used here is Sales Data and Customer Data, this was easily downloaded from the file that LITA provided via my Learning Management System (LMS) platform.

 ### Tools Used
 ---
 - Microsoft Excel [Download Here](https://canvas.instructure.com/files/273182802/download?download_frd=1)
   1. Data cleaning, analysis, and basic visualization
 - SQL- Structured Query Language: Data querying and manipulation
 - Power BI: Dashboard creation and advanced visualization
 - GitHub: Portfolio and project management
 - Canvas: Project assignments and submissions

### Data Cleaning and Preparation
---
In the initial phase of data preparation, I:
- Loaded the data for inspection.
- Removed blanks and handled missing values.
- Removed duplicates to ensure data accuracy.
- Converted files to CSV format for SQL upload

## Project 1: Sales Data

### Exploratory Data Analysis 
---
EDA involved exploring the Data to answer some questions about the provided Data such as the following  [Download Here](https://canvas.instructure.com/files/273182738/download?download_frd=1)
- Use pivot tables to summarize total sales by product, region, and month.
- Use Excel formulas to calculate metrics such as average sales per product and total revenue by region
- Write queries to retrieve the total sales for each product category
- Create a dashboard that visualizes the insights found in Excel and SQL

### Data Analysis for Sales Data
---
This is where we include some basic lines of code, queries and DAX expressions used during my analysis

#### Excel 
For data cleaning and analysis, I used Excel formulas and pivot tables. Here are a few examples:

- Data Cleaning: Using =TRIM(), =CLEAN(), and REMOVEDUPLICATES to remove inconsistencies and handle errors in the data.
- Analysis: Creating pivot tables to summarize and segment data, and using =SUM, =AVERAGEIF(), and =COUNTIF() functions for conditional calculations.

#### Calculating in Excel for Sales Data
- Generating Total Sales and Average Sales per Product (=F2*G2) and AVERAGEIF(C:C,C:C,H:H)

![Sales Data Table (Total Sales)](https://github.com/user-attachments/assets/7f7636ad-0c6f-4b26-a871-c5cbdfbc3bbf)


- Using pivot Table to generate
![Sales Data (Pivot Table)](https://github.com/user-attachments/assets/52016e7b-9b1d-4376-ae69-760cfc8bfe4d)

- Using a Chart to Visualize the Sales Data
![Sales Data (Chart)](https://github.com/user-attachments/assets/6b3b6166-e56a-415a-b9b1-3430fa34d04c)

#### SQL Queries for Sales Data
A variety of SQL queries were created to analyze and structure data, all documented below.

 ```Create
Database Capstone_Project
```
   
 ```Select *
From [dbo].[CAPSalesData]
```

 ```SELECT Product, SUM(Total_Sales) AS TotalSales
FROM [dbo].[CAPSalesData] GROUP BY Product
```

 ```Select Region,
 Count(OrderID) As Number_Of_Sales_Transaction
From [dbo].[CAPSalesData] Group by Region
```

 ```Select MAX(Product) As Product, 
 MAX(Total_Sales) As Highest_Selling_Product
From [dbo].[CAPSalesData]
```

 ```SELECT Product, SUM(Revenue) AS TotalRevenue 
 FROM [dbo].[CAPSalesData] GROUP BY Product
```

```SELECT * FROM [dbo].[CAPSalesData] 
WHERE Year(OrderDate) = 2024
```

```SELECT MONTH(OrderDate) AS month FROM [dbo].[CAPSalesData] 
WHERE Year(OrderDate) = 2024
```

```Select MONTH(OrderDate) AS Month, SUM(Total_Sales) AS MonthlySalesTotal 
FROM [dbo].[CAPSalesData] WHERE YEAR(OrderDate) = 2024 GROUP BY MONTH(OrderDate)
ORDER BY Month
```


```Select TOP 5 Customer_Id, SUM(Quantity*UnitPrice) AS TotalPurchaseAmount 
From [dbo].[CAPSalesData] Group By Customer_Id
Order By TotalPurchaseAmount Desc
```

 ```WITH Total_Sales AS ( SELECT SUM(Quantity * UnitPrice) AS TotalSalesAmount 
 FROM [dbo].[CAPSalesData]) SELECT Region, SUM(Quantity * UnitPrice) AS RegionSales,
(SUM(Quantity * UnitPrice) * 1.0 / (SELECT TotalSalesAmount FROM TotalSales) * 100) AS SalesPercentage
FROM [dbo].[CAPSalesData] GROUP BY Region
```

```Select Distinct Product from [dbo].[CAPSalesData] 
Where Product NOT IN( Select Product from [dbo].[CAPSalesData]
where OrderDate >= DateAdd(quarter,-1, GetDate()) and OrderDate < GetDate())
```

#### SQL Visuals
![SQL Sales Data Query](https://github.com/user-attachments/assets/899efb9a-16fc-4f77-90ab-e3f66e396dbb)

![SQL Sales Data Query 3](https://github.com/user-attachments/assets/3d2eee72-3eee-4728-92ef-fca76c04a4bd)
![SQL Sales Data Query 2](https://github.com/user-attachments/assets/598342da-bd32-42fc-8770-fc7210463223)



#### PowerBi for Sales Data
In Power BI, I used DAX expressions to create calculated fields and measures for visualization. Examples include:

Sales Calculation:
- Total Sales = SUM(Sales[Amount])
- Highest Selling Product = Max(SalesData[Product])
- Total Purchase Amount = (SalesData[Quantity]*SalesData[UnitPrice])
- Montly Sales 2024 = CALCULATE(SUM('SalesData'[Total Sales]),
    YEAR('SalesData'[OrderDate]) = YEAR(2024),
    VALUES('SalesData'[OrderDate]))

These tools and expressions helped in building a dynamic dashboard to visualize trends and insights.

#### Data Visualization

![Sales Data Visualization 1](https://github.com/user-attachments/assets/9b9eb44c-f198-474d-9353-62b9258a867f)

![Sales Data Visualization 2](https://github.com/user-attachments/assets/1d201087-e0d4-48e1-b747-5c1665b165f6)

### Insights from Sales Data Analysis
---
- Total Sales Performance:
 1. The total revenue from all regions amounts to 2.1 million.
 2. The overall sales figures indicate a healthy sales volume, with a total of 2 million in sales recorded.

- Revenue by Region:
1. South: $927,820
2. East: $485,925
3. North: $387,000
4. West: $300,345
5. The South region has the highest revenue, contributing significantly to the overall sales, while the West has the lowest.

- Total Sales by Product:
1. Shoes: $613,380
2. Shirt: $485,600
3. Hat: $316,195
4. Gloves: $296,900
5. Jacket: $208,230
6. Socks: $180,785
7. Shoes are the best-selling product, significantly outperforming others, with shirts also showing strong sales.

- Sales Transactions by Region:
  Sales transactions are distributed evenly across regions, with each contributing approximately 25% of the total transactions.
  
- Highest-Selling Product:
The highest-selling product by total sales value is Socks, with 600 units sold.

- Trends and Opportunities:
1. The strong performance of shoes suggests a potential focus for marketing efforts or promotions.
2. The lower sales in the West may indicate an opportunity for targeted sales strategies or increased promotional activities in that region.

### Recommendations
---
Consider implementing targeted marketing campaigns in the West region to boost sales.
Leverage the strong sales of shoes and shirts by introducing related accessories or seasonal promotions to enhance revenue further.
Regularly analyze sales data to track trends and adjust strategies accordingly.
These insights provide a comprehensive overview of the sales performance and highlight areas for potential growth and focus.

## Project 2: Customer Data

### Exploratory Data Analysis 
---
EDA involved exploring the Data to answer some questions about the provided Data such as the following  [Download Here](https://canvas.instructure.com/files/273182738/download?download_frd=1)
- Use pivot tables to find subscription patterns
-  average subscription duration and identify the most popular subscription types
- Write queries to extract key insights in customer data
- Create a dashboard that visualizes the insights found in Excel and SQL

### Data Analysis for Customer Data
---
This is where we include some basic lines of code, queries and DAX expressions used during my analysis

#### Excel 
For data cleaning and analysis, I used Excel formulas and pivot tables. Here are a few examples:

- Data Cleaning: Using =TRIM(), =CLEAN(), and REMOVEDUPLICATES to remove inconsistencies and handle errors in the data.
- Analysis: Creating pivot tables to summarize and
- 
#### Calculating in Excel for Customer Data
- Generating average subscription duration (=F2-E2)
  
  ![Customer Data (Subcription Duration)](https://github.com/user-attachments/assets/e6d7e06a-334b-4b55-92e6-a8d5bed10083)


- Using pivot Table to generate Subscription pattern in Customer Data




- Using a Chart to Visualize the Customer Data
  
#### SQL Queries for Customer Data
A variety of SQL queries were created to analyze and structure data, all documented below.







