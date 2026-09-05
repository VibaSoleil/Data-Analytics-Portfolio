# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 1

**Project:** Project_01_Data_Analyst
**Workflow:** WF_05_Data_Visualization_n8n
**Status Date:** 16 August 2026
**Report Purpose:** Final WF5 report prepared for email delivery

---

## 1. FINAL STATUS & AUDIT CHECKPOINT

| Component                      | Final Status    |
| ------------------------------ | --------------- |
| Current Final Execution Status | 🟢 SUCCESS      |
| Dashboard Generation Status    | 🟢 COMPLETED    |
| Input Validation               | 🟢 PASS         |
| KPI Reconciliation             | 🟢 PASS         |
| Chart Execution                | 🟢 COMPLETED    |
| Regional Analysis              | ⚪ NOT AVAILABLE |
| Output Generation              | 🟢 PASS         |
| Final Audit Status             | 🟢 COMPLETE     |

### Final WF5 Decision

**WF_05_Data_Visualization_n8n**

* **Execution Status:** 🟢 SUCCESS
* **Dashboard Status:** 🟢 COMPLETED
* **Reconciliation Status:** 🟢 PASS
* **Regional Analysis:** ⚪ NOT AVAILABLE
* **Output Status:** 🟢 PASS
* **Final Audit:** 🟢 COMPLETE

---

## 2. EXECUTIVE SUMMARY

WF_05_Data_Visualization_n8n successfully executed the business visualization process using the **canonical cleaned dataset** that was used by the previous workflows.

WF5 aims to transform the canonical data into a business dashboard that can be used to:

* understand revenue trends;
* view product performance;
* view customer contribution;
* view transaction category distribution;
* present Business KPI;
* produce visual business evidence;
* produce a dashboard in PNG and PDF formats.

WF5 **does not perform cleaning on the dataset** and **does not make any changes to the canonical dataset**.

The latest execution successfully ran to completion without traceback and produced:

* Chart 1;
* Chart 2;
* Chart 3;
* Chart 4 as **Regional Analysis = NOT AVAILABLE**;
* Chart 5;
* Chart 6;
* PNG Dashboard;
* PDF Dashboard.

Therefore, operationally, WF5 has successfully completed its execution.

However, the **FINAL AUDIT** status remains distinct from the execution status. The final audit ensures that all displayed visualizations and business conclusions are supported by a defensible data basis.

---

## 3. WORKFLOW STATUS

| Workflow | Function                | Final Status                |
| -------- | ----------------------- | --------------------------- |
| WF1      | Data Extraction         | ✅ COMPLETE / FROZEN         |
| WF2      | Data Cleaning           | ✅ COMPLETE / FROZEN         |
| WF3      | Data Quality Validation | 🟢 COMPLETE / PASS / FROZEN |
| WF4      | Data Analysis Report    | 🟢 COMPLETE / PASS          |
| WF5      | Data Visualization      | 🟢 EXECUTION SUCCESS        |

### Current Project Milestone

**WF1 → COMPLETE / FROZEN**
**WF2 → COMPLETE / FROZEN**
**WF3 → COMPLETE / PASS / FROZEN**
**WF4 → COMPLETE / PASS**
**WF5 → EXECUTION SUCCESS**

---

## 4. WF5 OBJECTIVE

WF5 aims to produce a business visualization dashboard from the **canonical cleaned dataset**.

The visualizations include:

* Monthly Revenue Trend
* Top Product Revenue
* Top Customers
* Regional Analysis handling
* Transaction Category
* Business Summary

In addition to visualizations, WF5 produces:

* Business KPI;
* Business Insights;
* Business Recommendations;
* Data Quality information;
* PNG Dashboard;
* PDF Dashboard.

WF5 uses the data already available and **does not make any changes to the canonical dataset**.

---

### AUDIT INTEGRITY PRINCIPLE

The entire content of this report follows the final WF5 evidence.

This report **does not alter the KPI values, execution status, reconciliation results, business insights, or audit decisions** established by WF5.

