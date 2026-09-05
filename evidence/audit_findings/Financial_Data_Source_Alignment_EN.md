AUDIT FINDING — FINANCIAL DATA SOURCE ALIGNMENT

Finding ID:
FINANCIAL-001

Title:
Financial Data Source and Grain Misalignment between Manual Python and n8n

Date:
30 July 2026

Status:
OPEN — IMPROVEMENT REQUIRED

Priority:
MEDIUM

Audit Classification:
Data Source Alignment / Data Grain / Data Lineage

============================================================

EXECUTIVE SUMMARY
============================================================

During the Financial Analysis reconciliation process, a difference
was identified between the revenue calculated using transaction-level
data in Manual Python and the revenue used by Financial
Analysis in n8n.

Reconciliation result:

Source Total Revenue

Manual Python Rp110.380.250.000
n8n Financial Analysis Rp104.902.500.000
Difference Rp5.477.750.000

Difference:

Rp5.477.750.000

This finding does not indicate that the entire Financial Analysis
n8n is internally incorrect.

The main issue identified is that the data source and
granularity used by Financial Analysis n8n are not fully aligned
with the validated transaction-level data used as the basis for
Manual Python calculation.

Therefore, the issue is classified as:

DATA SOURCE / DATA GRAIN ALIGNMENT ISSUE

not as:

arithmetic calculation error,
database corruption,
or evidence that the entire transaction data experienced
data loss in the latest dataset condition.
============================================================
2. AUDIT OBJECTIVE

The audit was conducted to ensure that:

the revenue data source can be traced;
the data grain used by each process can be identified;
the revenue difference can be reconciled;
no misinterpretation occurs regarding the data source;
Financial Analysis uses an appropriate data source;
there is a clear Single Source of Truth for financial
calculation;
the recommendation can be technically implemented and
fully supported.
============================================================
3. RECONCILIATION RESULT

Main comparison:

Parameter Manual Python n8n

Calculation Grain Transaction Level Aggregated
Source Validated Data Product Analysis Output
Total Revenue Rp110.380.250.000 Rp104.902.500.000
Difference Rp5.477.750.000

Status:

⚠️ DIFFERENCE IDENTIFIED

============================================================
4. MANUAL PYTHON FINANCIAL SOURCE

Manual Python uses transaction-level calculation as the basis for
financial calculation.

Transaction-level calculation allows revenue to be calculated
directly based on validated transactions.

With this approach, all transactions become the basis for
revenue calculation.

Result:

Total Transaction:
5.000

Total Unit:
27.400

Total Revenue:
Rp110.380.250.000

Status:

✅ PASS

Basis:

Validated Transaction Data

============================================================
5. n8n FINANCIAL SOURCE

Financial Analysis in n8n uses processed/product-level aggregated
results as one of the sources for the financial output calculation.

During the Product Analysis process, aggregation was found to be
based on:

nama_produk

Evidence from script:

ODC_Bag8_FinalReport_03_PRODUCT_Professional_n8n.py

Source code inspection result:

49: df.groupby("nama_produk")

