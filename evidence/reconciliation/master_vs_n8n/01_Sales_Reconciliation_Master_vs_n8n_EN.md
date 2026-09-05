RECONCILIATION REPORT

MASTER SALES vs n8n SALES PIPELINE

Project: Project_01_Data_Analyst
Module: SALES
Reconciliation Type: Master Layer Validation vs n8n Processing Output
Status: ON PROGRESS

PART 1 — RECONCILIATION SCOPE & SOURCE FILE
Reconciliation Objective

To validate the consistency between:

MASTER SALES
as the audit layer / reference dataset
n8n SALES Pipeline
as the result of the processing automation pipeline

Objectives:

ensure the transaction count is the same
ensure the revenue is the same
ensure the sales units are the same
ensure there is no data loss during the n8n process

SOURCE FILES USED
A. MASTER SALES FILE

Location:

D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv

Function:

Reference Master Dataset
Audit Layer
Primary comparison reference

Structure:

Rows : 5000
Columns : 14

Columns:

id_transaksi
tanggal_transaksi
tahun
bulan
periode
id_produk
nama_produk
harga
jumlah
total_harga
id_pelanggan
nama_pelanggan
pemasukan
kategori_transaksi

B. n8n CLEAN DATA FILE

Location:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

Function:

Input Dataset n8n SALES Analysis
n8n pipeline cleaning result
Source for SALES Professional calculations

Structure:

Rows : 5000
Columns : 14

C. n8n SALES ANALYSIS SCRIPT

File:

D:\Project_01_Data_Analyst\SCRIPT\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.py

Function:

Generates:

PART 1 SALES OVERVIEW
PART 2 MONTHLY SALES TREND
PART 3 MONTHLY SALES COMPARISON
PART 4 PRODUCT SALES PERFORMANCE
PART 5 PRODUCT MOVEMENT ANALYSIS
PART 6 CUSTOMER ANALYSIS
PART 7 CUSTOMER SEGMENTATION

PART 2 — KPI RECONCILIATION RESULT
Evidence #1 — Basic KPI Validation

Command:

py -c "import pandas as pd; ..."

Result:

KPI MASTER SALES n8n CLEAN DATA Status
Total Transaction 5,000 5,000 ✅ PASS
Total Revenue Rp110,380,250,000 Rp110,380,250,000 ✅ PASS
Total Unit Sold 27,400 27,400 ✅ PASS

Evidence Output

=== MASTER SALES ===

Rows: 5000
Revenue: 110380250000.0
Unit: 27400

=== n8n CLEAN DATA ===

Rows: 5000
Revenue: 110380250000.0
Unit: 27400

PART 3 — INITIAL CONCLUSION

Status:

✅ PASS

Finding:

No differences were found in the main KPIs between:

MASTER SALES
VS
n8n SALES PIPELINE

The initial validation confirms:

all transactions remain available
all revenue is preserved
all sales units remain the same

End of Part 1

PART 2 — TRANSACTION LEVEL RECONCILIATION
Objective

To perform a detailed transaction-level check between:

MASTER SALES
VS
n8n CLEAN DATA

Validation includes:

Unique transaction count
Missing transaction IDs
Additional transaction IDs
Duplicate transactions
Transaction value consistency

2.1 Transaction Count Validation

Files used:

MASTER
D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv
n8n
D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

Validation column:

id_transaksi

Evidence #2 — Unique Transaction Check

Validation results:

Parameter MASTER SALES n8n CLEAN DATA Status
Total Transaction ID 5.000 5.000 ✅ PASS
Unique Transaction ID 5.000 5.000 ✅ PASS
Duplicate Transaction 0 0 ✅ PASS

Conclusion

No:

missing transactions
duplicate transactions
additional transactions

Status:

✅ TRANSACTION INTEGRITY PASS

2.2 Transaction ID Matching

Method:

Performing a comparison between:

MASTER.id_transaksi
VS
n8n.id_transaksi

Audit formula:

Missing Transaction =
MASTER ID - n8n ID

Additional Transaction =
n8n ID - MASTER ID

Evidence #3 — Transaction ID Difference

Results:

Missing Transaction ID : 0

Additional Transaction ID : 0

Status:

✅ PASS

2.3 Transaction Value Validation

Columns compared:

Column
id_transaksi
id_produk
jumlah
total_harga

Objective:

Ensure that the same transactions have the same values.

Evidence #4 — Financial Transaction Match

Results:

Parameter Status
Transaction ID Match ✅ PASS
Product ID Match ✅ PASS
Quantity Match ✅ PASS
Total Harga Match ✅ PASS

PART 2 SUMMARY
Transaction Reconciliation Result

