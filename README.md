# Sales Data Analysis | Power BI Dashboard

A 5-page Power BI report that shows how sales, profit and units sold change over time, which products and cities perform best, and how promotions affect discounts. It also lets you compare two date ranges side by side.

![Sales Overview](<img width="1342" height="757" alt="S1" src="https://github.com/user-attachments/assets/2af33159-3821-45e9-984d-a729eec78c38" />)

## What you can find out

- Which products sell the most and the least
- Which products make the most and the least profit
- Which cities bring in the most sales
- Which promotions give the biggest average discount
- How one period compares with another

## Report pages

| # | Page | What it shows |
|---|------|---------------|
| 1 | Sales Overview | Top 5 and bottom 5 products by sales, profit and quantity |
| 2 | Region-Wise Sales Analysis | Sales trend, sales by city (map), number of orders, profit vs net sales, average discount by promotion |
| 3 | Comparison Sales-Profit-Quantity | Two date filters with side-by-side bars for sales, profit and quantity |
| 4 | Edit Interaction | Two date sliders, each controlling only its own visuals |
| 5 | Table Visual | Order-level table with slicers for date, customer, product and promotion |

### Screenshots

| Region-Wise Sales | Comparison |
|---|---|
| ![Region](screenshots/02_region_wise_sales.png) | ![Comparison](screenshots/03_comparison.png) |

| Edit Interaction | Table Visual |
|---|---|
| ![Edit Interaction](screenshots/04_edit_interaction.png) | ![Table](screenshots/05_table_visual.png) |

## Data model

![Data model](screenshots/00_data_model.png)

- **Star schema:** one `Fact_Table` linked to `Dim Customers`, `Dim Product` and `Dim Promotion` (one-to-many).
- **Two date tables:**
  - `Date_Table1` is the active relationship.
  - `Date_Table2` is inactive (dotted line) and is used only inside DAX with `USERELATIONSHIP`. This powers the date comparison.
- **Measures Table:** holds all DAX measures.

## Data preparation (Power Query)

- Removed null values
- Merged queries to combine data
- Other cleaning and shaping steps to prepare the model

## DAX measures

| Measure | Purpose |
|---------|---------|
| `Sum_Dim` | Total net sales |
| `Sum_Of_Net_Sales` | Net sales for the second date range |
| `Total_Profit` | Profit for the second date range |
| `Quantity_Sold` | Units sold for the second date range |

```DAX
Sum_Dim = SUM ( Fact_Table[Net_Sales] )

Sum_Of_Net_Sales =
CALCULATE (
    SUM ( 'Fact_Table'[Net_Sales] ),
    ALL ( Date_Table1 ),
    USERELATIONSHIP ( Date_Table2[Date], Fact_Table[Date (dd/mm/yyyy)] )
)

Total_Profit =
CALCULATE (
    SUM ( Fact_Table[Profit] ),
    ALL ( Date_Table1 ),
    USERELATIONSHIP ( Date_Table2[Date], Fact_Table[Date (dd/mm/yyyy)] )
)

Quantity_Sold =
CALCULATE (
    SUM ( Fact_Table[Units Sold] ),
    ALL ( Date_Table1 ),
    USERELATIONSHIP ( Date_Table2[Date], Fact_Table[Date (dd/mm/yyyy)] )
)
```

`ALL(Date_Table1)` removes the first date filter, and `USERELATIONSHIP` switches on the second date table. So the second date filter works on its own.

## Quick findings

- About 3.51K orders from 2020 to 2024
- Apple iPhone 14 and Apple MacBook Air lead on sales and profit
- Tupperware Lunch Box, L'Oreal Shampoo and Colgate Toothpaste are lowest on sales
- Summer Sale has the highest average discount among promotions

## Tools

Power BI Desktop | Power Query | DAX | Data modelling

## Repository structure

```
sales-data-analysis-powerbi/
├── SalesDataAnalysis.pbix
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
```

## How to open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows).
2. Download `SalesDataAnalysis.pbix` from this repo.
3. Open it. If asked,
