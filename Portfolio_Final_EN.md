 DATA ANALYTICS PORTFOLIO

## Project 01 — ODC Bag 8
#
### From Raw Data to Trusted Business Insight

**Data Analyst | Python • SQL • MySQL • n8n • Docker**

# 01 — EXECUTIVE SUMMARY

This project demonstrates an end-to-end data analytics solution built to transform raw transactional data into **validated, reconciled, and business-ready insights**.

The project covers the complete analytical chain:

**Data Extraction → Data Cleaning → Data Quality Validation → Analysis → Reconciliation → Audit → Visualization → Automated Reporting**

The key objective was not simply to produce reports.

It was to ensure that the numbers behind the reports were **correct, explainable, traceable, and defensible**.

The project ultimately established a controlled analytical workflow in which business results could be traced back to their underlying data and technical processing.

### The Business Value

The project demonstrates three capabilities working together:

**BUSINESS**
Understanding what the numbers mean and why they matter.

**ANALYTICAL**
Testing, reconciling, investigating, and explaining differences rather than accepting outputs at face value.

**TECHNICAL**
Building an automated data workflow using SQL, Python, MySQL, Docker, and n8n.

> **The strongest result was not a dashboard. It was confidence in the numbers behind the dashboard.**

# 02 — BUSINESS CHALLENGE

A business report is only as reliable as the data supporting it.

The project therefore addressed several practical analytical questions:

* Can the raw transactional data be transformed into a reliable analytical dataset?
* Are the resulting metrics consistent across analytical methods?
* Can differences between systems be identified and explained?
* Can the final results be traced back to their source?
* Can the analytical workflow be executed in a controlled and repeatable way?
* Can the final output support business interpretation rather than merely display numbers?

The project was designed around one principle:

> **Do not trust a number simply because a system produced it. Validate it.**

# 03 — DATA & PROJECT SCOPE

The project used a company transactional dataset containing:

* **5,000 initial records**
* **14 columns**
* Transaction, customer, product, and financial information
* MySQL as the database environment
* CSV as the analytical data exchange format

The analytical scope covered:

**Sales**
Revenue and transaction-level analysis.

**Product**
Product performance and reconciliation.

**Customer**
Customer population and segmentation.

**Transaction**
Transaction-level integrity and consistency.

**Finance**
Financial totals and revenue validation.

**Visualization**
Business-oriented analytical outputs.

**Automation**
End-to-end workflow orchestration.

# 04 — TECHNICAL ARCHITECTURE

The solution was designed as a controlled pipeline rather than a collection of disconnected scripts.

### Core Technology Stack

| Area                    | Technology                   |
| ----------------------- | ---------------------------- |
| Database                | MySQL                        |
| Query / Data Access     | SQL                          |
| Data Analysis           | Python                       |
| Data Processing         | Pandas                       |
| Visualization           | Matplotlib                   |
| Workflow Automation     | n8n                          |
| Application Environment | Docker                       |
| Data Exchange           | CSV                          |
| Reporting               | Automated analytical outputs |

### End-to-End Flow

**MySQL**

↓

**WF1 — Data Extraction**

↓

**WF2 — Data Cleaning**

↓

**WF3 — Data Quality Validation**

↓

**WF4 — Data Analysis**

↓

**WF5 — Visualization & Reporting**

↓

**WF_MASTER — End-to-End Orchestration**

The architecture separates extraction, transformation, validation, analysis, and presentation so that each stage can be checked independently.

> **Automation was designed around control, not convenience.**

---

# 05 — DATA EXTRACTION & CLEANING

The initial dataset contained **5,000 records**.

The cleaning process identified:

* **255 missing address values**
* **0 duplicate records**

An earlier cleaning output contained **4,745 records**, reflecting the removal of records associated with missing address values.

This became an important lesson in the project:

> **Cleaning is not only about improving data quality. It can also change the population being analysed.**

Therefore, downstream analytical results must always be interpreted in relation to the dataset version being used.

The project subsequently established a canonical analytical dataset so that later analysis and validation were performed against the correct data population.

# 06 — DATA QUALITY & VALIDATION

