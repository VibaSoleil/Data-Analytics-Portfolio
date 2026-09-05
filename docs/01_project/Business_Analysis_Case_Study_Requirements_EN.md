D:\Project_01_Data_Analyst>type "D:\AI_Project_Documentation\Business_Analysis_Case_Study_Requirements.md"

PROJECT QUESTIONS IN ENGLISH

Main Case Study (Combination of Several Business Problems)
Business Scenario

"The company has experienced a decline in sales performance during several recent periods. The management team requests an analysis to identify the causes of revenue decline and determine improvement strategies."

Participants are required to identify:

Problem 1 ÔÇö Declining Sales Performance
Analysis Requirements:

Analyze:

Monthly revenue comparison.
Number of transactions per period.
Products experiencing sales decline.
Regions experiencing a decrease in contribution.
Problem 2 ÔÇö Customers Becoming Inactive
Analysis Requirements:

Analyze:

Customers with a long period since their last transaction.
High-value customers who have stopped purchasing.
Top customers based on total purchase value.
Problem 3 ÔÇö Unbalanced Inventory
Analysis Requirements:

Analyze:

Products with high stock levels but low sales performance.
Products requiring restocking.
Products generating the highest revenue.
Problem 4 ÔÇö Data Cleaning Before Analysis
Tasks:

Identify:

Duplicate products.
Missing customer data.
Phone number standardization.

Validation:

Check whether:

quantity ├ù price = total_harga

is correct.

PART 1 ÔÇö DATA UNDERSTANDING & DATABASE EXPLORATION
Task 1. Understanding Database Structure

Use database:

perusahaan_db

Analyze the following tables:

produk
pelanggan
transaksi
keuangan

Create documentation:

Explain the function of each table.
Explain relationships between tables.
Create a simple Entity Relationship Diagram (ERD).
PART 2 ÔÇö DATA CLEANING

Before performing business analysis, conduct a data quality assessment.

Problem 1: Customer Data Quality

The marketing department found possible issues in customer data.

Perform analysis:

1. Identify Missing Values

Find:

Customers without addresses.
Customers without phone numbers.
Incomplete customer records.

Output format:

id_pelanggan    nama    masalah
xxx     xxx     missing address
2. Phone Number Standardization

Identify problems:

Examples:

+62-811-402-8937
0818762012
(004) 543 9687
+62 (27) 246-5718

Create standardization rules.

Final format:

Option 1:

08xxxxxxxxxx

or international format:

+628xxxxxxxxxx
3. Duplicate Customer Detection

Find customers with possible duplicates based on:

Same name.
Same phone number.
Same address.

Provide recommendations:

Should records be merged?
Should records be maintained separately?
Problem 2: Product Data Quality

Possible issues were found in the product master data.

Perform analysis:

1. Identify Duplicate Products

Example:

Laptop Lenovo
Laptop Lenovo

Answer:

Are both products actually the same item?
What impact will duplicates have on sales reports?
2. Product Price Validation

Compare:

produk.harga

with:

transaksi.total_harga / transaksi.jumlah

Identify transactions with incorrect values.

Problem 3: Transaction and Financial Data Validation

The company wants to ensure financial reporting accuracy.

Perform validation:

Formula:

quantity ├ù product price = transaction total_harga

Compare:

transaksi.total_harga

with:

keuangan.pemasukan

Identify:

Transactions with different values.
Transactions without financial records.
Financial records without matching trans

PART 3 ÔÇö SALES ANALYSIS
Problem 4: Is Sales Performance Declining?

Management suspects that company sales performance has decreased.

Analysis Requirements:

Analyze:

1. Monthly Sales Trend

Calculate:

Total revenue per month.
Number of transactions per month.
Total products sold per month.

Create visualizations:

Revenue line chart.
Transaction volume bar chart.

Answer the following questions:

Which month has the highest revenue?
Which month has the lowest revenue?
Is there a declining sales trend?
Problem 5: Best-Selling Products and Weak Products

Management wants to understand product performance.

Calculate product rankings based on:

A. Total Units Sold

Ranking format:

Product Units Sold      Ranking
B. Total Revenue

Ranking format:

Product Revenue Ranking
C. Transaction Frequency

Analyze:

Do products with the highest sales volume also generate the highest revenue?
Are high-frequency products the most profitable products?
Problem 6: Low-Performing Product Analysis