Area Audit Status
Transaction Count ✅ PASS
Unique ID Check ✅ PASS
Missing Transaction ✅ PASS
Additional Transaction ✅ PASS
Duplicate Transaction ✅ PASS
Transaction Value ✅ PASS

Finding Update

FINDING SALES-001

Title:
Transaction Consistency Validation

Status:
✅ COMPLETED

Evidence:

MASTER:

5000 transactions

n8n:

5000 transactions

Difference:

0 transactions

Conclusion PART 2

The transaction data in MASTER SALES and the n8n SALES Pipeline are identical at the transaction level.

No:

transaction loss
unauthorized transaction additions
changes in transaction values

MASTER SALES vs n8n SALES PIPELINE

PART 3 — REVENUE & PRODUCT SALES RECONCILIATION
3.1 Validation Objective

To check the consistency of sales results by product between:

MASTER SALES
VS
n8n SALES PIPELINE

Validation includes:

Total revenue per product
Total units sold per product
Number of transactions per product
Product ranking by revenue
Product ranking by units

3.2 Source File

MASTER SALES
D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv

Columns used:

nama_produk
jumlah
total_harga
id_transaksi

n8n SALES OUTPUT

Script:

D:\Project_01_Data_Analyst\SCRIPT\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.py

Output:

D:\Project_01_Data_Analyst\OUTPUT\DATA\
Product_Sales_Performance_Report.csv

and:

Product_Movement_Analysis.csv

3.3 Product Revenue Validation

MASTER SALES Results

Product revenue ranking:

Ranking Product Total Revenue
1 Laptop Lenovo Rp91.562.000.000
2 Printer Epson Rp13.037.500.000
3 Keyboard Mechanical Rp4.391.250.000
4 Mouse Logitech Rp1.389.500.000

n8n SALES Results

Product revenue ranking:

Ranking Product Total Revenue
1 Laptop Lenovo Rp91.562.000.000
2 Printer Epson Rp13.037.500.000
3 Keyboard Mechanical Rp4.391.250.000
4 Mouse Logitech Rp1.389.500.000

Evidence #5 — Revenue Product Match

Status:

Parameter Status
Total revenue per product ✅ PASS
Revenue ranking ✅ PASS
Top product ✅ PASS

3.4 Product Unit Validation

MASTER SALES

Ranking Product Units Sold
1 Laptop Lenovo 10.772
2 Keyboard Mechanical 5.855
3 Mouse Logitech 5.558
4 Printer Epson 5.215

n8n SALES

Ranking Product Units Sold
1 Laptop Lenovo 10.772
2 Keyboard Mechanical 5.855
3 Mouse Logitech 5.558
4 Printer Epson 5.215

Evidence #6 — Product Quantity Match

Status:

Parameter Status
Total Units ✅ PASS
Units per product ✅ PASS
Unit ranking ✅ PASS

3.5 Business Insight Validation

Dominant Product

Results from both systems:

Product:
Laptop Lenovo

Units:
10.772

Revenue:
Rp91.562.000.000

Conclusion:

Laptop Lenovo is:

✅ The product with the highest sales volume
✅ The product with the largest revenue contribution

PART 3 SUMMARY

Revenue & Product Reconciliation Result

Area Audit Status
Total Revenue ✅ PASS
Revenue per Product ✅ PASS
Total Units Sold ✅ PASS
Units per Product ✅ PASS
Product Ranking ✅ PASS
Business Insight ✅ PASS

Finding Update

FINDING SALES-002

Title:
Product Revenue and Sales Performance Consistency

Status:
✅ COMPLETED

Evidence:

MASTER and n8n produce:

Laptop Lenovo
Revenue : Rp91.562.000.000
Units : 10.772

No differences were found between:

MASTER SALES
VS
n8n SALES PIPELINE

Conclusion PART 3

The product analysis results from MASTER and n8n are fully consistent.

No:

changes in product revenue
changes in product ranking
loss of sales units

PART 4 — MONTHLY SALES TREND & TIME SERIES RECONCILIATION
4.1 Validation Objective

To validate sales patterns by time period between:

MASTER SALES
VS
n8n SALES PIPELINE

Validation covers:

Total monthly revenue
Number of transactions per month
Total units sold per month
Highest revenue month
Lowest revenue month
Sales increase and decrease trends

4.2 Source File

MASTER SALES

File:

D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv

Columns:

tanggal_transaksi
bulan
total_harga
jumlah
id_transaksi

n8n SALES PIPELINE

Script:

D:\Project_01_Data_Analyst\SCRIPT\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.py

Analysis sections:

PART 2 - MONTHLY SALES TREND
PART 3 - MONTHLY SALES COMPARISON

4.3 Monthly Revenue Comparison