Data quality validation was treated as a formal workflow stage.

The validation process checked whether the processed dataset met the expected analytical requirements before analysis continued.

### Validation Principle

**Input → Validate → Analyse**

rather than:

**Input → Analyse → Hope the result is correct**

WF3 achieved:

**STATUS: PASS**

The workflow was subsequently frozen as part of the controlled final project state.

This created an important control point between data preparation and analytical interpretation.

# 07 — ANALYTICAL FRAMEWORK

The analytical work was structured around five core business areas:

### Sales

Understand revenue performance and sales behaviour.

### Product

Identify product-level contribution and validate product metrics.

### Customer

Understand customer population and customer status.

### Transaction

Validate transaction volume, units, and revenue.

### Finance

Reconcile financial results across independent analytical sources.

Each analytical area was not treated as an isolated report.

The outputs were cross-checked against corresponding master and workflow results.

> **Analysis becomes stronger when the same business question can be answered consistently from more than one controlled source.**

# 08 — CUSTOMER ANALYSIS

The final Customer Master contained **1,848 customers**, and the customer segmentation was validated against the Customer Master through a formal reconciliation process.

### Customer Segmentation

| Segment               | Customers |       Share |       Total Purchases | Transactions |
| --------------------- | --------: | ----------: | --------------------: | -----------: |
| **Active Customer**   |   **691** |  **37.39%** |      Rp49,641,250,000 |        2,278 |
| **At-Risk Customer**  |   **734** |  **39.72%** |      Rp42,526,500,000 |        1,957 |
| **Inactive Customer** |   **423** |  **22.89%** |      Rp18,212,500,000 |          765 |
| **Total**             | **1,848** | **100.00%** | **Rp110,380,250,000** |    **5,000** |

### Analytical Finding

**At-Risk Customers represent the largest customer segment at 39.72% of the total customer population.**

The finding is significant because the at-risk population is larger than the active customer population:

**734 At-Risk Customers vs. 691 Active Customers**

This indicates a clear **customer-retention priority**.

However, the analysis does not treat segmentation as a conclusion by itself. The segmentation was recalculated from the Customer Churn output and reconciled against the Customer Master.

The reconciliation confirmed:

* **1,848 / 1,848 customers matched**
* Customer transaction values matched
* Customer purchase values matched
* Last transaction dates matched
* Customer category totals matched
* **Overall Customer Reconciliation: PASS**

### Business Interpretation

The immediate business question is therefore not simply:

> **“How many customers are at risk?”**

It is:

> **“Which customers are at risk, what is driving their inactivity, and which retention actions can recover the highest-value customers?”**

Potential business actions include:

* Prioritize high-value at-risk customers for targeted follow-up.
* Design retention offers based on customer purchase behaviour.
* Identify customers approaching inactivity thresholds.
* Develop reactivation strategies for inactive customers.
* Monitor the at-risk population as an ongoing retention KPI.

### Evidence & Traceability

**Primary analytical source**

`ODC_Bag8_FinalReport_04_CUSTOMER.xlsx`

Relevant sheets:

* `Customer_Churn`
* `Customer_Category`

**Customer Master source**

`ODC_Bag8_FinalReport_00_CUSTOMER_MASTER.xlsx`

Relevant sheets:

* `Customer_Master`
* `Data_Quality_Check`

**Primary reconciliation evidence**

`03_Customer_Reconciliation_ManualPython_vs_Master_EN.md`

### Final Analytical Statement

> **Customer analysis transformed 1,848 customer records into a validated segmentation framework, identifying 734 At-Risk Customers (39.72%) as the largest segment and establishing customer retention as a measurable business priority.**

# 09 — TRANSACTION & REVENUE ANALYSIS

The final validated transaction population established the following core metrics:

| KPI                    |      Validated Result |
| ---------------------- | --------------------: |
| **Total Transactions** |             **5,000** |
| **Total Units**        |            **27,400** |
| **Total Revenue**      | **Rp110,380,250,000** |

These metrics represent the quantitative foundation of the project and provide the baseline for subsequent financial, sales, customer, and business analysis.

### Analytical Control

