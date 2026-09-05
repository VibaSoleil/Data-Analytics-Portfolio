# 02_Product_Reconciliation_Manual_Python_vs_Master_EN.md

# PRODUCT RECONCILIATION REPORT

## Manual Python vs Master Dataset

---

# Document Information

| Item                | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| Project             | Project_01_Data_Analyst                                     |
| Module              | Product                                                     |
| Reconciliation Type | Manual Python vs Master                                     |
| Document Status     | FINAL                                                       |
| Validation Result   | PASS                                                        |
| Validation Method   | KPI Recalculation, Exact Matching, Business Rule Validation |

---

# 1. Objective

Ce document vise à effectuer la validation et la réconciliation entre l’output de l’analyse Product réalisé à l’aide de Manual Python et le Product Master Dataset.

Objectifs principaux :

* Vérifier la cohérence des KPI Product.
* Vérifier que Product Master peut servir d’audit layer.
* Vérifier que l’ensemble des analyses Product peut être reproduit à partir du Master Dataset.
* Vérifier qu’aucune différence n’existe entre les résultats de l’analyse et la source de données principale.

---

# 2. Reconciliation Scope

La réconciliation couvre :

## KPI principaux

1. Product Revenue
2. Product Quantity
3. Product Frequency

## Business Analysis Validation

4. Fast Moving / Slow Moving Product
5. Pareto Analysis

---

# 3. Source Files Comparison

## A. Manual Python Product Report

Fichier principal :

```text
D:\Project_01_Data_Analyst\OUTPUT\REPORT\
ODC_Bag8_FinalReport_03_PRODUCT.xlsx
```

Sheets utilisés :

| Sheet             | Fonction                                  |
| ----------------- | ----------------------------------------- |
| Product_Revenue   | Analyse du chiffre d’affaires produit     |
| Product_Quantity  | Analyse de la quantité de produits vendus |
| Product_Frequency | Analyse de la fréquence des transactions  |
| Fast_Slow_Product | Classification des produits               |
| Pareto_Analysis   | Analyse de la contribution au revenue     |

---

## B. Product Master Dataset

Fichier principal :

```text
D:\Project_01_Data_Analyst\OUTPUT\MASTER\PRODUCT_MASTER\
ODC_Bag8_FinalReport_00_PRODUCT_MASTER.xlsx
```

Sheets utilisés :

| Sheet            | Fonction                |
| ---------------- | ----------------------- |
| Product_Master   | Dataset master product  |
| Duplicate_Check  | Validation des doublons |
| Price_Validation | Validation des prix     |

---

# 4. Methodology

Méthode de réconciliation :

1. Lire le Product Master Dataset.
2. Lire chaque output Manual Python.
3. Effectuer le matching sur la base de :

```text
id_produk
nama_produk
```

4. Comparer les KPI :

* valeur du chiffre d’affaires
* quantité vendue
* nombre de transactions

5. Produire le statut :

```text
MATCH = PASS
```

Lorsque toutes les valeurs sont identiques.

---

# 5. Product Revenue Reconciliation

## Comparison

Master :

Colonne :

```text
total_omzet
```

Manual Python :

Sheet :

```text
Product_Revenue
```

Colonne :

```text
omzet
```

---

## Calculation

Formule :

```text
Revenue Match =
Master total_omzet == Manual Python omzet
```

---

## Result

| Product             | Master Revenue | Manual Revenue | Status |
| ------------------- | -------------: | -------------: | ------ |
| Laptop Lenovo ID 1  | 46,937,000,000 | 46,937,000,000 | PASS   |
| Laptop Lenovo ID 5  | 44,625,000,000 | 44,625,000,000 | PASS   |
| Printer Epson       | 13,037,500,000 | 13,037,500,000 | PASS   |
| Keyboard Mechanical |  4,391,250,000 |  4,391,250,000 | PASS   |
| Mouse Logitech      |  1,389,500,000 |  1,389,500,000 | PASS   |