**The canonical dataset remains FROZEN and has not been modified.**

**Validation Principle:**

> **Valid Data → Valid Calculation → Valid Visualization → Valid Business Conclusion**

---

**END OF PART 1**

# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 2

---

## 5. CANONICAL INPUT

### Canonical Input File

**File:** `Company_Data_Cleaned_n8n.csv`

**Path:**

`/app/OUTPUT/DATA/Company_Data_Cleaned_n8n.csv`

The file was successfully found and read by the execution within:

`python-project-container`

### Verified Result

| Item    | Result |
| ------- | -----: |
| Rows    |  5,000 |
| Columns |     14 |

### Column Structure

WF5 receives the following 14 columns:

1. `id_transaksi`
2. `tanggal_transaksi`
3. `id_produk`
4. `nama_produk`
5. `harga`
6. `jumlah`
7. `total_harga`
8. `id_pelanggan`
9. `nama_pelanggan`
10. `alamat`
11. `no_telepon`
12. `tanggal_keuangan`
13. `pemasukan`
14. `keterangan`

No column names were changed.

### Result

**CANONICAL INPUT = PASS**

**COLUMN STRUCTURE = PASS**

---

## 6. DATA TYPE PREPARATION

WF5 performs data type preparation for aggregation and visualization purposes.

### Processed Columns

| Column              | Preparation |
| ------------------- | ----------- |
| `tanggal_transaksi` | datetime    |
| `harga`             | numeric     |
| `jumlah`            | numeric     |
| `total_harga`       | numeric     |

The purpose is to ensure that calculation and aggregation are performed using appropriate data types.

### Result

**DATA TYPE PREPARATION = PASS**

---

## 7. BUSINESS KPI

WF5 successfully calculated the Business KPI from the canonical dataset.

| KPI                 |                 Nilai |
| ------------------- | --------------------: |
| Total Revenue       | **Rp110.380.250.000** |
| Total Transactions  |             **5.000** |
| Total Customers     |             **1.848** |
| Total Products      |                 **5** |
| Average Transaction |      **Rp22.076.050** |

The KPI were then reconciled again using command-line verification against:

`OUTPUT\DATA\Company_Data_Cleaned_n8n.csv`

The verification result showed the same values.

### Result

**BUSINESS KPI = PASS**

**KPI RECONCILIATION = PASS**

---

## 8. DATA PERIOD

The transaction period in the canonical dataset:

| Item     | Verified Value |
| -------- | -------------- |
| DATE_MIN | **2025-07-08** |
| DATE_MAX | **2026-07-08** |

WF5 uses `tanggal_transaksi` as the basis for the **Monthly Revenue Trend**.

WF5 does not state any period beyond the available evidence.

### Result

**DATE RANGE = VERIFIED**

---

## AUDIT INTEGRITY NOTE

The canonical input used by WF5 has been verified as:

* **5,000 records**
* **14 columns**
* Column structure consistent with the canonical dataset
* Data type preparation successfully completed
* Business KPI successfully calculated
* KPI successfully reconciled

No changes were made to the canonical dataset.

**Canonical Dataset Status: FROZEN**

---

**END OF PART 2**

# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 3

---

## 9. DATA PREPARATION

WF5 successfully prepared the following analytical data:

### 9.1 Sales Data

Used for:

* monthly revenue;
* transaction count;
* quantity aggregation.

### 9.2 Product Data

Used for:

* unit sold;
* revenue;
* transaction frequency.

### 9.3 Customer Data

Used for:

* customer purchase;
* transaction frequency;
* quantity.

### 9.4 Regional Data

At the initial stage, the script used `alamat` as the basis for regional analysis.

However, the audit subsequently found that:

`alamat`

**is not a dedicated regional field.**

The canonical dataset does not contain a dedicated field for:

* provinsi;
* kota;
* kabupaten;
* region;
* wilayah.

Therefore, regional analysis is not used as a business conclusion.

### Result

**DATA PREPARATION = PASS**