MASTER SALES Monthly Summary

Month Revenue
2025-07 Rp6.888.000.000
2025-08 Rp9.487.250.000
2025-09 Rp9.621.500.000
2025-10 Rp8.604.750.000
2025-11 Rp8.077.500.000
2025-12 Rp9.952.000.000
2026-01 Rp10.463.250.000
2026-02 Rp8.174.500.000
2026-03 Rp8.813.500.000
2026-04 Rp9.223.500.000
2026-05 Rp9.477.500.000
2026-06 Rp8.883.250.000
2026-07 Rp2.713.750.000

n8n Monthly Sales Trend

Execution result:

PART 2 - MONTHLY SALES TREND

Produced the same values:

Month Revenue
2025-07 Rp6.888.000.000
2025-08 Rp9.487.250.000
2025-09 Rp9.621.500.000
2025-10 Rp8.604.750.000
2025-11 Rp8.077.500.000
2025-12 Rp9.952.000.000
2026-01 Rp10.463.250.000
2026-02 Rp8.174.500.000
2026-03 Rp8.813.500.000
2026-04 Rp9.223.500.000
2026-05 Rp9.477.500.000
2026-06 Rp8.883.250.000
2026-07 Rp2.713.750.000
Evidence #7 — Monthly Revenue Match
Parameter Status
Number of periods ✅ PASS
Revenue for each month ✅ PASS
Trend pattern ✅ PASS
4.4 Highest & Lowest Sales Month Validation
Highest Revenue Month

MASTER:

Month:
2026-01

Revenue:
Rp10.463.250.000

n8n:

Month:
2026-01

Revenue:
Rp10.463.250.000

Status:

✅ MATCH

Lowest Revenue Month

MASTER:

Month:
2026-07

Revenue:
Rp2.713.750.000

n8n:

Month:
2026-07

Revenue:
Rp2.713.750.000

Status:

✅ MATCH

4.5 Sales Growth Pattern Validation

n8n produced:

Analysis period : 13 months

Increasing months:
7

Decreasing months:
5

Unchanged months:
0

Status:

✅ PASS

PART 4 SUMMARY
Monthly Trend Reconciliation Result
Audit Area Status
Monthly Revenue ✅ PASS
Monthly Transaction Count ✅ PASS
Monthly Unit Sold ✅ PASS
Highest Revenue Month ✅ PASS
Lowest Revenue Month ✅ PASS
Sales Trend Pattern ✅ PASS
Finding Update
FINDING SALES-003

Title:
Monthly Sales Trend Consistency Validation

Status:
✅ COMPLETED

Evidence:

MASTER and n8n show:

Peak Sales:
2026-01
Rp10.463.250.000

Lowest Sales:
2026-07
Rp2.713.750.000

Conclusion:

No differences were found in the monthly sales pattern.

PART 4 Conclusion

The time series analysis from MASTER SALES and n8n SALES PIPELINE shows the same results.

Validation confirms:

✅ same periods
✅ same monthly revenue
✅ same best month
✅ same lowest month
✅ same sales trend

PART 5 — CUSTOMER SALES RECONCILIATION
5.1 Validation Objective

To validate customer analysis results between:

MASTER SALES
VS
n8n SALES PIPELINE

Validation covers:

Unique customer count
Total customer purchases
Customer transaction frequency
Top customer ranking
Customer segmentation
Customer revenue contribution

5.2 Source File
A. MASTER SALES

File:

D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv

Columns:

id_pelanggan
nama_pelanggan
id_transaksi
jumlah
total_harga

Function:

Reference Customer Transaction Dataset

B. n8n CUSTOMER ANALYSIS OUTPUT

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_04_CUSTOMER_Professional_n8n.csv

Result:

Customer Analysis Output

Columns:

ranking
id_pelanggan
nama_pelanggan
total_pembelian
frekuensi_transaksi
jumlah_produk_dibeli
kategori_customer

C. n8n CUSTOMER SEGMENTATION OUTPUT

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_04_CUSTOMER_SEGMENTATION_Professional_n8n.csv

Columns:

id_pelanggan
nama_pelanggan
total_pembelian
frekuensi_transaksi
jumlah_produk_dibeli
ranking
segment

5.3 Customer Count Validation
MASTER SALES

Calculation result:

Unique Customer:
1848

n8n CUSTOMER ANALYSIS

Result:

Total Customer:
1848

Evidence #8 — Customer Count Match
Parameter MASTER n8n Status
Unique Customer 1.848 1.848 ✅ PASS

5.4 Customer Revenue Validation
Top Customer MASTER

Result:

Ranking Customer Total Purchase
1 Ratih Lailasari, S.E. Rp317.500.000
2 dr. Jati Manullang, S.T. Rp282.250.000
3 T. Prayogo Budiman Rp275.750.000

Top Customer n8n

Result:

Ranking Customer Total Purchase
1 Ratih Lailasari, S.E. Rp317.500.000
2 dr. Jati Manullang, S.T. Rp282.250.000
3 T. Prayogo Budiman Rp275.750.000

Evidence #9 — Customer Revenue Ranking Match

Status:

✅ PASS

Validation:

Top customer is the same
Purchase value is the same
Ranking is the same

5.5 Customer Segmentation Validation
n8n Customer Segmentation Result

Result:

Segment Customer Count
High Value Customer 251
Medium Value Customer 553
Low Value Customer 1.044

Total:

251 + 553 + 1044 = 1848 customers

Evidence #10 — Customer Segment Validation

Status:

✅ PASS

Segmentation was successfully performed based on customer purchase value.

5.6 Customer Revenue Contribution

n8n Result:

Segment Revenue Contribution
High Value Customer Rp39.192.750.000 35.51%
Medium Value Customer Rp47.579.250.000 43.10%
Low Value Customer Rp23.608.250.000 21.39%

Business Insight

Customer with the largest contribution:

Medium Value Customer

Revenue:
Rp47.579.250.000

Contribution:
43.10%

Premium customer:

High Value Customer

Revenue:
Rp39.192.750.000

Contribution:
35.51%

PART 5 SUMMARY
Customer Reconciliation Result
Audit Area Status
Unique Customer Count ✅ PASS
Customer Revenue ✅ PASS
Top Customer Ranking ✅ PASS
Customer Segmentation ✅ PASS
Revenue Contribution ✅ PASS

Finding Update
FINDING SALES-004

Title:
Customer Analytics Consistency Validation

Status:
✅ COMPLETED

Evidence:

MASTER and n8n produce:

Total Customer:
1848

Top Customer:

Ratih Lailasari, S.E.

Revenue:
Rp317.500.000

Segment:

High Value : 251
Medium Value : 553
Low Value : 1044

Conclusion PART 5

The customer analytics results from MASTER SALES and n8n SALES PIPELINE are consistent.

No:

✅ missing customers
✅ changes in customer ranking
✅ changes in customer revenue
✅ differences in segmentation

PART 6 — FINAL RECONCILIATION SUMMARY & AUDIT CONCLUSION
6.1 Audit Scope

The reconciliation was performed to ensure consistency between:

MASTER LAYER
VS
n8n PROCESSING PIPELINE

Validated scope:

Sales Overview
Monthly Sales Trend
Product Sales Performance
Product Movement Analysis
Customer Analysis
Customer Segmentation

6.2 Evidence Files Used
MASTER SOURCE
MASTER SALES FILE
D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv

Status:

PRIMARY REFERENCE DATASET

Information:

Parameter Value
Rows 5.000
Columns 14
Total Transaction 5.000
Total Unit 27.400
Total Revenue Rp110.380.250.000

n8n Source Files

Clean Data Source
D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

Validation:

Parameter Value
Rows 5.000
Columns 14
Revenue Rp110.380.250.000
Unit 27.400

Status:

✅ MATCH MASTER

Sales Analysis Output
D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv

Status:

✅ Generated Successfully

Product Performance Output
D:\Project_01_Data_Analyst\OUTPUT\DATA\Product_Sales_Performance_Report.csv

Status:

✅ Generated Successfully

Product Movement Output
D:\Project_01_Data_Analyst\OUTPUT\DATA\Product_Movement_Analysis.csv

Status:

✅ Generated Successfully

Customer Analysis Output
D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_04_CUSTOMER_Professional_n8n.csv

Status:

✅ Generated Successfully

Customer Segmentation Output
D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_04_CUSTOMER_SEGMENTATION_Professional_n8n.csv

Status:

✅ Generated Successfully

6.3 Final KPI Reconciliation
Sales KPI
Metric MASTER n8n Status
Transaction 5.000 5.000 ✅ PASS
Revenue Rp110.380.250.000 Rp110.380.250.000 ✅ PASS
Unit Sold 27.400 27.400 ✅ PASS

6.4 Product Validation Summary

Validation:

Best-selling product by units
Product with the highest revenue
Product ranking

Result:

Validation Result
Top Product Laptop Lenovo
Highest Unit 10.772
Highest Revenue Rp91.562.000.000

Status:

✅ PASS

6.5 Customer Validation Summary

Validation:

Customer count
Customer ranking
Customer segmentation

Result:

Metric Result
Total Customer 1.848
High Value Customer 251
Medium Value Customer 553
Low Value Customer 1.044

Status:

✅ PASS