The revenue figure was **not accepted simply because it appeared in an automated output**.

It was independently compared across controlled analytical sources and subjected to reconciliation.

The final investigation established that the validated revenue of:

**Rp110,380,250,000**

was supported by the complete **5,000-transaction population**.

This distinction became critical when a legacy n8n output reported a lower revenue figure. The discrepancy was subsequently investigated and traced to a difference in the underlying data population.

### Business Significance

The validated transaction population provides a reliable quantitative foundation for answering higher-level business questions, including:

* How much revenue was generated?
* How much transaction activity produced that revenue?
* How many units were sold?
* Are financial outputs consistent across analytical sources?
* Can reported revenue be traced back to the underlying transaction population?

The key analytical principle is:

> **A revenue KPI is only as reliable as the transaction population supporting it.**
### Evidence & Traceability

The validated transaction and revenue results are supported by a controlled chain of reconciliation and audit evidence.

**Primary Transaction Validation**

* `ODC_Bag8_FinalReport_00_TRANSACTION_MASTER.xlsx`
  Final Transaction Master and primary validated transaction dataset.

* `04_Transaction_Reconciliation_ManualPython_vs_Master_EN.md`
  Reconciles Manual Python transaction analysis against the Transaction Master, including validation of **5,000 transactions, 27,400 units, and Rp110,380,250,000 revenue**.

**Cross-System Transaction Reconciliation**

* `04_Transaction_Reconciliation_ManualPython_vs_n8n_EN.md`
  Validates transaction-analysis consistency between Manual Python and n8n.

* `04_Transaction_Reconciliation_Master_vs_n8n_EN.md`
  Provides the Master-versus-n8n transaction reconciliation and supports investigation of analytical differences.

**Financial Reconciliation & Revenue Control**

* `05_Financial_Reconciliation_ManualPython_vs_Master_EN.md`
  Validates financial results between Manual Python and the authoritative Master data.

* `05_Financial_Reconciliation_ManualPython_vs_n8n_EN.md`
  Provides the financial cross-system reconciliation between Manual Python and n8n.

* `05_Financial_Reconciliation_Master_vs_n8n_EN.md`
  Supports the final Master-versus-n8n financial comparison.

**Final Audit Evidence**

* `Final_Audit_Manual_Python_Financial_Analysis_EN.md`
  Provides the final independent audit evidence covering the validated financial and analytical results.

### Traceability Principle

The final figures were therefore not treated as system-generated outputs that could be accepted without verification.

They were established through:

**Transaction Master → Manual Python Analysis → Cross-System Comparison → Reconciliation → Independent Audit**

This creates a traceable evidence chain from the underlying transaction population to the final reported business metrics.

### Key Takeaway

> **The project established 5,000 validated transactions, 27,400 units, and Rp110,380,250,000 in revenue—then subjected those results to reconciliation rather than treating system-generated numbers as automatically correct.**

This transformed the transaction metrics from simple reported figures into **validated analytical evidence**.

# 10 — THE CRITICAL RECONCILIATION

One of the most important analytical findings occurred when two revenue results did not agree.

### Revenue Comparison

| Source                                          |               Revenue |
| ----------------------------------------------- | --------------------: |
| **Manual Python / Validated Analytical Source** | **Rp110,380,250,000** |
| **Legacy n8n Output**                           | **Rp104,902,500,000** |
| **Difference**                                  |   **Rp5,477,750,000** |

### The Investigation

A weaker analysis could have simply reported the discrepancy.

This project investigated it.

The investigation established that the two results were based on different data populations:

* **Validated transaction population:** 5,000 records
* **Legacy n8n population:** 4,745 records
* **Population difference:** 255 records

A transaction-level reconciliation identified that the 255-record difference corresponded to:

**Rp5,477,750,000**

—the exact difference between the two reported revenue figures.

### Critical Audit Qualification

The investigation did **not** stop at identifying the 255-record difference.

Source-code inspection, workflow examination, physical file verification, and data-lineage analysis were subsequently performed to determine **how the historical 4,745-row artifact had been produced**.

The investigation confirmed that:

* the current Python cleaning API can generate the complete **5,000-row dataset**;
* the current cleaned outputs contain **5,000 rows** and **Rp110,380,250,000** revenue;
* multiple physical paths and filenames are used for the same logical cleaned dataset;
* downstream components reference different output paths and filenames.

However, the exact historical mechanism that reduced the dataset from **5,000 to 4,745 records** was **not conclusively established** from the available source-code evidence.

Therefore, the 255-record difference is treated as a:

> **Historical unexplained discrepancy**

rather than as a proven deletion mechanism.

### Confirmed Root Cause

The investigation ultimately established a high-confidence **data-lineage and output-management issue**:

> **The same logical cleaned dataset was managed through multiple output paths and filenames without one consistently enforced canonical source.**

This created a structural risk of downstream processes consuming different or legacy artifacts.

Importantly, the investigation found **no evidence that the currently examined duplicate physical outputs contained different data**; the verified files had identical contents.

### Why This Finding Matters

The critical analytical achievement was therefore not merely discovering a revenue mismatch.

It was demonstrating the distinction between:

**Observed discrepancy → Evidence → Investigation → Root-cause boundary → Controlled conclusion**

The project did not force an unsupported explanation onto the evidence.

Instead, it established exactly what was proven, what remained historically unexplained, and what architectural issue could be confirmed with high confidence.

> **The discrepancy was not the end of the analysis. It was the beginning of an evidence-based investigation.**

Evidence & Traceability

Primary Root-Cause Investigation

. Finding_RootCase_Financial_Revenue_Inconsistency_EN.md

Financial Source & Grain Alignment

. Financial_Data_Source_Alignment_EN.md

Final Revenue Difference Audit

. SELISIH_Angka_Revenue_FINALAUDIT_EN.md

Final Audit

. Final_Audit_Manual_Python_Financial_Analysis_EN.md

### Final Analytical Conclusion

The project did not simply identify:

**Rp5,477,750,000 revenue difference.**

It traced the discrepancy back to a measurable difference in data population, investigated the historical artifact, examined the processing chain, and established the boundaries of what could and could not be proven.

The result is a stronger analytical conclusion:

> **5,000 validated transactions support Rp110,380,250,000 in revenue, while the legacy 4,745-record artifact produced Rp104,902,500,000. The 255-record historical discrepancy exactly corresponds to the revenue difference, while the confirmed high-confidence root cause lies in inconsistent output-file and data-lineage management—not in a proven transaction-deletion mechanism.**

# 11 — ROOT-CAUSE ANALYSIS

The revenue discrepancy was not accepted as a simple reporting or arithmetic error.

The investigation followed the data lineage from the validated transaction population through the legacy analytical output.

### Investigation Chain

**Different Revenue Result**

↓

**Compare Underlying Data Population**

↓

**5,000 Validated Transactions vs 4,745 Historical Records**

↓

**Identify 255-Record Historical Discrepancy**

↓

**Reconcile the Revenue Difference**

↓

**Inspect Source Code, Workflow, and Physical Output**

↓

**Eliminate Unsupported Deletion Hypotheses**

↓

**Establish the Confirmed Data-Lineage / Output-Management Issue**

### What the Investigation Proved

The investigation established that:

* The validated transaction population contains **5,000 transactions**.
* The historical artifact contained **4,745 records**.
* The revenue difference between the two states was **Rp5,477,750,000**.
* The historical 255-record discrepancy corresponds exactly to the revenue difference.
* The current Cleaning API was subsequently verified to receive and produce **5,000 transactions**.
* No evidence was found that the current Financial Layer directly deleted transactions.
* The exact historical mechanism that produced the 4,745-row artifact could **not be conclusively established** from the available source-code
 evidence.

The evidence confirmed the discrepancy, but it did not prove exactly how the historical 255 records were removed. The investigation therefore
 stopped where the evidence stopped.
 
### Root-Cause Classification

The confirmed architectural issue was:

> **Data Lineage / Output Management Inconsistency**

Multiple output paths and filenames were identified for the same logical cleaned dataset, increasing the risk of downstream processes referencing a legacy or non-canonical artifact.

