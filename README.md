# Power BI Financial Analysis Dashboard

A two-page Power BI dashboard built on the Superstore transaction dataset to help stakeholders quickly understand profitability, customer concentration, and product performance.

<img width="2000" height="1156" alt="image" src="https://github.com/user-attachments/assets/31387470-543c-41b2-88bd-4366721bf94f" />
<img width="2000" height="1156" alt="image" src="https://github.com/user-attachments/assets/5962b42f-a330-4c68-8bf5-5fe1ff5d6097" />

## Project Detail

This dashboard focuses on key financial and operational metrics such as **total profit**, **distinct customers**, and **top-performing products**, with built-in forecasting for future sales and order volume. All visuals are fully interactive and controlled by slicers for **Year**, **Region**, **Segment**, and **State**.

## Features

- **Executive KPIs** – Total Profit, Distinct Customers, Total Orders  
- **Top products analysis** – Separate views for:
  - Top 5 products by revenue (high-value items)
  - Top products by volume (high-quantity items)
- **Geographic performance** – Top 5 states by revenue plus revenue share percentages  
- **Forecasting** – Sales forecast and projected order volume extending into future years  
- **Interactive slicers** – Filter the entire report by Year, Region, Segment, and State  

## Important Insights (2015–2018)

- The highest total revenue between 2015–2018 comes from the **West**, specifically **California**, with **$446.31K** in sales.  
- Regionally, **Texas**, **Florida**, and **New York** are also major revenue generators.  
- The **Consumer** segment is the biggest revenue driver in these key states.  
- In the **South** region, **Virginia** is more profitable than Florida, despite Florida’s strong overall revenue.  

## Product Performance

**High-value products**

- **Canon imageCLASS copier** is the top high-value product with **$61,599.82** in total revenue.  
- **Fellowes binding machines** follow with **$27,453.38** in total sales.  

**High-volume products**

- The highest-volume items are mainly from the **Supplies** category (envelopes, art, fasteners, paper).  
- These supply items have a **combined volume of 186 units**, with **envelopes contributing around 25% of the related revenue**, indicating strong recurring demand.

## Customer & Geographic Distribution

- The customer base is **widely dispersed** across the U.S., but **California, New York, and Texas** consistently lead revenue across segments and years.  
- These states form the company’s most profitable and recurring customer base and act as the primary revenue hubs.  

## Future Trend

- Both **revenue** and **order volume** are expected to **continue growing at a steady rate**, based on historical performance and observed year‑over‑year increases.  

## Executive Summary Dashboard

**Page 1** serves as an executive overview of performance.

- Highlights profit by state and region, with **California, New York, and Texas** emerging as key contributors.  
- Shows order volume concentration in **Supplies**, especially **Envelopes** and **Fasteners**, which dominate item counts.  
- Emphasizes the strength of the **Consumer** segment and the impact of high‑value products like the Canon imageCLASS copier and Fellowes binding machines.  
- Demonstrates a **steady upward trajectory** in revenue and order volume, supporting expectations of continued growth.  

## Dataset & Deep Dive

**Page 2** focuses on the underlying dataset (with sensitive information redacted) for validation and deeper analysis.

Components:
- **Data table:** Order Date, Ship Date, Customer ID, State, Segment, Category, Sub-Category  
- **Card:** Total Orders, filterable through the same slicers as Page 1  
- **Metric:** Top 5% customer share, used to quantify profit concentration risk  
- **Treemap:** Sub-Category by **Total Sales** (e.g., Phones, Chairs, Storage, Tables, Binders, etc.)  

This page serves to:

- Examine how each **sub-category** contributes to profit **by state, region, and segment** within any selected time period.  
- Assess **risk diversification**: with the **top 5% customer share under 4%**, the business shows low dependency on a small group of customers and a healthy spread of revenue sources.  

## Dataset Context

This project uses a **retail time series dataset from a global superstore covering 4 years** of transactions (2015-2018), a total of 9800 records.  
The data contains order-level records (dates, products, customers, locations) and is well-suited for **exploratory data analysis (EDA)** and **short‑term sales forecasting**.  

The dataset is structured for BI modeling, making it suitable for both **descriptive analytics** (dashboards) and **predictive tasks**.

## Data Preparation & Cleaning

- Converted **Order Date** and related fields from text to proper date types.  
- Modified the query to correctly interpret dates in **UK format (dd/mm/yyyy)**, then standardized display formatting inside Power BI for consistent reporting.  
- Checked for and handled **null values** across key fields to ensure reliable aggregations, filters, and time intelligence.  

## Custom DAX Measures

Key DAX measures created for analysis and risk assessment include:

``
Year = YEAR([Order Date])
``

```
Top 5 Share % =
DIVIDE(
    SUMX(
        TOPN(
            5,
            SUMMARIZE(train, train[Customer ID], "OrderValue", SUM(train[Sales])),
            [OrderValue], DESC
        ),
        [OrderValue]
    ),
    CALCULATE(SUM(train[Sales]), ALL(train)),
    0
) * 100
```
```
Top Customer Risk % =
DIVIDE(
    MAXX(TOPN(1, train, train[Sales], DESC), train[Sales]),
    SUM(train[Sales])
)
```
## Usage

1. Download `.pbix` file from repository
2. Open the downloaded file through Power BI Desktop
3. Access dashboard components and interact with slicers for data visualizations and insights
   
## Contact

Feel free to reach out at kalden.dorji@outlook.com