6.6 Finding Register Update
FINDING-001
Dataset Revenue Difference

Initial finding:

Manual Python Revenue
Rp110.380.250.000

n8n Legacy Output
Rp104.902.500.000

Difference:

Rp5.477.750.000

Investigation Result

Root Cause:

Legacy File Path Mismatch

Old reference:

/app/OUTPUT/Company_Cleaned_n8n.csv

Current canonical:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

Finding Status

✅ COMPLETED

Evidence:

Current n8n dataset:

Rows:
5000

Revenue:
Rp110.380.250.000

Unit:
27400

FINDING-002
Output Filename Collision

Finding:

The SALES script used the same output filename for several processes:

Initially:

ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv

used for:

Sales Output
Customer Analysis
Customer Segmentation

Correction

Outputs were separated:

Sales:

ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv


Customer:


ODC_Bag8_FinalReport_04_CUSTOMER_Professional_n8n.csv


Segmentation:


ODC_Bag8_FinalReport_04_CUSTOMER_SEGMENTATION_Professional_n8n.csv


Status:


✅ COMPLETED


6.7 Final Audit Result
MASTER vs n8n SALES PIPELINE
Module Status
Dataset Validation ✅ PASS
Sales KPI ✅ PASS
Monthly Sales ✅ PASS
Product Analysis ✅ PASS
Product Movement ✅ PASS
Customer Analysis ✅ PASS
Customer Segmentation ✅ PASS
Revenue Validation ✅ PASS

FINAL CONCLUSION

Based on the reconciliation results:

MASTER SALES
=
n8n SALES PIPELINE

with the following results:

Transaction : 5,000
Unit : 27,400
Revenue : Rp110.380.250.000
Customer : 1.848

Therefore:

FINAL STATUS
✅ RECONCILIATION MASTER vs n8n SALES = COMPLETED

Audit Evidence Stored

Documentation locations:

D:\Project_01_Data_Analyst\OUTPUT\MASTER

and

D:\Project_01_Data_Analyst\OUTPUT\DATA

PART 7 — AUDIT TRAIL, LESSON LEARNED & RECOMMENDATION

7.1 Audit Trail Summary

Audit trail objective:

Ensure that every change, validation, and correction has traceable evidence.

Data flow:

DATA RAW
|
v
n8n PROCESSING PIPELINE
|
v
Company_Data_Cleaned_n8n.csv
|
v
SALES ANALYSIS
|
+--> Product Analysis
|
+--> Product Movement
|
+--> Customer Analysis
|
+--> Customer Segmentation
|
v
MASTER VALIDATION

7.2 Historical Finding Tracking

FINDING-001
Revenue Difference Between Manual / n8n Legacy Output

Initial Finding

A difference was identified:

Source Revenue
Manual Python / Current Dataset Rp110.380.250.000
n8n Legacy Dataset Rp104.902.500.000

Difference:

Rp5.477.750.000

Investigation Evidence

The investigation found:

Legacy file:

/app/OUTPUT/Company_Cleaned_n8n.csv

used an older dataset.

Current canonical file:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

contains:

Rows : 5000
Revenue : Rp110.380.250.000
Units : 27400

Final Status
✅ COMPLETED

Evidence:

The canonical dataset is consistent with MASTER SALES.

FINDING-002
Output File Collision

Initial Condition

Several processes used the same file name:

ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv

Impact:

Sales Output was overwritten
Customer Analysis was overwritten
Customer Segmentation was overwritten

Root Cause

The script used the same output variable:

segment_csv = os.path.join(
    OUTPUT_DATA,
    "ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv"
)

Correction

Outputs were separated into:

Sales Output
ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv

Customer Output
ODC_Bag8_FinalReport_04_CUSTOMER_Professional_n8n.csv

Customer Segmentation Output
ODC_Bag8_FinalReport_04_CUSTOMER_SEGMENTATION_Professional_n8n.csv

Final Status
✅ COMPLETED

7.3 Data Quality Validation

Data quality validation:

Parameter Result Status
Duplicate Transaction 0 ✅ PASS
Missing Critical Field 0 ✅ PASS
Transaction Count 5000 ✅ PASS
Revenue Consistency Match ✅ PASS
Customer Count 1848 ✅ PASS

7.4 Pipeline Reliability Assessment

Before Improvement

Issues:

❌ Inconsistent paths

Example:

/app/OUTPUT

vs

D:\Project_01_Data_Analyst\OUTPUT

❌ Output file overlap

❌ Historical artifacts causing confusion during the audit process

After Improvement

Improvements:

✅ Canonical path defined

OUTPUT/DATA

✅ Output for each module separated

✅ MASTER used as the validation layer

✅ All findings stored as audit history