**REGIONAL FIELD AVAILABILITY = NOT AVAILABLE**

---

# 10. CHART 1 — MONTHLY REVENUE TREND

WF5 produced the following visualization:

**Monthly Revenue Trend**

The calculation uses:

* `tanggal_transaksi`
* `total_harga`

The chart was successfully created during the latest execution.

### Result

**CHART 1 = PASS**

---

# 11. CHART 2 — TOP PRODUCT REVENUE

WF5 produced:

**Top Product Revenue**

The aggregation uses:

* `nama_produk`
* `total_harga`

The chart was successfully created.

### Business Verification

**Best Product: Laptop Lenovo**

### Result

**CHART 2 = PASS**

---

# 12. CHART 3 — TOP CUSTOMERS

WF5 produced:

**Top Customers**

The aggregation uses:

* `nama_pelanggan`
* `total_harga`
* `id_transaksi`
* `jumlah`

The chart was successfully created.

### Business Verification

**Best Customer: Paris Novitasari**

### Result

**CHART 3 = PASS**

---

## AUDIT INTEGRITY NOTE

Chart 1, Chart 2, and Chart 3 are based on calculations performed against the verified canonical dataset.

No business conclusion was made beyond the WF5 evidence.

Specifically:

* **Best Product = Laptop Lenovo**
* **Best Customer = Paris Novitasari**

are the results of WF5 business verification.

Regional analysis is **not used** as a business conclusion because a dedicated regional field is not available in the canonical dataset.

---

**END OF PART 3**

# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 4

---

# 13. CHART 4 — REGIONAL ANALYSIS

At the initial stage of WF5, a defect was identified in the regional visualization process.

### Historical Technical Issue

The previous script used:

`alamat`

as the basis for regional information.

Technically, this process caused an issue when the `alamat` values were processed as categorical values for Matplotlib.

However, the audit found that the issue was not only technical.

### Analytical Root Cause

`alamat` is not a dedicated regional field.

The canonical dataset does not provide a dedicated field for:

* region;
* provinsi;
* kota;
* kabupaten;
* wilayah.

Therefore, creating a regional conclusion based on address parsing does not have a sufficiently strong analytical basis.

### Corrective Decision

WF5 applies the following principle:

> **If a dedicated regional field is not available in the canonical dataset, WF5 does not make a regional business conclusion.**

The latest execution produced:

**Regional Analysis: NOT AVAILABLE**

**Reason: No dedicated regional field is available in the canonical dataset.**

### Final Regional Status

**REGIONAL ANALYSIS = NOT AVAILABLE**

This is **not a workflow failure**.

This is an analytical decision to prevent the dashboard from producing a regional conclusion that cannot be properly supported.

### Result

**REGIONAL ANALYSIS = NOT AVAILABLE / DATA FIELD NOT AVAILABLE**

---

# 14. CHART 5 — TRANSACTION CATEGORY

WF5 categorizes transactions based on `total_harga`.

### Classification

| Category | Definition                   |
| -------- | ---------------------------- |
| Small    | `< Rp5.000.000`              |
| Medium   | `Rp5.000.000 – Rp20.000.000` |
| Large    | `> Rp20.000.000`             |

### Independent CMD Verification

| Category  | Transactions |
| --------- | -----------: |
| Small     |    **1.730** |
| Medium    |    **1.552** |
| Large     |    **1.718** |
| **TOTAL** |    **5.000** |

### Reconciliation

**1.730 + 1.552 + 1.718 = 5.000**

Therefore, all 5,000 transactions fall into one of the categories.

### Result

**CHART 5 = PASS**

**TRANSACTION CATEGORY RECONCILIATION = PASS**

---

# 15. CHART 6 — BUSINESS SUMMARY

Business Summary displays KPI and business performance information derived from WF5 calculations.

### Verified Business Summary