This finding is further supported by the independent **Financial Data Source and Grain Alignment** investigation, which identified differences between transaction-level financial calculation and downstream aggregated analytical sources.

### Final Validated Revenue

The controlled reconciliation established the validated revenue at:

## **Rp110,380,250,000**

The key analytical capability demonstrated is therefore not simply identifying a numerical difference, but **tracing the difference through its underlying data population, processing path, source code, and evidence until the boundaries of what can—and cannot—be proven are clearly established.**

> **When numbers disagree, investigate the data lineage and population before blaming the arithmetic.**

### Evidence & Traceability

**Primary Root-Cause Investigation**

`Finding_RootCase_Financial_Revenue_Inconsistency_EN.md`

**Financial Data Source & Grain Alignment**

`Financial_Data_Source_Alignment_EN.md`

**Final Revenue Difference Audit**

SELISIH_Angka_Revenue_FINALAUDIT_EN.md

**Final Audit Evidence**

`Final_Audit_Manual_Python_Financial_Analysis_EN.md`

# 12 — RECONCILIATION AS A CONTROL

Reconciliation was used as a **control mechanism across the project**, not simply as a final comparison of numbers.

The analysis covered five key areas:

* Sales
* Product
* Customer
* Transaction
* Financial

Results were cross-checked through three control paths:

**Manual Python ↔ Master**

**Manual Python ↔ n8n**

**Master ↔ n8n**

### What Reconciliation Was Designed to Answer

The purpose was not to force different systems to produce the same numbers.

It was to determine:

1. **Should the results agree?**
2. **Do they actually agree?**
3. **If they differ, what caused the difference?**
4. **Which result is supported by the correct and validated data population?**

This approach allowed the project to separate:

**True data inconsistencies**

from

**Valid differences caused by different analytical logic, data grain, or source populations.**

### Why This Matters

The reconciliation process helped validate the major project outputs while also exposing differences that required further investigation.

For example, the financial reconciliation identified a **Rp5,477,750,000 revenue difference**. Instead of treating the difference as an error immediately, the investigation traced the underlying data population and processing path.

This turned reconciliation into an analytical control rather than a simple number-matching exercise.

> **Reconciliation does not make numbers agree. It proves whether they should agree—and explains why when they do not.**

### Evidence & Traceability

**Financial Reconciliation**

* `05_Financial_Reconciliation_ManualPython_vs_Master_EN.md`
* `05_Financial_Reconciliation_ManualPython_vs_n8n_EN.md`
* `05_Financial_Reconciliation_Master_vs_n8n_EN.md`


### Key Takeaway

> **Reconciliation turned the project from a collection of calculated outputs into a controlled, traceable analytical process.**

# 13 — AUDIT & EVIDENCE

The project was subjected to a **formal final audit** covering the major technical and analytical components:

**DATABASE · SALES · PRODUCT · CUSTOMER · REGION · TRANSACTION · FINANCE · GENERATOR · DASHBOARD**

The audit was designed to verify not only whether the workflows ran successfully, but whether the resulting outputs were **consistent, traceable, and supported by evidence**.

### Final Workflow Audit

| Workflow                          | Final Status  |
| --------------------------------- | ------------- |
| **WF1 — Extraction**              | COMPLETE      |
| **WF2 — Cleaning**                | COMPLETE      |
| **WF3 — Data Quality Validation** | PASS          |
| **WF4 — Data Analysis**           | PASS          |
| **WF5 — Visualization**           | PASS          |
| **WF_MASTER — Orchestration**     | FINAL CONTROL |

### What the Audit Confirmed

The final audit established that:

* the core workflows were completed;
* validation controls were passed;
* analytical outputs were reconciled;
* identified discrepancies were investigated;
* root-cause findings were documented;
* final outputs were supported by traceable evidence.

This created a controlled link between:

**Data → Workflow → Analysis → Reconciliation → Audit Evidence**

### Final Audit Status

## **COMPLETE**

The project was not considered complete simply because the workflows executed successfully.

Completion was established after the outputs had been **validated, reconciled, investigated where necessary, and supported by documented audit evidence**.

> **The project was not only built to produce results. It was controlled to prove that the results could be trusted.**

