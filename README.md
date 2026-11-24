# Superstore Sales & Profitability Dashboard | Power BI

## 1. Project Overview

This project focuses on analysing Superstore sales and profitability using Microsoft Power BI. The objective is to transform raw sales transaction data into an interactive business intelligence dashboard that helps understand overall business performance, regional contribution, product profitability, and sales trends over time.

The dashboard provides an overview of key performance indicators (KPIs), enables comparisons across regions and product categories, and supports interactive analysis through date and region slicers.

**Project Type:** Business Intelligence & Data Analytics  
**Tool:** Microsoft Power BI  
**Data Source:** Superstore Sales Dataset

---

## 2. Business Problem

Businesses need to monitor sales performance and profitability to identify growth opportunities, understand regional differences, and evaluate product performance.

The project addresses the following business questions:

- What are the overall sales, profit, order volume, and profit margin?
- How do sales and profit change over time?
- Which regions contribute the most to overall sales?
- How does profitability vary across regions?
- Which product categories and sub-categories generate the highest sales and profit?
- Which products have low or negative profit margins?
- How does sales performance compare with the previous year?

---

## 3. Project Objectives

- Analyse overall sales and profitability.
- Track monthly sales and profit trends.
- Evaluate regional sales performance and profit margins.
- Identify high- and low-performing product categories and sub-categories.
- Calculate year-over-year (YoY) sales growth.
- Build an interactive dashboard with dynamic filtering.
- Organise the data using a Star Schema data model.

---

## 4. Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| Microsoft Power BI Desktop | Dashboard development and data visualisation |
| Power Query | Data cleaning and transformation |
| DAX | Measures and business calculations |
| Superstore Sales Dataset | Source transaction data |

---

## 5. Dataset & Data Preparation

The project uses Superstore sales transaction data containing information about orders, customers, products, shipping, sales, and profit.

### Data preparation steps

The following transformations were performed using Power Query:

1. Imported the original Superstore dataset into Power BI.
2. Converted Order Date and Ship Date columns to the Date data type.
3. Identified records with missing Order Date values.
4. Removed 806 records with missing Order Date values to maintain date-based analysis.
5. Retained 11 records with missing Postal Code values because Postal Code was not required for the core analysis.
6. Created separate dimension tables for customers and products.
7. Created a dedicated date dimension covering January 2015 to December 2018.

**Final Fact Orders table:** 9,994 rows.

The original source Excel file was not modified.

---

## 6. Data Modelling – Star Schema

A Star Schema was implemented to organise the data and support efficient filtering and analysis.

### Tables created

**Fact Orders**
- Contains the sales transaction records.
- Includes order details, customer and product identifiers, dates, sales, profit, and other transaction attributes.

**Dim Customer**
- Customer ID
- Customer Name
- Segment
- Country
- City
- State
- Postal Code
- Region

**Dim Product**
- Product ID
- Product Name
- Category
- Sub-Category

**Dim Date**
- Date
- Year
- Month Number
- Month
- Quarter
- Year-Month

### Relationships

The following one-to-many relationships were established:

| Dimension Table | Fact Table | Relationship |
|---|---|---|
| Dim Customer | Fact Orders | Customer ID |
| Dim Product | Fact Orders | Product ID |
| Dim Date | Fact Orders | Order Date |

All relationships use single-direction filtering from the dimension tables to the Fact Orders table.

---

## 7. DAX Measures

The following DAX measures were created to calculate the key business metrics.

### Total Sales

```dax
Total Sales = SUM('Fact Orders'[Sales])
```

### Total Profit

```dax
Total Profit = SUM('Fact Orders'[Profit])
```

### Total Orders

```dax
Total Orders = DISTINCTCOUNT('Fact Orders'[Order ID])
```

### Profit Margin %

```dax
Profit Margin % =
DIVIDE([Total Profit], [Total Sales], 0)
```

### Previous Year Sales

```dax
Previous Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Dim Date'[Date])
)
```

### YoY Sales Growth %

```dax
YoY Sales Growth % =
DIVIDE(
    [Total Sales] - [Previous Year Sales],
    [Previous Year Sales],
    0
)
```

Percentage measures were formatted to display two decimal places.

---

## 8. Dashboard Design & Visualisations

The dashboard consists of three interactive report pages.

### Page 1 – Executive Overview

Provides a consolidated view of overall business performance.

**Key Performance Indicators:**
- Total Sales
- Total Profit
- Total Orders
- Profit Margin %
- YoY Sales Growth %

**Visualisations:**
- Line chart displaying monthly sales and profit trends.
- Treemap showing sales contribution by product category and sub-category.
- Waterfall chart showing monthly sales contribution using Year-Month.
- Date slicer for date-based filtering.
- Region slicer for regional filtering.

### Page 2 – Regional Performance

Focuses on comparing sales and profitability across geographical regions.

**Visualisations:**
- Clustered bar chart comparing Total Sales and Total Profit by region.
- Clustered column chart comparing Profit Margin % by region.
- Treemap showing regional sales contribution.

### Page 3 – Product Profitability

Provides a detailed analysis of product category and sub-category performance.

**Visualisation:**
- Matrix displaying Total Sales, Total Profit, and Profit Margin % by Category and Sub-Category.

**Additional formatting:**
- Conditional formatting applied to Profit Margin %.
- Colour indicators help distinguish different profitability ranges.
- Negative profit margins remain visible in the matrix.

---

## 9. Interactive Dashboard Features

- **Date Slicer:** Enables analysis over a selected date range.
- **Region Slicer:** Allows users to focus on individual regions.
- **Synchronized Slicers:** Date and region selections are synchronized across all three report pages.
- **Dynamic Filtering:** Visualisations update based on the selected filters.

These features allow users to explore business performance from different perspectives.

---

## 10. Key Business Metrics

The following figures represent the overall dataset values with no additional date or region filters applied.

| Metric | Value |
|---|---:|
| Total Sales | $2,297,200.86 |
| Total Profit | $286,397.02 |
| Total Orders | 5,009 |
| Profit Margin | 12.47% |
| YoY Sales Growth | 46.88% |

### Regional Profit Margin

| Region | Profit Margin |
|---|---:|
| East | 15.46% |
| West | 12.82% |
| Central | 12.26% |
| South | 7.51% |

### Business Observations

- The East region has the highest profit margin among the four regions.
- The South region has the lowest profit margin.
- Overall profit margin is 12.47%.
- Product profitability varies significantly across categories and sub-categories.
- Some sub-categories generate negative profits, highlighting areas that may require further business investigation.

---

## 11. Project Deliverables

The repository contains the following project files:

| File | Description |
|---|---|
| `.pbix` file | Interactive Power BI report |
| `.pdf` file | Exported dashboard report |
| `README.md` | Project documentation |

Dashboard screenshots will also be included in the repository to provide a quick visual preview of the report.

---

## 12. Skills Demonstrated

- Data cleaning and transformation
- Power Query
- Data modelling and Star Schema design
- One-to-many table relationships
- DAX calculations and measures
- KPI development
- Business intelligence and data visualisation
- Interactive dashboard development
- Sales and profitability analysis
- Business interpretation and reporting

---

## 13. Conclusion

This project demonstrates how raw sales transaction data can be transformed into an interactive business intelligence solution using Microsoft Power BI.

By combining data preparation, Star Schema modelling, DAX measures, and interactive visualisations, the dashboard provides insights into overall business performance, regional contribution, and product profitability.

The project highlights the use of data analytics to support business monitoring, performance evaluation, and data-driven decision-making.