7.5 Recommendation

Recommendation 1
File Path Standardization

All scripts should use a single configuration:

Example:

BASE_PATH = "D:/Project_01_Data_Analyst"


OUTPUT_DATA = BASE_PATH + "/OUTPUT/DATA"


OUTPUT_MASTER = BASE_PATH + "/OUTPUT/MASTER"

Objective:

Avoid path mismatches
Simplify deployment

Recommendation 2
Unique Naming Convention

Use the format:

MODULE_PROCESS_VERSION_DATE

Example:

SALES_ANALYSIS_n8n_v1_20260805.csv

Objective:

Avoid overwriting
Facilitate tracking

Recommendation 3
Automated Reconciliation Check

Add automated validation:

Example:

IF MASTER_REVENUE == N8N_REVENUE


STATUS = PASS


ELSE


STATUS = INVESTIGATION

Recommendation 4
Maintain Evidence Repository

Structure:

OUTPUT
 |
 +-- MASTER
 |
 +-- DATA
 |
 +-- AUDIT
 |
 +-- REPORT
 |
 +-- ARCHIVE

All evidence remains stored.

7.6 Final Audit Statement

Based on all evidence:

MASTER SALES
=
n8n SALES PIPELINE

Final validation:

Area Status
Transaction Data ✅ PASS
Revenue ✅ PASS
Product Analysis ✅ PASS
Customer Analysis ✅ PASS
Segmentation ✅ PASS
Data Quality ✅ PASS
Audit Trail ✅ PASS

FINAL STATUS
🟢 MASTER vs n8n SALES RECONCILIATION
COMPLETED

Audit Evidence Available:

MASTER:
D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER

n8n:
D:\Project_01_Data_Analyst\OUTPUT\DATA

Scripts:
D:\Project_01_Data_Analyst\SCRIPT

Archive:
D:\Project_01_Data_Analyst\ARCHIVE

PART 8 — FINAL EVIDENCE REGISTER & HANDOVER DOCUMENTATION

8.1 Evidence Repository Structure

All reconciliation evidence is stored in the following structure:

D:\Project_01_Data_Analyst


|
+-- OUTPUT
|    |
|    +-- MASTER
|    |     |
|    |     +-- SALES_MASTER
|    |
|    +-- DATA
|    |
|    +-- AUDIT
|    |
|    +-- REPORT
|
+-- SCRIPT
|
+-- ARCHIVE

8.2 MASTER Evidence Register

MASTER SALES Dataset

File:

D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv

Function:

Reference Dataset

Validation:

Parameter Result
Total Row 5.000
Total Column 14
Total Transaction 5.000
Total Unit 27.400
Total Revenue Rp110.380.250.000

Status:

✅ VERIFIED

8.3 n8n Evidence Register

A. Clean Dataset

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

Validation:

Parameter Result
Rows 5.000
Revenue Rp110.380.250.000
Unit 27.400

Status:

✅ VERIFIED

B. Sales Analysis Output

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv

Contains:

Sales KPI
Monthly Trend
Sales Comparison

Status:

✅ GENERATED

C. Product Performance Evidence

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Product_Sales_Performance_Report.csv

Validation:

Top Product:

Laptop Lenovo

Unit:

10.772

Revenue:

Rp91.562.000.000

Status:

✅ PASS

D. Product Movement Evidence

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Product_Movement_Analysis.csv

Validation:

Fast Moving Product
Slow Moving Product
Revenue Ranking

Status:

✅ PASS

E. Customer Analysis Evidence

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_04_CUSTOMER_Professional_n8n.csv

Validation:

Parameter Result
Customer Count 1.848
Top Customer Ratih Lailasari, S.E.
Revenue Rp317.500.000

Status:

✅ PASS

F. Customer Segmentation Evidence

File:

D:\Project_01_Data_Analyst\OUTPUT\DATA\ODC_Bag8_FinalReport_04_CUSTOMER_SEGMENTATION_Professional_n8n.csv

Segment Result:

Segment Count
High Value Customer 251
Medium Value Customer 553
Low Value Customer 1.044

Status:

✅ PASS

8.4 Reconciliation Evidence Matrix

No Validation Area MASTER n8n Status
1 Transaction Count 5000 5000 ✅ PASS
2 Revenue 110.380B 110.380B ✅ PASS
3 Unit Sold 27400 27400 ✅ PASS
4 Product Ranking Match Match ✅ PASS
5 Customer Count 1848 1848 ✅ PASS
6 Top Customer Match Match ✅ PASS
7 Segmentation Match Match ✅ PASS

8.5 Audit Finding Final Register

Finding ID Description Status
FINDING-001 Revenue Difference Legacy Dataset ✅ COMPLETED
FINDING-002 Output Filename Collision ✅ COMPLETED

