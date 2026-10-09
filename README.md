# Sales Performance Dashboard (Power BI)

An interactive Power BI dashboard that analyses retail sales, profit and quantity trends across regions, categories and products, built on the Superstore dataset.


> Add your dashboard screenshot to this repo as `dashboard.png` so it shows above.

## Objective

Help a retail business answer simple, practical questions:

- How much are we selling, and how profitable is it?
- Which regions, categories and products drive sales?
- How do sales change over time?

## Dataset

- **Source:** [Superstore Dataset (Kaggle)](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
- **Size:** 9,994 orders, 2014 to 2017
- **Key columns:** Order Date, Region, Category, Sub-Category, Product Name, Sales, Quantity, Discount, Profit

## Tools Used

- Power BI Desktop
- Power Query (data cleaning)
- DAX (measures and date table)

## Dashboard Features

- **KPI cards:** Total Sales, Profit Margin %, Total Profit, Total Quantity
- **Sales trend:** line chart of sales by month
- **Category analysis:** sales by product category
- **Regional analysis:** sales share by region
- **Top 10 products:** best sellers by sales
- **Slicers:** filter by Year, Region and Category

## Key Numbers

| Metric | Value |
| --- | --- |
| Total Sales | 2.30M |
| Total Profit | 286.40K |
| Profit Margin | 12.47% |
| Total Quantity | 38K |

## Key Insights

- The **West** region has the highest sales (about 725K, 31.5% of total), followed by the **East** (about 679K, 29.6%).
- **Technology** is the top category by sales, with Furniture and Office Supplies close behind.
- Overall profit margin is **12.47%**.
- _Add your own insight about the monthly trend (for example, which months peak) after checking the line chart._
- _Add your own insight about the top products._

## How I Built It

### 1. Data cleaning (Power Query)

- Set `Order Date` to Date type (using the English (United States) locale, since the dates are in month/day/year format)
- Set `Sales` and `Profit` to Decimal Number
- Checked for duplicates and blank values

### 2. Date table (DAX)

```
DateT = CALENDAR(MIN(Superstore[Order Date]), MAX(Superstore[Order Date]))
Year = YEAR(DateT[Date])
Month = FORMAT(DateT[Date], "MMM")
MonthNo = MONTH(DateT[Date])
```

`DateT[Date]` is related to `Superstore[Order Date]` (one to many, single direction), and `Month` is sorted by `MonthNo`.

### 3. Measures (DAX)

```
Total Sales = SUM(Superstore[Sales])
Total Profit = SUM(Superstore[Profit])
Total Quantity = SUM(Superstore[Quantity])
Profit Margin % = DIVIDE([Total Profit], [Total Sales])
Total Orders = DISTINCTCOUNT(Superstore[Order ID])
```

### 4. Report design

- Dark theme with one blue colour for all bar and line charts
- Layout: title on top, slicers on the left, KPI cards in the first row, charts in the second row, Top 10 products at the bottom
- Top 10 products uses a Top N filter on Product Name by Total Sales

## How to Open

1. Download `Sales Dashboard.pbix` from this repo.
2. Open it in [Power BI Desktop](https://powerbi.microsoft.com/desktop) (free, Windows only).
3. If Power BI asks for the data file, point it to `Sample - Superstore.csv` from the Kaggle link above.