Result:

```text
Overall Revenue Match = TRUE
```

---

# 6. Product Quantity Reconciliation

## Comparison

Master :

```text
jumlah_terjual
```

Manual Python :

Sheet :

```text
Product_Quantity
```

Column :

```text
jumlah_terjual
```

---

## Calculation

Formule :

```text
Quantity Match =
Master jumlah_terjual == Manual jumlah_terjual
```

---

## Result

| Product             | Master Qty | Manual Qty | Status |
| ------------------- | ---------: | ---------: | ------ |
| Laptop Lenovo ID 1  |       5522 |       5522 | PASS   |
| Laptop Lenovo ID 5  |       5250 |       5250 | PASS   |
| Printer Epson       |       5215 |       5215 | PASS   |
| Keyboard Mechanical |       5855 |       5855 | PASS   |
| Mouse Logitech      |       5558 |       5558 | PASS   |

Result:

```text
Overall Quantity Match = TRUE
```

---

# 7. Product Frequency Reconciliation

## Comparison

Master :

```text
total_transaksi
```

Manual Python :

Sheet :

```text
Product_Frequency
```

Column :

```text
frekuensi_transaksi
```

---

## Calculation

Formule :

```text
Frequency Match =
Master total_transaksi == Manual frekuensi_transaksi
```

---

## Result

| Product             | Master Frequency | Manual Frequency | Status |
| ------------------- | ---------------: | ---------------: | ------ |
| Laptop Lenovo ID 1  |             1024 |             1024 | PASS   |
| Laptop Lenovo ID 5  |              943 |              943 | PASS   |
| Printer Epson       |              982 |              982 | PASS   |
| Keyboard Mechanical |             1048 |             1048 | PASS   |
| Mouse Logitech      |             1003 |             1003 | PASS   |

Result:

```text
Overall Frequency Match = TRUE
```

---

# 8. Fast Moving / Slow Moving Validation

## Source

Manual Python :

Sheet :

```text
Fast_Slow_Product
```

---

## Logic Validation

Source Script :

```text
ODC_Bag8_FinalReport_03_PRODUCT_Professional.py
```

Logic :

```python
if total_penjualan >= rata_penjualan:
    Fast Moving Product
else:
    Slow Moving Product
```

---

## Calculation

Average Sales :

```text
(5855 + 5558 + 5522 + 5250 + 5215) / 5

= 5480
```

---

## Validation Result

| Product             | Sales | Average | Category    | Status |
| ------------------- | ----: | ------: | ----------- | ------ |
| Keyboard Mechanical |  5855 |    5480 | Fast Moving | PASS   |
| Mouse Logitech      |  5558 |    5480 | Fast Moving | PASS   |
| Laptop Lenovo ID 1  |  5522 |    5480 | Fast Moving | PASS   |
| Laptop Lenovo ID 5  |  5250 |    5480 | Slow Moving | PASS   |
| Printer Epson       |  5215 |    5480 | Slow Moving | PASS   |

---

# 9. Pareto Analysis Validation

## Source

Manual Python :

Sheet :

```text
Pareto_Analysis
```

---

## Calculation

Formule :

```text
Persentase Produk =
Omzet Produk / Total Omzet x 100
```

Formule :

```text
Persentase Kumulatif =
Cumulative Sum(Persentase)
```

---

## Result

| Ranking | Product             | Contribution |
| ------- | ------------------- | -----------: |
| 1       | Laptop Lenovo ID 1  |       42.52% |
| 2       | Laptop Lenovo ID 5  |       82.95% |
| 3       | Printer Epson       |       94.76% |
| 4       | Keyboard Mechanical |       98.74% |
| 5       | Mouse Logitech      |         100% |

Status:

```text
Pareto Validation = PASS
```
# 10. Final Reconciliation Summary

| Validation Area         | Result |
| ----------------------- | ------ |
| Product Revenue         | PASS   |
| Product Quantity        | PASS   |
| Product Frequency       | PASS   |
| Fast/Slow Product Logic | PASS   |
| Pareto Analysis         | PASS   |