119-120:
df.groupby(
["nama_produk"],

187-188:
df.groupby(
["nama_produk"],

253-254:
df.groupby(
["nama_produk"],

This finding indicates that Product Professional Analysis
uses:

PRODUCT NAME LEVEL

as the aggregation grain.

Meanwhile, validated transaction calculation uses:

TRANSACTION LEVEL

as the calculation grain.

============================================================
6. DATA GRAIN COMPARISON

Manual Python:

TRANSACTION LEVEL
↓
Transaction calculation
↓
Revenue
↓
Rp110.380.250.000

n8n Product / Financial Path:

TRANSACTION DATA
↓
PRODUCT AGGREGATION
↓
Product-level output
↓
Financial Analysis
↓
Rp104.902.500.000

Therefore, the two processes do not use exactly the same grain
as the calculation basis.

============================================================
7. EVIDENCE OF REVENUE DIFFERENCE

The reconciliation result shows:

Manual Python:

Rp110.380.250.000

n8n:

Rp104.902.500.000

Difference:

Rp5.477.750.000

This difference must be reconciled before the two financial
outputs can be declared fully aligned.

============================================================
8. RELATIONSHIP WITH HISTORICAL 4,745-ROW DATA

During the previous investigation, a historical artifact was
identified:

Company_Data_Cleaned_n8n.csv

with the following condition:

Rows:
4.745

Revenue:
Rp104.902.500.000

Meanwhile, the validated RAW Data has:

Rows:
5.000

Revenue:
Rp110.380.250.000

Transaction-level reconciliation against the historical
4,745-row artifact showed:

Missing Transactions:
255

Missing Revenue:
Rp5.477.750.000

The missing revenue value is identical to the revenue difference
between:

Rp110.380.250.000

and

Rp104.902.500.000.

This finding is important evidence in the historical
investigation.

However, based on the source code inspection and latest outputs,
it must not be concluded that Financial Analysis directly
deleted 255 transactions.

Source code investigation shows that:

main.py does not use dropna() to remove transactions;
missing values are handled using fillna();
no transaction deletion filter based on address was found;
FastAPI receives 5,000 rows;
the latest cleaning API output contains 5,000 rows;
the latest revenue output is Rp110.380.250.000.

Therefore:

The 255-row discrepancy is recorded as

HISTORICAL UNEXPLAINED DISCREPANCY

and is not used as evidence that the current cleaning API
causes data loss.

============================================================
9. FINANCIAL LAYER ELIMINATION

The financial layer was also examined through:

ODC_Bag8_FinalReport_07_FINANCE_Professional_n8n.py
Financial_Performance_Report_n8n.csv
ODC_Bag8_FinalReport_07_FINANCE_Professional_n8n.json
FinalAudit_07_Financial_n8n.py

The inspection results show that the financial layer essentially
performs:

data reading;
aggregation/calculation;
result storage;
validation.

No evidence was found indicating that the financial layer
explicitly deletes transactions.

Therefore:

Financial Layer as a data deletion mechanism:

❌ NOT CONFIRMED

Financial Data Source / Grain Alignment Issue:

✅ CONFIRMED

============================================================
10. ROOT CAUSE CLASSIFICATION

The relevant Root Cause for this Finding is:

FINANCIAL DATA SOURCE AND GRAIN MISALIGNMENT

Technically, there is a difference between:

Validated Transaction-Level Data

and

Product-Level Aggregated Data

used in downstream financial analysis.

In addition, a separate Root Cause investigation has identified
an architectural/data-lineage issue involving multiple output
paths and filenames for the logical cleaned dataset.

Therefore, there are two levels of issues that must be
distinguished:

LEVEL 1 — FINANCIAL ALIGNMENT

Financial calculation does not use a source/grain that is
fully consistent with the transaction-level source of truth.

LEVEL 2 — DATA LINEAGE / OUTPUT MANAGEMENT

The management of the cleaned dataset uses multiple physical
paths and filenames, increasing the risk of using a historical
artifact or an incorrect source.

These two issues are related but must not be stated as the same
mechanism.

============================================================
11. WHAT HAS BEEN PROVEN

Based on the available evidence, the following points have been
successfully proven:

Manual Python produces:

Rp110.380.250.000

n8n Financial Analysis produces:

Rp104.902.500.000

Difference:

Rp5.477.750.000

The historical 4,745-row artifact contains:

Rp104.902.500.000

The validated RAW Data contains:

5.000 rows

Rp110.380.250.000

The latest cleaning API output contains:

5.000 rows

Rp110.380.250.000

The Product Professional script uses:

groupby("nama_produk")

Product Professional has the grain:

PRODUCT NAME LEVEL

Transaction-level calculation has the grain:

TRANSACTION LEVEL

The financial source is not yet fully aligned with the
transaction-level source of truth.
============================================================
12. WHAT HAS NOT BEEN PROVEN

The audit did not find sufficient evidence to state that:

The Financial script directly deletes transactions;
main.py currently causes the loss of 255 transactions;
every physical copy currently has different contents;
path differences automatically cause revenue differences;
arithmetic calculation in Financial Analysis is the primary
cause of the difference.

Regarding the latest physical file verification:

The three files currently examined have identical MD5:

fe6e06010a1149b7e9acc5e272c8c487

Therefore, these physical copies currently have identical
byte-for-byte contents.

============================================================
13. IMPACT ASSESSMENT

Impact on data:

No evidence was found that the latest validated transaction dataset
experienced transaction loss.

Status:

✅ PASS

Impact on Financial Alignment:

The n8n Financial KPI is not yet fully aligned with
transaction-level financial calculation.

Status:

⚠️ IMPROVEMENT REQUIRED

Impact on Data Lineage:

Multiple path / filename references increase the risk of:

use of historical artifacts;
use of a non-canonical source;
incorrect downstream references;
tracing difficulties;
differences in results across workflows.

Status:

⚠️ IMPROVEMENT REQUIRED

============================================================
14. SINGLE SOURCE OF TRUTH

It is recommended that:

VALIDATED TRANSACTION DATA

be established as:

SINGLE SOURCE OF TRUTH

for all financial calculations.

Recommended architecture:

RAW DATA
↓
VALIDATION
↓
VALIDATED TRANSACTION DATA
↓
├── Financial Calculation
├── Sales Analysis
├── Product Analysis
└── Customer Analysis

Product aggregation is not eliminated.

Product aggregation remains used for:

Product Contribution Analysis
Product Ranking
Pareto Analysis
Product Performance Analysis

However, product aggregation should not replace the
validated transaction-level source for total financial revenue.

============================================================
15. RECOMMENDED DATA ARCHITECTURE

Canonical data flow:

RAW
↓
VALIDATION
↓
TRANSACTION MASTER
↓
├── SALES MASTER
├── PRODUCT MASTER
├── CUSTOMER MASTER
└── FINANCIAL MASTER

Financial Master must obtain revenue from:

TRANSACTION MASTER

not from historical product aggregation output.

============================================================
16. CORRECTIVE ACTION

Corrective Action 1:

Establish validated transaction data as the canonical
financial source.

Status:

⏳ REQUIRED

Corrective Action 2:

Standardize the output path and filename.

Status:

⏳ REQUIRED

Corrective Action 3:

Establish one canonical cleaned dataset for all
downstream workflows.

Status:

⏳ REQUIRED

Corrective Action 4:

Ensure Product Analysis continues to be used for product
analytics and does not become the primary source for total
financial revenue.

Status:

⏳ REQUIRED

Corrective Action 5:

Re-run Financial Analysis using the canonical
transaction-level source.

Status:

⏳ REQUIRED

Corrective Action 6:

Perform final reconciliation after corrective action.

Status:

⏳ REQUIRED

============================================================
17. VALIDATION MATRIX
Component Status

RAW Data Integrity ✅ PASS
Transaction Data ✅ PASS
Transaction Count ✅ PASS
Total Unit ✅ PASS
Manual Python Revenue ✅ PASS
Historical 4,745-row Artifact ⚠️ HISTORICAL
Historical Revenue Difference ⚠️ IDENTIFIED
Cleaning API Input ✅ PASS
Cleaning API Latest Output ✅ PASS
Financial Calculation ⚠️ MISALIGNED
Product Aggregation Grain ⚠️ DIFFERENT
Data Lineage ⚠️ IMPROVEMENT REQUIRED
Single Source of Truth ⚠️ REQUIRED
Corrective Action ⏳ OPEN

============================================================
18. FINAL AUDIT CONCLUSION

Based on all evidence examined, the Financial Revenue difference
of:

Rp5.477.750.000

between:

Manual Python
Rp110.380.250.000

and:

n8n
Rp104.902.500.000

has been successfully identified and reconciled at the level of
historical data state and data-source/grain alignment.

The audit found no evidence that Financial Analysis directly
deleted transactions.

The audit also found no evidence that the latest cleaning API
produced data loss.

Instead, the evidence shows that:

validated transaction data contains 5,000 transactions and
revenue of Rp110.380.250.000;
the historical 4,745-row artifact contains revenue of
Rp104.902.500.000;
Product Professional Analysis uses
nama_produk as the aggregation key;
transaction-level financial calculation uses
validated transaction data;
there is a data-source and data-grain misalignment in
downstream financial analysis;
there is an architectural/data-lineage issue caused by
multiple output paths and filenames;
the canonical transaction-level source must be established
as the Single Source of Truth for financial calculation.
============================================================
19. FINAL FINDING STATUS

Finding ID:

FINANCIAL-001

Finding:

Financial Data Source and Grain Misalignment

Root Cause Classification:

DATA SOURCE / DATA GRAIN ALIGNMENT ISSUE

Status:

🟡 OPEN — IMPROVEMENT REQUIRED

Priority:

MEDIUM

Confidence:

HIGH — based on source-code inspection,
workflow inspection, physical file verification,
and reconciliation evidence.

============================================================
20. FINAL RECOMMENDATION

The project must establish:

VALIDATED TRANSACTION DATA

as:

SINGLE SOURCE OF TRUTH

for:

Financial Calculation
Revenue Calculation
Financial KPI
Financial Master

Meanwhile:

PRODUCT AGGREGATION

continues to be used for:

Product Ranking
Product Contribution
Pareto Analysis
Product Performance

With this standardization, financial calculation will have
consistent grain, clearer data lineage, and reconciliation
between Manual Python, n8n, Master, and Final Audit can be
performed deterministically and reproducibly.

============================================================
FINAL AUDIT STATEMENT

The investigation into the financial discrepancy was conducted using transaction-level reconciliation, source-code inspection, workflow inspection, and physical file verification.

The available evidence supports a Financial Data Source and Grain Alignment issue as well as a related Data Lineage / Output Management issue.

No sufficient evidence was found to classify the discrepancy as transaction deletion performed by the Financial Layer or the latest Cleaning API.

Therefore, the required improvement is to establish the validated transaction dataset as the canonical financial source and establish one consistent output path for downstream processing.

FINAL STATUS:

🟡 OPEN — IMPROVEMENT REQUIRED

ROOT CAUSE / ALIGNMENT ISSUE IDENTIFIED

CORRECTIVE ACTION REQUIRED

AUDIT EVIDENCE AVAILABLE