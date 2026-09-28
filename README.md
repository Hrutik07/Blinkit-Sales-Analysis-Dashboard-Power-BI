# Blinkit-Sales-Analysis-Dashboard-Power-BI
Power BI dashboard analyzing Blinkit sales, products, outlets, and customer preferences using DAX and interactive visualizations.

## Project Overview

This project is a Power BI dashboard created to analyze Blinkit-style outlet and product sales data.

The dashboard focuses on sales performance, product performance, outlet performance, and customer preferences. It was developed as a portfolio project to demonstrate data analysis, DAX measures, data visualization, and business insight generation using Microsoft Power BI.

## Business Questions

The dashboard addresses the following business questions:

### Sales Analysis
- What are the total sales across all outlets?
- Which product categories contribute the most to revenue?
- How do sales vary across different outlet types?
- What is the trend in sales over different establishment years?

### Product Performance
- Which items have the highest and lowest sales?
- How does item visibility impact sales?
- Does item weight have any correlation with sales?

### Outlet Performance
- Which outlets generate the highest revenue?
- How does outlet size affect sales?
- How does outlet type compare in terms of sales performance?

### Customer Preferences
- What is the distribution of item fat content among the best-selling products?
- How do customers rate products, and how does rating relate to sales?

## Dashboard Pages

The Power BI report contains four main analysis pages.

### 1. Sales Analysis

Key elements:
- Total Sales KPI
- Average Sales Per Outlet KPI
- Total Records KPI
- Sales Growth %
- Sales by Item Type
- Sales by Outlet Type
- Sales trend by Outlet Establishment Year

### 2. Product Performance

Key elements:
- Top and bottom sales analysis
- Sales by Item Identifier
- Item Visibility vs Sales
- Item Weight vs Sales
- Top 5 Selling Items

### 3. Outlet Performance

Key elements:
- Outlet Performance Score
- Sales by Outlet Identifier
- Sales by Outlet Size
- Sales by Outlet Type
- Sales by Outlet Location Type

### 4. Customer Preferences

Key elements:
- Sales by Item Type and Fat Content
- Rating Distribution
- Sales vs Average Rating by Establishment Year

## Key DAX Measures

The project uses DAX measures to calculate the main KPIs and analytical metrics.

### Total Sales

```DAX
TOTAL SALES
```

The existing total sales measure is used throughout the report.

### Average Sales Per Outlet

```DAX
Average Sales Per Outlet =
DIVIDE(
    [TOTAL SALES],
    DISTINCTCOUNT('Blinkit Data'[Outlet Identifier]),
    0
)
```

### Total Records

```DAX
Total Records =
COUNTROWS('Blinkit Data')
```

The dataset does not provide a dedicated transaction ID. Therefore, this metric represents the number of records in the dataset rather than independently verified real-world transactions.

### Average Rating

```DAX
Average Rating =
AVERAGE('Blinkit Data'[Rating])
```

### Sales Growth %

```DAX
Sales Growth % =
VAR CurrentSales =
    [TOTAL SALES]
VAR PreviousYearSales =
    CALCULATE(
        [TOTAL SALES],
        FILTER(
            ALL('Blinkit Data'[Outlet Establishment Year]),
            'Blinkit Data'[Outlet Establishment Year]
                = MAX('Blinkit Data'[Outlet Establishment Year]) - 1
        )
    )
RETURN
    DIVIDE(
        CurrentSales - PreviousYearSales,
        PreviousYearSales,
        0
    )
```

Because the dataset does not contain a transaction date, this measure compares sales across Outlet Establishment Year values. It should therefore be interpreted as growth between establishment-year groups rather than conventional transaction-level year-over-year growth.

### Outlet Sales Contribution %

```DAX
Outlet Sales Contribution % =
DIVIDE(
    [TOTAL SALES],
    CALCULATE(
        [TOTAL SALES],
        ALLSELECTED('Blinkit Data'[Outlet Identifier])
    ),
    0
)
```

### Outlet Performance Score

```DAX
Outlet Performance Score =
VAR SalesScore =
    [Outlet Sales Contribution %] * 100

VAR RatingScore =
    DIVIDE(
        [Average Rating],
        5,
        0
    ) * 100

RETURN
    (SalesScore * 0.70) +
    (RatingScore * 0.30)
```

The Outlet Performance Score is a custom portfolio metric. It combines outlet sales contribution and average rating. It is not an official Blinkit metric.

## Visualizations

The report uses Power BI visualizations including:

- KPI Cards
- Bar Charts
- Column Charts
- Stacked Column Charts
- Line Charts
- Scatter Plots
- Treemap
- Rating distribution chart

The visual design is intended to make sales trends, product performance, outlet comparisons, and customer-related patterns easy to analyze.

## Data Limitations

The dataset has several limitations that are important when interpreting the dashboard:

1. There is no dedicated transaction ID, so the Total Records measure should not automatically be interpreted as the number of real-world transactions.
2. There is no transaction date field. Outlet Establishment Year is used as the available time-related dimension.
3. The Outlet Performance Score is a custom analytical metric created for this portfolio project.
4. Outlet Location Type is treated as a categorical field. It does not necessarily provide precise geographic coordinates suitable for a geographic map.
5. Profit or cost information is not available in the model, so outlet performance is analyzed using sales rather than actual profit.

## Tools Used

- Microsoft Power BI
- Power Query
- DAX
- Data Visualization
- Data Analysis

## Project Structure

```text
Blinkit-PowerBI-Analysis/
│
├── Blinkit_By_Hrutik_Mock_25_09.pbix
├── README.md
└── screenshots/
    ├── sales-analysis.png
    ├── product-performance.png
    ├── outlet-performance.png
    └── customer-preferences.png
```

## How to Use

1. Download the `.pbix` file.
2. Open it using Microsoft Power BI Desktop.
3. Refresh the data if the source connection is available.
4. Explore the four dashboard pages and interact with the filters and visuals.

## Portfolio Disclaimer

This is a personal Power BI portfolio project created for learning and demonstration purposes.

The project uses Blinkit-related sample data and branding references for analytical demonstration. It is not an official Blinkit report and is not affiliated with, sponsored by, or endorsed by Blinkit.

The underlying dataset should be redistributed only if its original license or source terms permit redistribution.

## Author

Hrutik Hiwase

Power BI | Data Analysis | DAX | Business Intelligence