| Metric          | Verified Result       |
| --------------- | --------------------- |
| Revenue         | **Rp110.380.250.000** |
| Transactions    | **5.000**             |
| Customers       | **1.848**             |
| Products        | **5**                 |
| Best Product    | **Laptop Lenovo**     |
| Best Customer   | **Paris Novitasari**  |
| Highest Month   | **2026-01**           |
| Highest Revenue | **Rp10.463.250.000**  |
| Lowest Month    | **2026-07**           |
| Lowest Revenue  | **Rp2.713.750.000**   |

**Best Region is not used as a business conclusion**, because a regional field is not available.

### Result

**CHART 6 = PASS**

**BUSINESS SUMMARY = PASS**

---

# 16. BUSINESS INSIGHTS

The following Business Insights were successfully verified:

* **Best Product:** Laptop Lenovo
* **Best Customer:** Paris Novitasari
* **Highest Revenue Month:** 2026-01
* **Highest Monthly Revenue:** Rp10.463.250.000
* **Total Revenue:** Rp110.380.250.000

All of these insights are derived from calculations against the canonical dataset.

No regional insight is used as a final conclusion.

### Result

**BUSINESS INSIGHTS = PASS**

---

## AUDIT INTEGRITY NOTE

WF5 does not make business conclusions based on fields that are not available.

Specifically, WF5 does not claim:

* Best Region;
* Revenue by Region;
* Highest Revenue Region;
* Regional Performance;
* Regional Growth.

**Regional Analysis = NOT AVAILABLE**

This decision is part of the analytical integrity of WF5.

---

**END OF PART 4**

# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 5

---

# 17. BUSINESS RECOMMENDATIONS

WF5 produced the following recommendations:

1. **Maintain stock for best-selling products.**
2. **Increase customer loyalty programs.**
3. **Review sales trends regularly to support marketing decisions.**
4. **Improve customer data quality.**
5. **Monitor sales trend every month.**

Recommendations related to regional expansion are not used after regional analysis was determined to be unavailable.

Therefore, the recommendations are not based on any regional assumption.

### Result

**BUSINESS RECOMMENDATIONS = PASS**

---

# 18. DATA QUALITY INFORMATION

The latest execution produced:

| Data Quality Item | Result |
| ----------------- | -----: |
| Missing Address   |  **0** |
| Missing Phone     |  **0** |

### Repeated Customer Records

The script produced:

**Repeated Customer Records: 4.004**

This value comes from duplicate checking based on the combination of:

* `nama_pelanggan`
* `alamat`

The calculation used by WF5 is a `duplicated` check based on these two fields.

---

## 18.1 IMPORTANT AUDIT INTERPRETATION

The value **4.004 Repeated Customer Records**:

* **Does NOT mean that there are 4.004 duplicate transactions.**
* **Does NOT mean that there are 4.004 invalid transactions.**
* **Does NOT mean that there are 4.004 corrupted transactions.**
* **Does NOT mean that there are 4.004 transactions that must be deleted.**

This metric counts records after the first occurrence that have the same combination of:

**nama_pelanggan + alamat**

as a previous record.

Because the canonical dataset is a **transaction-level dataset**, a customer may make multiple transactions.

As a result, the same customer may appear across multiple transaction records with the same name and address.

Therefore:

> **4.004 Repeated Customer Records ≠ 4.004 Duplicate Transactions**

---

## 18.2 BUSINESS INTERPRETATION

The value **4.004** should be understood as an indicator of:

**repeated customer occurrences across transaction records**

Such repetition can occur normally when the same customer makes more than one purchase.

Therefore, this number is not used to conclude that there are 4.004 transactions that must be deleted or considered data errors.

---

# 18.3 RELATIONSHIP WITH WF3 DATA QUALITY VALIDATION

The WF5 value **must not be equated** with the duplicate validation result from WF3 because the two use different validation definitions.

### WF3 Dedicated Data-Quality Validation

| WF3 Validation            | Result |
| ------------------------- | -----: |
| Duplicate Rows            |  **0** |
| Duplicate Transaction IDs |  **0** |

WF3 remains the basis for the conclusion that no duplicate transaction rows were found according to the WF3 validation rule.

