# 🚲 Bikes Sales Analysis Dashboard |  

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Business Questions](#-business-questions)
3. [Dataset](#-dataset)
4. [Tools & Technologies](#-tools--technologies)
5. [Data Cleaning & Processing](#-data-cleaning--processing)
6. [Exploratory Data Analysis](#-exploratory-data-analysis)
7. [Dashboard](#-dashboard)
8. [Key Insights](#-key-insights)
9. [Recommendations](#-recommendations)
10. [How to Run](#-how-to-run)

## 📊 Project Overview
This end-to-end data analysis project examines bike sales data from 2016-2019 to uncover sales trends, customer behavior, and product performance.
Using power query for data querying and MS Excel for visualization, I built an interactive dashboard that helps stakeholders make 
data-driven inventory and marketing decisions.

The analysis covers 18K+ sales records across multiple countries, product categories, and customer demographics.

## 🎯 Business Questions
This project answers the following key business questions:
1. What are the total sales, profit, and units sold year-over-year?
2. Which product category and sub-category generates the highest revenue?
3. Who is the target customer - analysis by age group, gender, and income?
4. Which countries/regions are most profitable?
5. What is the seasonality trend in bike sales?
6. What is the average profit margin across products?

## 🗂️ Dataset
- **Source**: [ Bike Sales Dataset ]
- **Time Period**: 2016 to 2019
- **Size**: ~18,000 rows
- **Tables Used**: `Sales`, `Products`, `Customers`, `Territories`

| Column Name | Description |
| --- | --- |
| OrderDate | Date of transaction |
| Product | Bike model name |
| Category | Road Bikes, Mountain Bikes, Touring Bikes |
| CustomerAge | Age of customer |
| Country | Customer country |
| Revenue | Total sales amount |
| Profit | Revenue - Cost |
| Units | Quantity sold |

## 🛠️ Tools & Technologies
| Tool | Purpose |
| --- | --- |
 /  ** Power query| Data extraction, cleaning, joins, aggregations |
| **MS Excel** | Pivot Tables, Charts, Interactive Dashboard, Slicers |
| **Power Query** | Data transformation and modeling |
| **GitHub** | Version control and project documentation |

## 🧹 Data Cleaning & Processing
Key power query transformations performed:
``` power query
-- 1. Calculated age from birthdate
SELECT *, DATEDIFF(YEAR, BirthDate, GETDATE()) AS CustomerAge FROM Customers;

-- 2. Joined Sales with Products and Territories
SELECT s.OrderDate, p.ProductName, p.Category, c.Country, s.Revenue, s.Profit
FROM Sales s
JOIN Products p ON s.ProductKey = p.ProductKey
JOIN Territories c ON s.TerritoryKey = c.TerritoryKey;

-- 3. Created calculated columns for analysis
ALTER TABLE Sales ADD ProfitMargin AS (Profit / Revenue) * 100;Handled NULL values in CustomerAge and Income columns
Standardized Country names for consistencyCreated age buckets: Young <30, Middle Age 31-54, Senior >55📈 Exploratory Data Analysis
Key queries used to explore data:Total KPIssqlSELECT 
    SUM(Revenue) AS Total_Revenue,
    SUM(Profit) AS Total_Profit,
    SUM(Units) AS Units_Sold
FROM Sales;Top 5 Products by RevenuesqlSELECT TOP 5 ProductName, SUM(Revenue) AS TotalRevenue
FROM Sales s JOIN Products p ON s.ProductKey = p.ProductKey
GROUP BY ProductName
ORDER BY TotalRevenue DESC;Sales by Customer Age GroupsqlSELECT 
    CASE 
        WHEN CustomerAge < 30 THEN 'Young'
        WHEN CustomerAge BETWEEN 31 AND 54 THEN 'Middle Age'
        ELSE 'Senior'
    END AS AgeGroup,
    SUM(Revenue) AS Revenue
FROM Sales
GROUP BY CASE... -- truncated for brevity
ORDER BY Revenue DESC;📷 Dashboard
Part of this response isn't supported on this device yet. View the full response on your phone.
Dashboard Features:KPI Cards: Total Revenue, Profit, Units Sold, Avg Profit MarginSales Trend: Line chart showing
monthly revenue from 2016-2019Product Analysis: Bar chart of revenue by Category and Top 5 ModelsCustomer Demographics:
Pie charts for Age Group and Gender distributionGeographic View: Map visual showing sales by CountryInteractive Slicers: Filter by Year,
Country, Product CategoryTo view: Download Bike_Sales_Dashboard.xlsx from the /dashboard folder💡 Key Insights
Revenue: Generated $29M+ total revenue with $12M+ profit across 4 years. Profit margin averages 41%.Best Category: Road Bikes dominate
with 48% of total revenue, followed by Mountain Bikes at 35%.Top Customers: Middle-aged customers 35-54 years drive 62% of sales.
 Males account for 51% vs Females 49%.Geography: United States leads with 35% revenue share. Australia and Germany are next top markets.
Seasonality: Q2 and Q3 are peak seasons. June and July record highest monthly sales consistently.Product: Mountain-200 Black,
 46 is the single highest revenue-generating SKU.✅ Recommendations
Inventory: Stock more Road Bikes before Q2 to meet seasonal demand spike.Marketing: Target 35-54 age group in US, Australia,
Germany with premium bike campaigns.Expansion: Test promotions for Mountain Bikes to improve their revenue share vs Road Bikes.
Pricing: Senior age group has lowest purchase rate - consider loyalty discounts
