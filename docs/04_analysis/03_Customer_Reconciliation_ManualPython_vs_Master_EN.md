
# CUSTOMER RECONCILIATION REPORT
## Python Manual Analysis VS Customer Master Validation

**Project:** Project_01_Data_Analyst
**Module:** Customer Analysis
**Reconciliation Type:** Manual Python Output VS Master Data
**Status:** ✅ PASS

---

# 1. Objective

This document aims to perform validation and reconciliation between the Customer analysis results produced using the Manual Python process and the Customer Master as the primary data source.

Main objectives:

* Ensure that the customer data resulting from the Python analysis originates from the correct master data.
* Ensure that there are no differences in customer transaction values.
* Ensure that customer purchase values are consistent with the master.
* Ensure that customer segmentation results have been calculated consistently.

---

# 2. Compared Files

## A. Manual Python Customer Report

Location:

```text
D:\Project_01_Data_Analyst\OUTPUT\REPORT\ODC_Bag8_FinalReport_04_CUSTOMER.xlsx
```

Sheets used:

| Sheet             | Function                                               |
| ----------------- | ------------------------------------------------------ |
| Customer_Ranking  | Top Customer analysis based on purchase value          |
| Customer_Churn    | Customer status analysis based on transaction activity |
| Customer_Category | Customer segmentation summary                          |

---

## B. Customer Master

Location:

```text
D:\Project_01_Data_Analyst\OUTPUT\MASTER\CUSTOMER_MASTER\ODC_Bag8_FinalReport_00_CUSTOMER_MASTER.xlsx
```

Sheets used:

| Sheet              | Function                |
| ------------------ | ----------------------- |
| Customer_Master    | Main customer data      |
| Data_Quality_Check | Data quality validation |

---

# 3. Reconciliation Method

The method used:

1. Comparing customers based on:

```text
id_pelanggan
nama_pelanggan
```

2. Performing KPI validation:

* Total purchases
* Number of transactions
* Total product items
* Last transaction date
* Customer segmentation

3. Each value is compared between:

```text
Manual Python
        VS
Customer Master
```

Status assigned:

* MATCH / PASS
* NOT MATCH / FAIL

---

# 4. Customer Ranking Validation

## Scope

Sheet:

```text
Customer_Ranking
```

contains:

* Top 10 Customers based on the highest purchases.

Data volume:

| Source                |        Quantity |
| --------------------- | --------------: |
| Manual Python Ranking |    10 Customers |
| Customer Master       | 1,848 Customers |

Because Manual only takes the Top 10, validation is performed by locating those customers in the Customer Master.

---

## Field Mapping

| Manual Python        | Customer Master |
| -------------------- | --------------- |
| id_pelanggan         | id_pelanggan    |
| nama_pelanggan       | nama_pelanggan  |
| total_pembelian      | total_pembelian |
| frekuensi_transaksi  | total_transaksi |
| jumlah_produk_dibeli | total_item      |

---

## Result

Validation was performed on the 10 highest-ranked customers.

Result:

| KPI                   | Result |
| --------------------- | ------ |
| Customer ID           | PASS   |
| Customer Name         | PASS   |
| Total Purchases       | PASS   |
| Transaction Frequency | PASS   |
| Products Purchased    | PASS   |

Evidence:

```text
10 / 10 customers successfully found
All KPI values are identical

Overall PASS = True
```

Status:

```text
CUSTOMER RANKING : PASS ✅
```

---

# 5. Customer Churn Validation

## Scope

Sheet:

```text
Customer_Churn
```

Data volume:

| Source                       |  Rows |
| ---------------------------- | ----: |
| Manual Python Customer Churn | 1.848 |
| Customer Master              | 1.848 |

---

## Field Mapping

| Manual Python      | Customer Master    |
| ------------------ | ------------------ |
| id_pelanggan       | id_pelanggan       |
| nama_pelanggan     | nama_pelanggan     |
| jumlah_transaksi   | total_transaksi    |
| total_pembelian    | total_pembelian    |
| transaksi_terakhir | transaksi_terakhir |

---

## Validation Result

| Validation                  |        Result |
| --------------------------- | ------------: |
| Transaction Match           | 1.848 / 1.848 |
| Purchase Match              | 1.848 / 1.848 |
| Last Transaction Date Match | 1.848 / 1.848 |

Evidence:

```text
Transaksi_Match = 1848
Pembelian_Match = 1848
Tanggal_Match   = 1848

Overall PASS = True
```

Status:

```text
CUSTOMER CHURN : PASS ✅
```

---

# 6. Customer Category Validation

## Objective

Ensure that the customer segmentation results are consistent with the aggregation results from Customer Churn data.

Categories:

1. Active Customer
2. At-Risk Customer
3. Inactive Customer

---

## Validation Method

Recalculation was performed:

```text
Customer_Churn
        |
        |
     GROUP BY kategori
        |
        |
 compared with
 Customer_Category
```

---

## Result

| Category          | Number of Customers |  Total Purchases | Total Transactions | Status |
| ----------------- | ------------------: | ---------------: | -----------------: | ------ |
| Active Customer   |                 691 | Rp49.641.250.000 |              2.278 | PASS   |
| At-Risk Customer  |                 734 | Rp42.526.500.000 |              1.957 | PASS   |
| Inactive Customer |                 423 | Rp18.212.500.000 |                765 | PASS   |

---

Evidence:

```text
Customer_Match  = True
Pembelian_Match = True
Transaksi_Match = True

Overall PASS = True
```

Status:

```text
CUSTOMER CATEGORY : PASS ✅
```

---

# 7. Final Reconciliation Summary

| Module            | Status |
| ----------------- | ------ |
| Customer Ranking  | ✅ PASS |
| Customer Churn    | ✅ PASS |
| Customer Category | ✅ PASS |

---

# 8. Audit Conclusion

Based on the reconciliation process:

* Manual Python customer data is consistent with the Customer Master.
* No differences were found in transaction values.
* No differences were found in total purchases.
* No differences were found in the last transaction dates.
* Customer segmentation has been validated through recalculation.

Final conclusion:

```text
========================================
CUSTOMER RECONCILIATION RESULT
========================================

FINAL STATUS : PASS ✅

No discrepancy detected.
========================================
```

---

# 9. Audit Evidence

Validation sources:

```text
Manual Python:
ODC_Bag8_FinalReport_04_CUSTOMER.xlsx

Master:
ODC_Bag8_FinalReport_00_CUSTOMER_MASTER.xlsx
```

Method:

```text
Python Pandas Reconciliation
Data Matching
Aggregation Validation
KPI Comparison
```

Audit Date:

```text
2026
```