### WF5 Additional Information

| WF5 Metric                |    Result |
| ------------------------- | --------: |
| Repeated Customer Records | **4.004** |

WF5 uses the subset:

`nama_pelanggan + alamat`

to provide information regarding repeated customer records.

Therefore:

**WF3 Duplicate Rows = 0**  
**WF3 Duplicate Transaction IDs = 0**

remain the basis for duplicate transaction validation.

Meanwhile:

**WF5 Repeated Customer Records = 4.004**

is additional information regarding repeated customer identity across transaction records and **is not a replacement for the WF3 validation result**.

---

# 18.4 AUDIT DECISION

| Audit Item                                    | Final Decision                     |
| --------------------------------------------- | ---------------------------------- |
| Repeated Customer Records                     | **4.004**                          |
| Duplicate Transaction Status from this metric | **NOT CONCLUDED FROM THIS METRIC** |
| Duplicate Transaction Validation              | **BASED ON WF3 RESULT**            |
| WF3 Duplicate Rows                            | **0**                              |
| WF3 Duplicate Transaction IDs                 | **0**                              |
| Master Data Impact                            | **NONE**                           |
| Canonical Dataset Impact                      | **NONE**                           |
| Master Data Status                            | **FROZEN**                         |
| Final Data Quality Interpretation             | **VALID WITH CLARIFICATION**       |

### Required Management Reporting Terminology

For management reporting, the term:

❌ **Duplicate Data: 4.004**

is not used.

The correct term is:

✅ **Repeated Customer Records: 4.004**

And this number **must not be interpreted as 4.004 duplicate transactions**.

---

## AUDIT INTEGRITY NOTE

WF5 maintains the distinction between:

**Customer Record Repetition**

and

**Duplicate Transaction Validation**

This separation of definitions is necessary to ensure that business reporting does not produce a misleading conclusion.

**Master Data Impact: NONE**

**Canonical Dataset Impact: NONE**

**Master Data Status: FROZEN**

---

**END OF PART 5**

# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 6

---

# 19. DASHBOARD EXECUTION RESULT

The latest execution successfully completed all stages:

| Execution Part | Status       |
| -------------- | ------------ |
| PART 1         | 🟢 COMPLETED |
| PART 2         | 🟢 COMPLETED |
| PART 3         | 🟢 COMPLETED |
| PART 3A        | 🟢 COMPLETED |
| PART 3B        | 🟢 COMPLETED |
| PART 3C        | 🟢 COMPLETED |
| PART 4         | 🟢 COMPLETED |

### Chart Execution

| Chart   | Final Status                          |
| ------- | ------------------------------------- |
| Chart 1 | 🟢 COMPLETED                          |
| Chart 2 | 🟢 COMPLETED                          |
| Chart 3 | 🟢 COMPLETED                          |
| Chart 4 | ⚪ NOT AVAILABLE / ANALYTICAL DECISION |
| Chart 5 | 🟢 COMPLETED                          |
| Chart 6 | 🟢 COMPLETED                          |

No traceback occurred during the latest execution.

### Result

**DASHBOARD EXECUTION = SUCCESS**

---

# 20. OUTPUT GENERATION

WF5 successfully generated two dashboard outputs.

### PNG Dashboard

`/app/OUTPUT/DASHBOARD/ODC_Business_Dashboard_n8n.png`

### PDF Dashboard

`/app/OUTPUT/DASHBOARD/ODC_Business_Dashboard_n8n.pdf`

The execution provided the following confirmations:

* **PNG Dashboard Saved**
* **PDF Dashboard Saved**

### Result

**PNG OUTPUT = PASS**

**PDF OUTPUT = PASS**

---

# 21. RECONCILIATION RESULT

WF5 reconciliation was performed against the canonical dataset.