8.6 Handover Checklist

Before the project is declared complete:

Checklist Status
Source file identified ✅
MASTER created ✅
n8n output validated ✅
Revenue reconciled ✅
Customer validated ✅
Product validated ✅
Finding documented ✅
Evidence stored ✅

8.7 Final Handover Statement

Based on the entire validation process:

MASTER SALES DATA
|
|
V
n8n SALES PIPELINE OUTPUT

has been reconciled and produced:

Transaction : 5.000
Unit : 27.400
Revenue : Rp110.380.250.000
Customer : 1.848

No data differences were found between:

MASTER
VS
n8n CURRENT PIPELINE

FINAL PROJECT STATUS
🟢 COMPLETED

Final Documentation Available:

RECONCILIATION
MASTER SALES vs n8n SALES PIPELINE

Version:

FINAL

Status:

AUDIT READY

PART 9 — EXECUTIVE SUMMARY

9.1 Project Overview

Project Name

Sales Data Reconciliation & Validation

Objective

Validate data consistency between:

MASTER SALES DATA

    VS

n8n SALES ANALYTICS PIPELINE

Main objectives:

Ensure sales report accuracy
Ensure the automation pipeline produces correct data
Identify the causes of data discrepancies
Provide traceable audit evidence

9.2 Executive Result

Based on the reconciliation process:

STATUS:
🟢 PASS — DATA VALIDATED

The results show:

MASTER SALES
=
n8n SALES PIPELINE

9.3 Business KPI Validation

Sales Performance

KPI Result
Total Transaction 5.000
Total Unit Sold 27.400
Total Revenue Rp110.380.250.000
Average Transaction Value Rp22.076.050

Status:

✅ VALIDATED

9.4 Sales Performance Insight

Best Sales Period

The period with the highest revenue:

January 2026

Revenue:

Rp10.463.250.000

Number of transactions:

454 transactions

Number of products:

2.471 units

Lowest Sales Period

The lowest period:

July 2026

Revenue:

Rp2.713.750.000

Number of transactions:

126 transactions

9.5 Product Business Insight

Top Revenue Product

Product:

Laptop Lenovo

Performance:

Metric Value
Unit Sold 10.772
Revenue Rp91.562.000.000

Conclusion:

Laptop Lenovo is the company's main revenue contributor.

9.6 Customer Business Insight

Customer Database

Total customers:

1.848 Customer

Customer Segmentation

Segment Customer Contribution
High Value Customer 251 35.51%
Medium Value Customer 553 43.10%
Low Value Customer 1.044 21.39%

Highest Value Customer

Customer:

Ratih Lailasari, S.E.

Total Purchase:

Rp317.500.000

9.7 Issue Resolution Summary

Two main issues were identified during the audit.

Issue 1 — Revenue Difference

Problem

Revenue difference:

Rp5.477.750.000

Root Cause

The legacy dataset used the old path:

/app/OUTPUT/Company_Cleaned_n8n.csv

Resolution

Using the canonical dataset:

Company_Data_Cleaned_n8n.csv

Result:

Revenue:
Rp110.380.250.000

Status:

✅ RESOLVED

Issue 2 — Output File Collision

Problem

Several processes wrote their output to the same file.

Impact:

Output was overwritten
Audit trail was unclear

Resolution

Output separation:

SALES OUTPUT

CUSTOMER OUTPUT

CUSTOMER SEGMENTATION OUTPUT

Status:

✅ RESOLVED

9.8 Data Reliability Assessment

Area Status
Data Accuracy 🟢 PASS
Data Completeness 🟢 PASS
Revenue Validation 🟢 PASS
Customer Validation 🟢 PASS
Product Validation 🟢 PASS
Pipeline Reliability 🟢 PASS

9.9 Management Recommendation

Maintain MASTER Layer

MASTER is used as:

Reference Data
Validation Layer
Audit Evidence

Implement Automated Reconciliation

Add an automated check:

Revenue MASTER
=
Revenue PIPELINE

If different:

Trigger Investigation

Improve Pipeline Governance

Standardize:

File naming
Folder structure
Version control
Evidence storage

9.10 Final Management Statement

Based on the reconciliation results:

MASTER SALES DATA

and

n8n SALES PIPELINE

have been validated and produce consistent data.

Final KPI:

Transaction : 5.000
Unit : 27.400
Revenue : Rp110.380.250.000
Customer : 1.848

FINAL PROJECT STATUS
🟢 APPROVED
MASTER vs n8n SALES RECONCILIATION
COMPLETED & AUDIT READY

PART 10 — TECHNICAL APPENDIX & REPRODUCIBILITY EVIDENCE

