# Capstone_Project
This project analyzes Sales and Customer Data to uncover insights for better business decisions. Key tasks include data cleaning, exploration, and visualization of sales trends and customer segments. Using Excel, SQL, and Power BI, it provides a clear view of essential metrics to boost business intelligence.

### Project Title: Capstone Project 
### Project Overview
 This Capstone project analyzes Sales and Customer Data to uncover insights for better business decisions. Key tasks include data cleaning, exploration, and visualization of sales trends and customer segments. Using Excel, SQL, and Power BI, it provides a clear view of essential metrics to boost business intelligence.

 ### Data Sources
The primary source of Data used here is Sales Data and Customer Data, this was easily downloaded from the file that LITA provided via my Learning Management System (LMS) platform.

 ### Tools Used
 - Microsoft Excel [Download Here](https://canvas.instructure.com/files/273182802/download?download_frd=1)
   1. Data cleaning, analysis, and basic visualization
 - SQL- Structured Query Language: Data querying and manipulation
 - Power BI: Dashboard creation and advanced visualization
 - GitHub: Portfolio and project management
 - Canvas: Project assignments and submissions

### Data Cleaning and Preparation
In the initial phase of data preparation, I:
- Loaded the data for inspection.
- Removed blanks and handled missing values.
- Removed duplicates to ensure data accuracy.
- Converted files to CSV format for SQL upload

### Exploratory Data Analysis 
EDA involved exploring the Data to answer some questions about the provided Data such as the following  [Download Here](https://canvas.instructure.com/files/273182738/download?download_frd=1)
- Use pivot tables to summarize total sales by product, region, and month.
- Use Excel formulas to calculate metrics such as average sales per product and total revenue by region
- Write queries to retrieve the total sales for each product category
- Create a dashboard that visualizes the insights found in Excel and SQL

### Data Analysis
This is where we include some basic lines of code, queries and DAX expressions used during my analysis
Excel

```Create Database Capstone_Project```

```Select * From [dbo].[CAPSalesData]```

----Retrieve the total sales for each product category----
```SELECT Product, SUM(Total_Sales) AS TotalSales
FROM [dbo].[CAPSalesData]
GROUP BY Product```


---Number of sales transactions in each region---
```Select Region, Count(OrderID) As Number_Of_Sales_Transaction
From [dbo].[CAPSalesData]
Group by Region```


----Highest-selling product by total sales value---
```Select MAX(Product) As Product, MAX(Total_Sales) As Highest_Selling_Product 
From [dbo].[CAPSalesData]```


----Total revenue per product-----
```SELECT Product, SUM(Revenue) AS TotalRevenue
FROM [dbo].[CAPSalesData]
GROUP BY Product```


----Calculate monthly sales totals for the current year-----
```SELECT * FROM [dbo].[CAPSalesData] WHERE Year(OrderDate) = 2024```

```SELECT MONTH(OrderDate) AS month FROM [dbo].[CAPSalesData]
 WHERE Year(OrderDate) = 2024```

```Select MONTH(OrderDate) AS Month, SUM(Total_Sales) AS MonthlySalesTotal
FROM [dbo].[CAPSalesData]
WHERE YEAR(OrderDate) = 2024
GROUP BY MONTH(OrderDate)
ORDER BY Month```


---top 5 customers by total purchase amount---
```Select TOP 5 Customer_Id, SUM(Quantity*UnitPrice) AS TotalPurchaseAmount
From [dbo].[CAPSalesData]
Group By Customer_Id 
Order By TotalPurchaseAmount Desc```

----calculate the percentage of total sales contributed by each region---
```WITH Total_Sales AS (
    SELECT SUM(Quantity * UnitPrice) AS TotalSalesAmount
    FROM [dbo].[CAPSalesData]
)
SELECT Region,
    SUM(Quantity * UnitPrice) AS RegionSales,
    (SUM(Quantity * UnitPrice) * 1.0 / (SELECT TotalSalesAmount FROM TotalSales) * 100) AS SalesPercentage
FROM [dbo].[CAPSalesData]
GROUP BY Region```

---Identify products with no sales in the last quarter----
```Select Distinct Product 
from [dbo].[CAPSalesData]
Where Product NOT IN(
Select Product from [dbo].[CAPSalesData]
where OrderDate >= DateAdd(quarter,-1, GetDate()) and OrderDate < GetDate())```