| Item                |               WF5 | Canonical Verification | Result  |
| ------------------- | ----------------: | ---------------------: | ------- |
| Records             |             5.000 |                  5.000 | ✅ MATCH |
| Columns             |                14 |                     14 | ✅ MATCH |
| Revenue             | Rp110.380.250.000 |      Rp110.380.250.000 | ✅ MATCH |
| Transactions        |             5.000 |                  5.000 | ✅ MATCH |
| Customers           |             1.848 |                  1.848 | ✅ MATCH |
| Products            |                 5 |                      5 | ✅ MATCH |
| Average Transaction |      Rp22.076.050 |           Rp22.076.050 | ✅ MATCH |

### Chart 5 Reconciliation

| Category  | Verified Count |
| --------- | -------------: |
| Small     |          1.730 |
| Medium    |          1.552 |
| Large     |          1.718 |
| **TOTAL** |      **5.000** |

### Result

**WF5 KPI RECONCILIATION = PASS**

**CHART 5 RECONCILIATION = PASS**

---

# 22. FINAL AUDIT RESULT

The WF5 final audit includes:

| Component                | Result          |
| ------------------------ | --------------- |
| Canonical Input          | ✅ PASS          |
| 5,000 Records            | ✅ PASS          |
| 14 Columns               | ✅ PASS          |
| Column Structure         | ✅ PASS          |
| Data Type Preparation    | ✅ PASS          |
| Business KPI             | ✅ PASS          |
| KPI Reconciliation       | ✅ PASS          |
| Date Range               | ✅ VERIFIED      |
| Chart 1                  | ✅ PASS          |
| Chart 2                  | ✅ PASS          |
| Chart 3                  | ✅ PASS          |
| Regional Analysis        | ⚪ NOT AVAILABLE |
| Chart 5                  | ✅ PASS          |
| Chart 5 Reconciliation   | ✅ PASS          |
| Chart 6                  | ✅ PASS          |
| Business Insights        | ✅ PASS          |
| Business Recommendations | ✅ PASS          |
| PNG Generation           | ✅ PASS          |
| PDF Generation           | ✅ PASS          |
| Traceback                | ✅ NONE          |
| Final Execution          | 🟢 SUCCESS      |

---

## AUDIT CONCLUSION

Based on the execution and reconciliation results:

* the canonical input was successfully verified;
* the KPI were successfully reconciled;
* Chart 1–3 were successfully completed;
* Regional Analysis was determined to be **NOT AVAILABLE** based on an analytical decision;
* Chart 5 was successfully completed and reconciled;
* Chart 6 was successfully completed;
* Business Insights were successfully verified;
* Business Recommendations were successfully completed;
* the PNG was successfully generated;
* the PDF was successfully generated;
* no traceback occurred during the latest execution.

Therefore:

**FINAL AUDIT STATUS = 🟢 COMPLETE**

---

**END OF PART 6**

# WF_05 — DATA VISUALIZATION

## EMAIL FINAL REPORT — PART 7

---

# 23. FROZEN COMPONENTS

Components that have become part of the previous workflows must remain unchanged.

### Frozen Components

* **WF1**
* **WF2**
* **WF3**
* **Company_Data_Cleaned_n8n.csv**

WF5 only uses the canonical dataset as its input.

WF5 does not make any changes to:

`Company_Data_Cleaned_n8n.csv`

WF2 and WF3 remain in the following status:

**COMPLETE / FROZEN**

WF5 changes are made only to:

`ODC_Bag8_FinalReport_09_DASHBOARD_n8n.py`

and only to correct verified defects or documented controlled enhancements.

---

# 24. AUDIT TRAIL NOTE

At the initial stage of WF5 execution, a defect was identified in:

**Chart 4 — Revenue by Region**

### Historical Issue

The script used:

`alamat`

as the basis for regional analysis.

The execution then produced a Matplotlib error related to non-string categorical values.

### Technical Root Cause

The parsing of `alamat` could produce values that were not suitable for categorical plotting.

### Analytical Root Cause

More fundamentally, the canonical dataset does not have a dedicated regional field.

Therefore, simply converting the data type to string would not be sufficient to produce a valid regional business analysis.