The warehouse team identified several products with excessive inventory.

Find products with:

High stock levels.
Low sales performance.

Create categories:

Fast Moving Product

Criteria:

High sales volume.
Inventory decreases quickly.
Slow Moving Product

Criteria:

High inventory level.
Low transaction frequency.

Provide recommendations:

Discount strategy.
Promotional campaigns.
Inventory reduction strategy.
PART 4 ÔÇö CUSTOMER ANALYSIS
Problem 7: Identifying Best Customers

The marketing team wants to reward loyal customers.

Calculate customer ranking based on:

Total Purchase Value

Formula:

SUM(total_harga)
Transaction Frequency

Formula:

COUNT(id_transaksi)
Total Products Purchased

Formula:

SUM(jumlah)

Create:

Top 10 Best Customers Report
Problem 8: Customer Churn Analysis

The company has lost several customers.

Identify customers who:

Purchased previously.
Have not made transactions for a long time.

Use:

Last transaction date.
Previous transaction count.
Total purchase value.

Classify customers into:

Active Customer

Customers who frequently purchase.

At Risk Customer

Customers showing decreasing activity.

Inactive Customer

Customers who have stopped purchasing.

Provide strategies:

Special promotions.
Customer follow-up.
Loyalty programs.
PART 5 ÔÇö REGIONAL ANALYSIS
Problem 9: Sales Distribution Analysis

Use customer address data.

Analyze:

Cities with the highest number of transactions.
Cities generating the highest revenue.
Regions with the largest customer base.

Create:

Top 10 Potential Regions

Answer:

Which regions require stronger marketing focus?
Which regions represent new market opportunities?
PART 6 ÔÇö TRANSACTION ANALYSIS
Problem 10: Customer Transaction Pattern Analysis

Analyze transactions based on:

Time Dimension:
Month.
Date.
Specific periods.

Find:

Highest transaction periods.
Purchasing patterns.
Transaction Value Classification

Group transactions into:

Small Transaction
< Rp5,000,000
Medium Transaction
Rp5,000,000 - Rp20,000,000
Large Transaction
> Rp20,000,000

Analyze:

Contribution percentage of each transaction category.
Which category contributes the largest revenue.
PART 7 ÔÇö FINANCIAL ANALYSIS
Problem 11: Revenue Analysis

Use table:

keuangan

Calculate:

Total revenue.
Average transaction revenue.
Revenue growth.

Analyze:

Does increasing transaction quantity always increase revenue?
What factors influence revenue growth?
Problem 12: Highest Revenue Contribution Products

Combine:

produk
+
transaksi
+
keuangan

Identify:

Products contributing the most:

Revenue.
Transaction volume.

Apply:

Pareto Analysis (80/20 Principle)

Determine:

Which products generate the majority of company revenue.
Which products contribute minimally.
PART 8 ÔÇö FINAL BUSINESS REPORT

Create a final management report.

The report must contain:

1. Executive Summary

Include:

Current business condition.
Main business problems.
Business opportunities.
2. Key Findings

Minimum:

5 Business Insights

Example:

"Laptop Lenovo contributes 65% of total revenue but creates product dependency risk."

3. Business Recommendations

Provide recommendations for:

Product Strategy

Examples:

Inventory strategy.
Product promotion.
Product development.
Customer Strategy

Examples:

Loyalty programs.
Customer retention programs.
Regional Strategy

Examples:

Market expansion.
Regional marketing improvement.
Operational Strategy

Examples:

Data quality improvement.
Process optimization.
FINAL PROJECT OUTPUT REQUIREMENTS

Participants must produce:

1. Database Analysis

Contains:

SQL queries.
Data exploration.
Data cleaning results.
Validation results.
2. Business Dashboard

Minimum dashboard components:

KPI Metrics
Total Revenue.
Total Transactions.
Total Customers.
Total Products.
Business Performance Visualization

Include:

Best-performing product.
Best customer.
Sales trend.
Best-performing region.
3. Business Report

Format:

PDF.
PowerPoint.

Must contain:

Business problems.
Analysis process.
Data visualization.
Business insights.
Strategic recommendations.
PROJECT OBJECTIVE

The final objective is to transform raw business data into meaningful strategic insights that support management decision-making through:

Accurate data analysis.
Professional visualization.
Business intelligence reporting.
Data-driven recommendations.
D:\Project_01_Data_Analyst>








