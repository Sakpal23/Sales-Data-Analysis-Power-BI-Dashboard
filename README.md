# Sales-Data-Analysis-Power-BI-Dashboard
A 5-page Power BI report that shows how sales, profit and units sold change over time, which products and cities perform best, and how promotions affect discounts. It also lets you compare two date ranges side by side.
Sales Overview

What you can find out
Which products sell the most and the least
Which products make the most and the least profit
Which cities bring in the most sales
Which promotions give the biggest average discount
How a period compares with another period


Report pages
#	Page	What it shows
1	Sales Overview	Top 5 and bottom 5 products by sales, profit and quantity
2	Region-Wise Sales Analysis	Sales trend over time, sales by city (map), number of orders, profit vs net sales, average discount by promotion
3	Comparison Sales-Profit-Quantity	Two date filters and side-by-side bars for sales, profit and quantity
4	Edit Interaction	Two date sliders, each controlling only its own set of visuals
5	Table Visual	Order-level table with slicers for date, customer, product and promotion

Screenshots
Region-Wise Sales	Comparison
Region	Comparison
Edit Interaction	Table Visual
Edit Interaction	Table
Data model

Data model

Star schema: one Fact_Table linked to Dim Customers, Dim Product and Dim Promotion (one-to-many).
Two date tables:
Date_Table1 is the active relationship.
Date_Table2 is inactive (dotted line) and is used only inside DAX with USERELATIONSHIP. This powers the date comparison.
Measures Table: holds all DAX measures.


Data preparation (Power Query)
Removed null values
Merged queries to combine data from different sources
Other cleaning and shaping steps to prepare the model
DAX measures
Measure	Purpose
Sum_Dim	Total net sales
Sum_Of_Net_Sales	Net sales for the second date range
Total_Profit	Profit for the second date range
Quantity_Sold	Units sold for the second date range

The last three use ALL(Date_Table1) and USERELATIONSHIP so the second date filter works independently. Full code is in dax/measures.md.

Quick findings
The report covers about 3.51K orders from 2020 to 2024.
Apple iPhone 14 and Apple MacBook Air lead on sales and profit.
Tupperware Lunch Box, L'Oreal Shampoo and Colgate Toothpaste are at the bottom on sales.
Summer Sale has the highest average discount among promotions.
Sales are spread across many Indian cities, with large bubbles in the big metros.
Tools

Power BI Desktop | Power Query | DAX | Data modelling

Repository structure
sales-data-analysis-powerbi/
├── SalesDataAnalysis.pbix      <- add your report file here
├── README.md
├── dax/
│   └── measures.md
├── presentation/
│   └── Sales_Data_Analysis_PowerBI.pptx
└── screenshots/
    ├── 00_data_model.png
    ├── 01_sales_overview.png
    ├── 02_region_wise_sales.png
    ├── 03_comparison.png
    ├── 04_edit_interaction.png
    └── 05_table_visual.png
How to open
Install Power BI Desktop (free, Windows).
Download SalesDataAnalysis.pbix from this repo.
Open it. If asked, refresh the data or point it to your local data file.
Dataset

Sample sales dataset (orders, products, customers, promotions, 2020-2024). Source: add source here.

Author

Umesh Sakpal | Power BI Developer and Data Analyst Email: umeshsakpal14@gmail.com | GitHub: Sakpal23
