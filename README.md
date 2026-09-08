# BUSINESS SALES PERFORMANCE ANALYSIS PROJECT

### From Raw Data to Trusted Business Insight

**Data Analyst | Python • SQL • MySQL • n8n • Docker**

---

## 🔴 PROBLEM

Business performance data can appear complete and consistent while still containing hidden **data-quality and data-lineage risks**.

This project addressed several critical business questions:

* Can reported revenue be trusted and independently validated?
* Is the transaction population complete and consistent across analytical outputs?
* Which products, customers, and transactions drive business performance?
* Which customers require retention attention?
* Can differences between analytical sources be traced, explained, and supported by evidence?

The core challenge was not simply to produce reports or dashboards.

It was to establish a reliable analytical foundation before business conclusions were made.

### Core Question

> **Can the business numbers be trusted, traced, and explained?**

---

## 💡 SOLUTION

I designed and executed an end-to-end data analytics and control workflow that transformed raw transactional data into **validated, reconciled, 
and business-ready insight**.

### Analytical Workflow

**Raw Data → Database → Cleaning → Data Quality Validation → Analysis → Reconciliation → Root-Cause Investigation → Audit → Visualization → 
Reporting**

### Analytical Approach

**Data Quality & Cleaning**
Validated missing values, duplicates, consistency, and transaction-level integrity.

**Transaction Validation**
Validated transaction records and financial calculations, including quantity, price, and transaction value relationships.

**Business Analysis**
Analyzed:

* Sales Performance
* Product Performance
* Customer Behavior
* Transaction Performance
* Financial Performance
* Regional Performance

**Customer Segmentation**
Evaluated customer activity and identified customers requiring retention attention.

**Cross-Source Reconciliation**
Compared analytical outputs across controlled sources to determine whether differences were valid, explainable, or required further investigation.

**Root-Cause Investigation**
Traced material discrepancies from reported numbers to their underlying data population, processing path, and output lineage.

**Audit & Evidence Control**
Supported final conclusions with validated datasets, reconciliation results, workflow evidence, and documented audit findings.

### Technology

**Python • Pandas • SQL • MySQL • Matplotlib • n8n • Docker**

---

## 🏆 RESULT

The project established a validated and reconciled business view based on **5,000 transactions**.

### Validated Business Results

| Metric                |      Validated Result |
| --------------------- | --------------------: |
| **Transactions**      |             **5,000** |
| **Units Sold**        |            **27,400** |
| **Validated Revenue** | **Rp110,380,250,000** |
| **Customers**         |             **1,848** |
| **At-Risk Customers** |      **734 (39.72%)** |

### Customer Retention Finding

**734 customers (39.72%)** were classified as **At-Risk Customers**, making this the largest customer segment within the validated population 
of 1,848 customers.

This established **customer retention as a measurable business priority** for targeted follow-up and reactivation.

### Critical Reconciliation Finding

A material revenue discrepancy was identified during cross-source reconciliation:

**Rp110,380,250,000**
vs.
**Rp104,902,500,000**

**Difference: Rp5,477,750,000**

The investigation established that the two outputs were based on different record populations:

* **Validated analytical population:** 5,000 transactions
* **Legacy output population:** 4,745 transactions
* **Population difference:** 255 transactions
* **Revenue difference:** Rp5,477,750,000

The 255-record difference exactly corresponded to the reported revenue difference.

### Root-Cause Boundary

Further investigation examined the source code, workflow, physical output files, and data lineage.

The investigation established a high-confidence **data-lineage and output-management inconsistency**: multiple output paths and filenames existed 
for the same logical cleaned dataset without one consistently enforced canonical source.

However, the exact historical mechanism that produced the 4,745-record artifact could not be conclusively established from the available evidence.

Therefore, the project **does not claim an unsupported historical deletion mechanism**.

> **The discrepancy was not simply reported. It was traced to the underlying data population, investigated through the processing chain, and
 bounded by the evidence.**

### Business Outcome

The project established:

* Validated transaction and revenue figures
* Evidence-supported customer segmentation
* Reconciled analytical outputs
* Traceable discrepancy investigation
* Documented root-cause analysis
* Controlled end-to-end analytical workflow
* Audit-ready supporting evidence

> **The result was not simply a set of numbers. It was a validated, reconciled, traceable, and business-ready analytical foundation.**

---

## 📊 PORTFOLIO EVIDENCE

The complete project documentation, analytical outputs, reconciliation evidence, audit records, workflow documentation, and final business 
presentation are available in the project repository.

### Reconciliation Coverage

The project used reconciliation as a control mechanism across:

**Sales • Product • Customer • Transaction • Financial**

Results were cross-checked through controlled analytical paths, including:

**Manual Python ↔ Master**

**Manual Python ↔ n8n**

**Master ↔ n8n**

The purpose was not to force different systems to produce identical numbers, but to determine:

* whether results should agree;
* whether they actually agree;
* why differences exist;
* and which result is supported by the validated data population.

> **Reconciliation does not make numbers agree. It proves whether they should agree—and explains why when they do not.**

### Final Audit

The final audit covered the major technical and analytical components:

**DATABASE · SALES · PRODUCT · CUSTOMER · REGION · TRANSACTION · FINANCE · GENERATOR · DASHBOARD**

Final workflow status:

| Workflow                          | Status     |
| --------------------------------- | ---------- |
| **WF1 — Extraction**              | ✅ COMPLETE |
| **WF2 — Cleaning**                | ✅ COMPLETE |
| **WF3 — Data Quality Validation** | ✅ PASS     |
| **WF4 — Data Analysis**           | ✅ PASS     |
| **WF5 — Visualization**           | ✅ PASS     |
| **WF_MASTER — Final Control**     | ✅ COMPLETE |
| **Final Audit**                   | ✅ COMPLETE |

### Automation

The completed workflow connects:

**WF1 → WF2 → WF3 → WF4 → WF5**

through **WF_MASTER**, creating a controlled path from source data through validation, analysis, visualization, and reporting.

The value of the automation is not simply speed.

It provides:

**Repeatability • Consistency • Control • Reduced Manual Intervention • Traceability**

> **The strength is not the number of tools used. It is the ability to make them work together to solve a real analytical problem.**

---

## FINAL PROJECT OUTCOME

The project demonstrates the integration of:

**Business Understanding + Analytical Reasoning + Technical Execution**

The analytical process can be summarized as:

**Processed → Validated → Reconciled → Investigated → Explained → Audited**

The final outcome is an analytical workflow that is:

**Accurate.
Traceable.
Reproducible.
Auditable.
Business-oriented.**

> **Reliable analytics is not about producing more numbers. It is about producing numbers that can be trusted, explained, and used to make better
 decisions.**