10.1 Technical Validation Objective

Objective:

Ensure that the reconciliation results can be reproduced using:

The same source file
The same script
The same command
The same result

Principle:

id="0q1p9f"
SAME INPUT
    +
SAME PROCESS
    =
SAME RESULT

10.2 Environment Validation

Operating Environment

Component Value
Operating System Windows
Python Python 3.12
Data Processing Pandas
Automation Pipeline n8n
Container Environment Docker

10.3 Project Directory Structure

Main location:

D:\Project_01_Data_Analyst

Structure:

Project_01_Data_Analyst


|
+-- DATA_RAW
|
+-- DATABASE
|
+-- SCRIPT
|
+-- OUTPUT
|     |
|     +-- DATA
|     |
|     +-- MASTER
|     |
|     +-- AUDIT
|     |
|     +-- REPORT
|
+-- ARCHIVE

10.4 Script Evidence

Main SALES script:

D:\Project_01_Data_Analyst\SCRIPT\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.py

Function:

id="t6hs0u"
1. Read Clean Dataset
2. Sales KPI Calculation
3. Monthly Sales Analysis
4. Product Performance
5. Product Movement
6. Customer Analysis
7. Customer Segmentation
8. Generate Output Report

10.5 Execution Command Evidence

Command:

py D:\Project_01_Data_Analyst\SCRIPT\ODC_Bag8_FinalReport_02_SALES_Professional_n8n.py

Result:

SALES ANALYSIS n8n

File successfully read

Data Count : 5000
Column Count : 14

Status:

✅ SUCCESS

10.6 MASTER Validation Command

Command:

py -c "import pandas as pd; f=r'D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv'; df=pd.read_csv(f); print(df.shape); print('TOTAL TRANSAKSI:',df['id_transaksi'].count()); print('TOTAL OMZET:',df['total_harga'].sum()); print('TOTAL UNIT:',df['jumlah'].sum())"

Result:

Rows:
5000

Total Transaction:
5000

Total Revenue:
110380250000

Total Unit:
27400

Status:

✅ VERIFIED

10.7 n8n Dataset Validation Command

Command:

py -c "import pandas as pd; f=r'D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv'; df=pd.read_csv(f); print(df.shape); print('TOTAL TRANSAKSI:',df['id_transaksi'].count()); print('TOTAL OMZET:',df['total_harga'].sum()); print('TOTAL UNIT:',df['jumlah'].sum())"

Result:

Rows:
5000

Total Transaction:
5000

Total Revenue:
110380250000

Total Unit:
27400

Status:

✅ VERIFIED

10.8 MASTER vs n8n Comparison Command

Command:

py -c "import pandas as pd; master=r'D:\Project_01_Data_Analyst\OUTPUT\MASTER\SALES_MASTER\ODC_Bag8_FinalReport_00_SALES_MASTER.csv'; n8n=r'D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv'; df1=pd.read_csv(master); df2=pd.read_csv(n8n); print('=== MASTER SALES ==='); print('Rows:',len(df1)); print('Omzet:',df1['total_harga'].sum()); print('Unit:',df1['jumlah'].sum()); print(); print('=== n8n CLEAN DATA ==='); print('Rows:',len(df2)); print('Omzet:',df2['total_harga'].sum()); print('Unit:',df2['jumlah'].sum())"

Result:

=== MASTER SALES ===

Rows:
5000

Omzet:
110380250000

Unit:
27400

=== n8n CLEAN DATA ===

Rows:
5000

Omzet:
110380250000

Unit:
27400

Status:

✅ MATCH

10.9 Output Evidence Validation

Sales Output
ODC_Bag8_FinalReport_02_SALES_Professional_n8n.csv

Status:

✅ Generated

Customer Output
ODC_Bag8_FinalReport_04_CUSTOMER_Professional_n8n.csv

Status:

✅ Generated

Customer Segmentation Output
ODC_Bag8_FinalReport_04_CUSTOMER_SEGMENTATION_Professional_n8n.csv

Status:

✅ Generated

10.10 Reproducibility Checklist

Item Status
Source Dataset Available ✅
MASTER Dataset Available ✅
Script Available ✅
Execution Command Available ✅
Output Evidence Available ✅
KPI Match Verified ✅
Finding Documentation Available ✅

10.11 Technical Conclusion

Based on the re-testing:

MASTER SALES CSV

    MATCH

Company_Data_Cleaned_n8n.csv

with the following results:

Transaction : 5000
Unit : 27400
Revenue : Rp110.380.250.000

The pipeline can be reproduced and the results can be verified again.

FINAL TECHNICAL STATUS
🟢 REPRODUCIBLE & VERIFIED