### Evidence & Traceability

`Final_Audit_Manual_Python_Financial_Analysis_EN.md`

# 14 — VISUALIZATION & REPORTING

The visualization stage transformed validated analytical results into **clear, business-oriented outputs**.

WF5 generated:

* Analytical charts
* Dashboard outputs
* PDF reports
* Automated reporting content

Visualization was treated as the **communication layer** of the analytical process.

The objective was not to create charts simply because visualization was required.

The objective was to make validated results:

**easier to understand, easier to compare, and easier to act upon.**

Each visualization was therefore designed to support a business question rather than simply display data.

> **A visualization becomes valuable when it helps decision-makers understand what happened, why it matters, and where action may be needed.**

# 15 — AUTOMATION

The project evolved from individual workflow stages into an **end-to-end automated orchestration model**.

### WF_MASTER

The master workflow coordinates:

**WF1 → WF2 → WF3 → WF4 → WF5**

creating a controlled execution path from:

**Source Data → Cleaning → Validation → Analysis → Visualization**

Automation provides:

* **Repeatability** — the process can be executed consistently.
* **Consistency** — each stage follows a defined workflow.
* **Reduced manual intervention** — fewer repetitive handoffs.
* **Clear workflow boundaries** — each stage has a defined responsibility.
* **Traceability** — outputs can be followed across the workflow.

### Why the Automation Matters

The technical achievement is not simply **using n8n**.

The real achievement is designing an automated process in which individual analytical stages can be **connected, executed, validated, and traced as one controlled system**.

This makes the workflow more suitable for repeatable analytical operations rather than one-time manual analysis.

> **The value of automation is not simply doing the work faster. It is making the process repeatable, controlled, and traceable.**

# 16 — TECHNICAL CAPABILITY

This project demonstrates practical capability across **data, automation, and analytical engineering**.

### SQL / MySQL

Database querying, transactional data handling, aggregation, and structured analytical data preparation.

### Python

Data cleaning, validation, reconciliation, analysis, and analytical control.

### Pandas

Data transformation, aggregation, matching, and structured analytical processing.

### Matplotlib

Business-oriented charts and analytical visualization.

### n8n

Workflow orchestration, system integration, automated processing, and end-to-end execution.

### Docker

Containerized execution environments, service isolation, and multi-service architecture.

### Analytical Engineering

Connecting databases, Python services, validation processes, analytical workflows, and reporting into **one repeatable and traceable system**.

### What This Demonstrates

The technical value is not simply familiarity with individual tools.

It is the ability to **combine them into a working analytical system** where data can move from source to validated business output through a controlled process.

> **The strength is not the number of tools used. It is the ability to make the tools work together to solve a real analytical problem.**

# 17 — WHAT THIS PROJECT DEMONSTRATES

This project demonstrates the ability to connect **technical execution, analytical reasoning, and business impact**.

### BUSINESS

The ability to turn analytical findings into business questions and priorities.

Examples:

* **Customer risk →** retention priority
* **Revenue discrepancy →** financial reliability
* **Transaction population →** reporting accuracy
* **Visualization →** clearer decision communication

### ANALYTICAL

The ability to:

* Validate assumptions
* Reconcile independent results
* Investigate discrepancies
* Trace root causes
* Build evidence
* Distinguish symptoms from causes
* Avoid conclusions that are not supported by evidence

### TECHNICAL

The ability to:

* Query and work with MySQL data
* Process and analyze data with Python and Pandas
* Build structured analytical workflows
* Automate processing with n8n
* Run services in Docker-based environments
* Produce analytical visualizations and reports

### What Connects Them

The value of the project comes from connecting these three layers:

**Technical execution**
produces reliable data and outputs.

↓

**Analytical reasoning**
tests, reconciles, and explains those outputs.

↓

**Business thinking**
turns validated evidence into meaningful decisions.

> **Technical execution produces data. Analytical thinking turns data into evidence. Business thinking turns evidence into value.**

# 18 — KEY ACHIEVEMENTS

### 01 — Established the Validated Revenue

## **Rp110,380,250,000**

Established from the final validated transaction population and supported by reconciliation and audit evidence.