---

# 11. Final Audit Conclusion

Based on the reconciliation results, all Product Manual Python outputs were successfully validated against the Product Master Dataset.

No findings were identified regarding:

* revenue differences,
* differences in the quantity of products sold,
* differences in the number of transactions,
* differences in product classification,
* differences in Pareto analysis.

The Product Master Dataset has been proven to serve as a consistent audit layer for all Product analyses.

---

# 12. Final Status

```text
PRODUCT RECONCILIATION

Manual Python VS Master

STATUS:

PASS

Accuracy:

100%
```

---

# Recommendation

The Product Master Dataset can be used as the canonical source for future validation and audit of the Product analysis process.

All Product Manual Python reports are declared validated and consistent with the Master Dataset.

# PRODUCT RECONCILIATION

## Manual Python VS Master

Date:
01 August 2026

Project:
Project_01_Data_Analyst

Status:
PASS - COMPLETED

============================================================

# 1. RECONCILIATION OBJECTIVE

The objectives of the Product reconciliation are:

* To ensure that the Product analysis results from Manual Python are consistent with the Master Output.
* To ensure that there are no differences in Product KPI values.
* To ensure that the Master functions as a valid Audit Layer.
* To ensure that the Product Report calculations originate from a consistent data source.

Note:

Master is not a processing pipeline.

Master only stores the extracted and validated data
as an audit reference.

============================================================

# 2. FILES COMPARED

## A. Manual Python Product Report

Source:

D:\Project_01_Data_Analyst\OUTPUT\REPORT\ODC_Bag8_FinalReport_03_PRODUCT.xlsx

Sheets used:

1. Product_Quantity
2. Product_Revenue
3. Product_Frequency
4. Fast_Slow_Product
5. Pareto_Analysis

============================================================

## B. Master Product Output

Source:

D:\Project_01_Data_Analyst\OUTPUT\MASTER\PRODUCT_MASTER\ODC_Bag8_FinalReport_00_PRODUCT_MASTER.xlsx

Sheet used:

Product_Master

============================================================

# 3. RECONCILIATION METHOD

The comparison was performed based on:

* id_produk
* nama_produk

KPIs compared:

1. Quantity of Products Sold
2. Total Product Revenue
3. Transaction Frequency
4. Fast / Slow Moving Classification
5. Pareto Analysis

Method:

Manual Python Output

compared with

Master Output

Status:

Exact Matching Validation

============================================================

# 4. PRODUCT REVENUE RECONCILIATION

## Manual Python File:

Sheet:

Product_Revenue

Columns:

* id_produk
* nama_produk
* omzet
* ranking

## Master File:

Sheet:

Product_Master

Columns:

* id_produk
* nama_produk
* total_omzet

Results:

| ID Produk | Nama Produk         |   Master Omzet |   Manual Omzet | Status |
| --------- | ------------------- | -------------: | -------------: | ------ |
| 1         | Laptop Lenovo       | 46,937,000,000 | 46,937,000,000 | PASS   |
| 5         | Laptop Lenovo       | 44,625,000,000 | 44,625,000,000 | PASS   |
| 2         | Printer Epson       | 13,037,500,000 | 13,037,500,000 | PASS   |
| 4         | Keyboard Mechanical |  4,391,250,000 |  4,391,250,000 | PASS   |
| 3         | Mouse Logitech      |  1,389,500,000 |  1,389,500,000 | PASS   |

Validation Result:

Omzet Match = TRUE

Status:

PASS

============================================================

# 5. PRODUCT QUANTITY RECONCILIATION

## Manual Python File:

Sheet:

Product_Quantity

Columns:

* id_produk
* nama_produk
* jumlah_terjual

## Master File:

Columns:

* id_produk
* nama_produk
* jumlah_terjual

Results:

| ID Produk | Nama Produk         | Master Qty | Manual Qty | Status |
| --------- | ------------------- | ---------: | ---------: | ------ |
| 1         | Laptop Lenovo       |       5522 |       5522 | PASS   |
| 5         | Laptop Lenovo       |       5250 |       5250 | PASS   |
| 2         | Printer Epson       |       5215 |       5215 | PASS   |
| 4         | Keyboard Mechanical |       5855 |       5855 | PASS   |
| 3         | Mouse Logitech      |       5558 |       5558 | PASS   |

Validation Result:

Quantity Match = TRUE

Status:

PASS

============================================================

# 6. PRODUCT FREQUENCY RECONCILIATION

## Manual Python File:

Sheet:

Product_Frequency

Columns:

* id_produk
* nama_produk
* frekuensi_transaksi

## Master File:

Columns:

* total_transaksi

Formula:

Frequency Manual

=

Frequency Master

Results:

| ID Produk | Nama Produk         | Master Frequency | Manual Frequency | Status |
| --------- | ------------------- | ---------------: | ---------------: | ------ |
| 1         | Laptop Lenovo       |             1024 |             1024 | PASS   |
| 5         | Laptop Lenovo       |              943 |              943 | PASS   |
| 2         | Printer Epson       |              982 |              982 | PASS   |
| 4         | Keyboard Mechanical |             1048 |             1048 | PASS   |
| 3         | Mouse Logitech      |             1003 |             1003 | PASS   |

Validation Result:

Frequency Match = TRUE

Status:

PASS

============================================================

# 7. FAST / SLOW MOVING PRODUCT VALIDATION

## Manual Python File:

Sheet:

Fast_Slow_Product

Columns:

* total_penjualan
* jumlah_transaksi
* kategori

Formula:

If:

total_penjualan >= average sales

then:

Fast Moving Product

If:

total_penjualan < average sales

then:

Slow Moving Product

Results:

| Produk              | Kategori Manual     | Status |
| ------------------- | ------------------- | ------ |
| Keyboard Mechanical | Fast Moving Product | PASS   |
| Mouse Logitech      | Fast Moving Product | PASS   |
| Laptop Lenovo ID 1  | Fast Moving Product | PASS   |
| Laptop Lenovo ID 5  | Slow Moving Product | PASS   |
| Printer Epson       | Slow Moving Product | PASS   |

Status:

PASS

============================================================

# 8. PARETO ANALYSIS VALIDATION

Sheet:

Pareto_Analysis

Calculation:

Product Percentage:

Product Revenue / Total Revenue x 100%

Cumulative Percentage:

Sum of revenue percentages based on ranking

Results:

| Produk              | Revenue Contribution | Cumulative |
| ------------------- | -------------------: | ---------: |
| Laptop Lenovo ID 1  |               42.52% |     42.52% |
| Laptop Lenovo ID 5  |               40.43% |     82.95% |
| Printer Epson       |               11.81% |     94.76% |
| Keyboard Mechanical |                3.98% |     98.74% |
| Mouse Logitech      |                1.26% |       100% |

Validation:

Pareto calculation is consistent.

Status:

PASS

============================================================

# 9. RECONCILIATION RESULTS SUMMARY

| Component                | Status |
| ------------------------ | ------ |
| Product Revenue          | PASS   |
| Product Quantity         | PASS   |
| Product Frequency        | PASS   |
| Fast Slow Moving Product | PASS   |
| Pareto Analysis          | PASS   |

Total Validation:

5 / 5 PASS

Success Rate:

100%

============================================================

# 10. FINAL CONCLUSION

Based on the reconciliation results:

Manual Python Product Analysis

and

Master Product Output

have identical results.

No findings were identified regarding:

* Revenue differences
* Differences in the quantity of products sold
* Differences in transaction frequency
* Differences in product categories
* Differences in Pareto Analysis results

Conclusion:

PRODUCT RECONCILIATION

MANUAL PYTHON VS MASTER

= PASS

The Master Product has been successfully validated as an Audit Layer.

