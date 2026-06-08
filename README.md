# Sales Data Analysis

## 1. Project Overview

This repository contains a Power BI sales analysis dashboard developed as a capstone project for a Data Analytics course. Using a sample sales dataset, the project demonstrates the complete analytics lifecycle, including data transformation, data modeling, DAX calculations, interactive dashboard development, and the generation of actionable business insights and recommendations.

The primary objective of this project is to transform raw sales data into meaningful information that supports business decision-making across sales, marketing, inventory management, customer retention, and return management.

---

## 2. Business Problems and Key Questions

As part of the capstone project, business problems were identified and addressed through data analysis and dashboard development. The project focuses on answering the following questions:

1. What is the current performance of the business?
2. Which periods should be prioritized for marketing and promotional activities?
3. Which products contribute the most to revenue and profit?
4. How can inventory be managed more effectively?
5. What actions should be taken for stores across different regions?
6. How can the customer base be retained and expanded?
7. How can product return rates be reduced?

---

## 3. Methodology

The project was completed through the following stages:

1. Data Connection, Cleaning, and Transformation
2. Data Modeling
3. Data Analysis using DAX
4. Data Visualization
5. Insight Generation and Recommendations

### 3.1 Data Connection, Cleaning, and Transformation

The dataset was provided in CSV format; therefore, data extraction was not required. Each file was imported into Power BI and transformed using Power Query.

The data preparation process included:

* Validating column names and data types
* Text extraction and concatenation for required fields
* Applying conditional logic
* Identifying and handling missing values, duplicates, and data quality issues
* Reviewing column quality, distribution, and profiling where necessary

These steps ensured that the dataset was clean, consistent, and suitable for analysis.

---

### 3.2 Data Model

A Star Schema data model was implemented to optimize reporting performance and simplify analytical calculations.

<img width="1080" height="744" alt="Screenshot 2026-06-09 at 12 32 56 AM" src="https://github.com/user-attachments/assets/66137252-a9e7-490b-8437-3757c926a383" />

---

### 3.3 Data Analysis Using DAX

A variety of DAX measures were created to support business analysis and performance evaluation.

#### i. Cumulative Sales %

This measure calculates cumulative revenue contribution after ranking products by revenue. It is used to perform ABC Analysis and identify products that contribute the highest proportion of total sales.

```DAX
Cumulative Sales % =
VAR TotalSales =
    CALCULATE([Total Revenue], ALLSELECTED(Products))

VAR CurrentProductSales =
    [Total Revenue]

VAR CumulativeSales =
    CALCULATE(
        [Total Revenue],
        FILTER(
            ALLSELECTED(Products),
            [Total Revenue] >= CurrentProductSales
        )
    )

RETURN
    DIVIDE(CumulativeSales, TotalSales, 0)
```

#### ii. Year-over-Year Profit Growth %

This measure compares current-year profit with the previous year's profit to evaluate business growth performance.

```DAX
YOY Profit Growth % =
VAR PreviousYearProfit =
    CALCULATE(
        [Total Profit],
        SAMEPERIODLASTYEAR('Calendar'[Date])
    )

RETURN
    DIVIDE(
        [Total Profit] - PreviousYearProfit,
        PreviousYearProfit
    )
```

---

### 3.4 Data Visualization

After completing the analysis and calculations, appropriate visualizations were selected to communicate insights effectively.

Examples include:

* Combo Charts (Column + Line) to compare monthly revenue, costs, and sales trends across 1997 and 1998
* Bar Charts to display top-performing products and brands by profit
* KPI Cards to highlight Year-over-Year revenue and profit growth
* Treemaps to visualize regional revenue contribution
* Pie and Donut Charts for customer segmentation and purchase behavior analysis
* Tornado Charts to compare store performance between years
* Ribbon Charts to track changes in store rankings over time
* Scatter Plots to analyze the relationship between sales quantities and return quantities across regions

To enhance usability and enable deeper analysis, the dashboard also incorporates:

* Drill-down functionality
* Drill-through pages
* Dynamic tooltips
* Interactive slicers
* Navigation buttons

---

### 3.5 Insight Generation and Recommendations

Business insights were generated from each dashboard page to address the identified business questions. Based on these findings, practical recommendations were provided to support decision-making and improve business performance.

---

## 4. Key Learning and Findings

One of the most valuable aspects of this project was applying business concepts to real-world analytical scenarios. To strengthen the business context of the analysis, additional research was conducted on sales and inventory management concepts, including the Pareto Principle and ABC Analysis.

According to the Pareto Principle, approximately 20% of products are expected to generate 80% of total revenue. However, the dataset used in this project exhibited a different pattern. The analysis revealed that approximately 62.6% of products were required to contribute 80% of total sales revenue.

This finding suggests that the business is not heavily dependent on a small group of products, reducing the risk associated with pricing changes or demand fluctuations in individual products. However, it also presents a challenge from an inventory management perspective, as a larger number of products require close monitoring and control.

To address this issue, the traditional ABC Analysis was further refined by dividing Class A products into two subcategories:

* **Class A1 (Critical Products)** – Products contributing the first 50% of total revenue.
* **Class A2 (Core Products)** – Products contributing the remaining 30% required to reach the 80% cumulative revenue threshold.
* **Class B Products** – Products contributing approximately 15% of total revenue.
* **Class C Products** – Products contributing the remaining 5% of total revenue.

This enhanced classification enables more targeted inventory control strategies and helps prioritize resources toward products with the greatest business impact.