### 02 — Investigated a Rp5.477.750.000 Revenue Difference

The project identified and investigated the difference between:

**Validated Revenue:** Rp110,380,250,000
**Legacy n8n Revenue:** Rp104,902,500,000

The investigation traced the difference to a **historical 4,745-record artifact versus the validated 5,000-transaction population**, while clearly separating confirmed evidence from mechanisms that could not be conclusively proven.

### 03 — Validated 5,000 Transactions

Established and reconciled the final transaction population:

**5,000 Transactions · 27,400 Units · Rp110,380,250,000 Revenue**

### 04 — Identified Customer Retention Risk

**734 customers / 39.72%**

were classified as **At-Risk Customers (Risiko Hilang)** within the validated customer population of **1,848 customers**.

As the largest customer segment, this finding identifies **customer retention as a clear business priority** for targeted follow-up and reactivation strategies.


### 05 — Built a Controlled End-to-End Workflow

Completed and orchestrated:

**WF1 → WF2 → WF3 → WF4 → WF5**

through **WF_MASTER**, creating a repeatable path from source data to validated analytical output.

### 06 — Established Auditability

Key analytical results were supported by:

**Reconciliation → Investigation → Evidence → Final Audit**

This created a traceable connection between the underlying data, analytical results, and final business conclusions.

---

## FINAL PROJECT OUTCOME

The project delivered more than automated analysis.

It established a workflow in which data could be:

**Processed → Validated → Reconciled → Investigated → Explained → Audited**

> **The result is not simply a set of numbers. It is a set of numbers with evidence behind them.**

# 19 — THE ANALYST'S APPROACH

The project follows a simple analytical principle:

**Question the data.**

**Validate the result.**

**Investigate the difference.**

**Find the cause.**

**Turn the finding into business meaning.**

This approach reflects how real-world analytical work often operates.

Data does not always align.
Systems do not always produce the same result.
And a number is not automatically correct simply because a system produced it.

The real value of an analyst becomes visible when the data becomes difficult.

> **A good analyst explains what happened. A strong analyst investigates why it happened — and can support the answer with evidence.**

# 20 — CLOSING

## From Data to Decision Confidence

This project demonstrates an end-to-end approach to data analytics:

**Raw Data**
→ **Clean Data**
→ **Validated Data**
→ **Analysis**
→ **Reconciliation**
→ **Root Cause Investigation**
→ **Business Insight**
→ **Automated Reporting**

The project brings together **Business Understanding, Analytical Thinking, and Technical Execution** within one controlled workflow.

The final outcome is more than a collection of scripts, dashboards, or reports.

It demonstrates the ability to build an analytical process that is:

**Accurate.**
**Traceable.**
**Reproducible.**
**Auditable.**
**Business-oriented.**

### Final Message

> **Reliable analytics is not about producing more numbers.
> It is about producing numbers that can be trusted, explained, and used to make better decisions.**

---

## CONTACT

**Data Analyst**

**Email:** Soleilbenidata@gmail.com

**GitHub:** https://github.com/VibaSoleil/Data-Analytics-Portfolio


**Portfolio:** `Project_01_Data_Analyst / ODC Bag 8`

## Workflow 1
![Workflow 1](Foto_WF_01_Data_Extraction_MySQL_to_CSV_n8n.jpg)

## Workflow 2
![Workflow 2](Foto_WF_02_Data_Cleaning_n8n.jpg)

## Workflow 3
![Workflow 3](Foto_WF_03_Data_Quality_Validation_n8n.jpg)

## Workflow 4
![Workflow 4](Foto_WF_04_Data_Analysis_Report_n8n.jpg)

## Workflow 5
![Workflow 5](Foto_WF_05_Data_Visualization_n8n.jpg)

## WF MASTER
![WF MASTER](Foto_WF_MASTER_Project_01_Data_Analyst.jpg)

## Business Dashboard — Final PNG
![Business Dashboard — Final](ODC_Business_Dashboard_n8n.png)

## Business Dashboard — Final PDF
[Business Dashboard — Final PDF](ODC_Business_Dashboard_n8n.pdf)