### Corrective Action

Regional analysis was subsequently disabled as a business conclusion.

WF5 uses:

**Regional Analysis: NOT AVAILABLE**

with the following reason:

> **No dedicated regional field is available in the canonical dataset.**

### Verification

After the corrective action:

* the workflow was successfully executed to completion;
* Chart 1 was successfully completed;
* Chart 2 was successfully completed;
* Chart 3 was successfully completed;
* Regional Analysis did not produce an unsupported claim;
* Chart 5 was successfully completed;
* Chart 6 was successfully completed;
* the PNG was successfully generated;
* the PDF was successfully generated;
* no traceback occurred.

### Audit Conclusion

The corrective action successfully resolved the technical defect while maintaining the **analytical integrity** of the dashboard.

---

# 25. FINAL WF5 DECISION

Based on:

* successful execution;
* canonical input verification;
* KPI reconciliation;
* Chart 1–3 verification;
* Regional Analysis handling;
* Chart 5 reconciliation;
* Chart 6 verification;
* business insight verification;
* PNG generation;
* PDF generation;
* absence of traceback;

WF5 has successfully completed its operational execution.

## Current Decision

### 🟢 WF_05_Data_Visualization_n8n

| Final Component       | Status              |
| --------------------- | ------------------- |
| Execution Status      | 🟢 **SUCCESS**      |
| Dashboard Status      | 🟢 **COMPLETED**    |
| Reconciliation Status | 🟢 **PASS**         |
| Regional Analysis     | ⚪ **NOT AVAILABLE** |
| Output Status         | 🟢 **PASS**         |
| Final Audit           | 🟢 **COMPLETE**     |

---

# 26. VALIDATION FRAMEWORK

WF5 uses four validation layers.

## 26.1 Valid Data

Ensures:

* the canonical dataset is correct;
* the number of records is correct;
* the number of columns is correct;
* the source data used is correct.

## 26.2 Valid Calculation

Ensures that all KPI and dashboard calculations are consistent with the reconciled data.

## 26.3 Valid Visualization

Ensures that every displayed chart is consistent with the calculation results and does not present information that is unsupported by the data.

## 26.4 Valid Business Conclusion

Ensures that business insights and recommendations are derived from correct analysis and do not make claims that are unsupported by evidence.

### Validation Chain

**Valid Data → Valid Calculation → Valid Visualization → Valid Business Conclusion**

---

# 27. PROJECT MILESTONE

| Workflow | Final Status                |
| -------- | --------------------------- |
| WF1      | ✅ COMPLETE / FROZEN         |
| WF2      | ✅ COMPLETE / FROZEN         |
| WF3      | 🟢 COMPLETE / PASS / FROZEN |
| WF4      | 🟢 COMPLETE / PASS          |
| WF5      | 🟢 COMPLETE / PASS          |

---

# 28. FINAL AUDIT PRINCIPLE

WF5 does not make business conclusions based on fields that are not available.

Specifically, WF5 does not claim:

* **Best Region**
* **Revenue by Region**
* **Highest Revenue Region**
* **Regional Performance**
* **Regional Growth**

because the canonical dataset does not provide a dedicated regional field.

Therefore, the dashboard maintains the principle:

# **Valid Data → Valid Calculation → Valid Visualization → Valid Business Conclusion**

---

# FINAL WF5 STATEMENT

**WF_05_Data_Visualization_n8n has successfully completed execution, generated the PNG and PDF dashboards, achieved KPI reconciliation PASS, maintained the canonical dataset in a FROZEN state, and completed the final audit while maintaining analytical integrity.**

**Regional Analysis remains designated as NOT AVAILABLE because a dedicated regional field is not available in the canonical dataset.**

**No changes were made to the canonical dataset or to the frozen WF1–WF3 components.**

**Final Status: 🟢 SUCCESS / COMPLETE / PASS**

---

**END OF PART 7**

**END OF WF_05_DATA_VISUALIZATION_EMAIL_FINAL_REPORT_20260817_EN**
