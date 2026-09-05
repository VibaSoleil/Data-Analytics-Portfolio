WF_04_DATA_ANALYSIS_REPORT_N8N
FINAL STATUS & AUDIT SUMMARY

Project: Project_01_Data_Analyst
Workflow: WF_04_Data_Analysis_Report_n8n
Status Date: 12 August 2026
Final Execution Status: 🟢 SUCCESS
Analysis Status: 🟢 COMPLETED
Input Validation Status: 🟢 PASS
Reconciliation Status: 🟢 PASS
Exception Status: 🟢 PASS

1. EXECUTIVE SUMMARY

WF_04_Data_Analysis_Report_n8n has been successfully executed through the dedicated Data Analysis Report Engine and integrated n8n workflow.

WF4 performs structured data analysis after the completion of:

WF1 — Data Extraction
WF2 — Data Cleaning
WF3 — Data Quality Validation

The workflow uses batch processing with:

Batch Size: 100 records

The full workflow execution completed successfully.

The verified Analysis Engine response returned:

analysis_status = COMPLETED
input_validation.status = PASS
total_records = 100
reconciliation_status = PASS
exception_status = PASS

The verified analytical checks returned:

Formula failures: 0
Negative quantity records: 0
Negative revenue records: 0
Invalid transaction dates: 0
Total exception flags: 0
Duplicate transaction IDs: 0
Financial reconciliation: MATCH

The workflow successfully processed the canonical dataset through the configured batch-processing architecture.

2. WORKFLOW STATUS
Workflow	Function	Final Status
WF1	Data Extraction	✅ COMPLETE / FROZEN
WF2	Data Cleaning	✅ COMPLETE / FROZEN
WF3	Data Quality Validation	🟢 COMPLETE / PASS / FROZEN
WF4	Data Analysis Report	🟢 COMPLETE / PASS
WF5	Data Visualization	⏳ NOT STARTED
3. WF4 OBJECTIVE

WF4 is designed to perform structured analytical processing against the canonical cleaned dataset and generate analytical evidence and business insights.

The analysis covers:

Record-level analytical processing
Transaction analysis
Product performance
Customer performance
Financial analysis
Exception analysis
Data reliability checks
Reconciliation
Business insight generation

WF4 is also designed to ensure that analytical processing does not modify the canonical input dataset.

4. CANONICAL INPUT

WF4 uses the canonical cleaned dataset established by the previous workflow stages:

Company_Data_Cleaned_n8n.csv

Previously verified canonical dataset:

Total Records: 5,000
Total Columns: 14

The canonical dataset remains unchanged.

WF4 uses the dataset as an analytical input and does not perform data cleaning or recreation of the canonical dataset.

5. ANALYSIS ENGINE

Dedicated Analysis Engine:

Data_Analysis_Report_Engine_n8n.py

Dedicated Docker container:

wf4-analysis-engine

API configuration:

Container Port: 8000
Host Port: 8003

The Analysis Engine is responsible for:

Analytical processing
Financial analysis
Customer analysis
Product analysis
Exception detection
Reconciliation
Business insight generation
Analytical evidence generation

WF4 uses a dedicated analytical service and does not call the existing WF2 /clean endpoint.

This preserves the separation between:

WF2 = Data Cleaning

and

WF4 = Data Analysis

6. API ARCHITECTURE

WF4 architecture:

n8n
│
├── When clicking Execute Workflow
│
├── Read/Write Files from Disk
│
├── Extract From File
│
├── Loop Over Items
│      Batch Size = 100
│
├── HTTP Request
│      POST /analyze
│
└── Code in JavaScript
       │
       └── Return to Loop Over Items

Dedicated Analysis API:

wf4-analysis-engine
│
└── Port 8000
       │
       └── /analyze

Host mapping:

localhost:8003
       ↓
wf4-analysis-engine:8000

The /analyze endpoint is dedicated to WF4 analytical processing.

7. N8N WF4 INTEGRATION

The final n8n workflow structure is:

When clicking Execute Workflow
        ↓
Read/Write Files from Disk
        ↓
Extract From File
        ↓
Loop Over Items
        ↓
HTTP Request
        ↓
Code in JavaScript
        ↩
Loop Over Items
Loop Configuration

Batch Size: 100

Canonical input:

5,000 records

Batch calculation:

5,000 ÷ 100 = 50 batches

Therefore:

50 batches × 100 records = 5,000 records

The Loop Over Items node successfully completed the configured batch-processing cycle.

HTTP Request Configuration

Method:
POST

URL:

http://wf4-analysis-engine:8000/analyze

Authentication:
None

Send Query Parameters:
OFF

Send Headers:
OFF

Send Body:
ON

Body Content Type:
JSON

JSON Body:

{{ { "records": $input.all().map(item => item.json) } }}

This configuration sends the records received by the current loop iteration to the Analysis Engine as the records array.

8. ANALYSIS RESULT

The WF4 Analysis Engine successfully returned analytical results.

Verified batch response:

analysis_status       : COMPLETED
input_validation      : PASS
total_records         : 100

The final evidence section of the verified response returned:

input_records             : 100
analysis_engine_records   : 100
reconciliation_status     : PASS
exception_status          : PASS

This confirms that the number of records received by the Analysis Engine matched the number of records processed by the engine for the verified batch.

Financial Analysis

Verified financial result:

total_revenue               : 4,870,500,000
total_financial_income      : 4,870,500,000
difference_revenue_income   : 0
status                      : MATCH

Result:

FINANCIAL RECONCILIATION = PASS

Audit Note:

The 4,870,500,000 value shown above belongs to the verified analytical batch of 100 records.

It must not be interpreted as the total revenue of the complete 5,000-record dataset.

No overall 5,000-record revenue KPI is recorded in this report unless an aggregated full-dataset evidence is separately verified.

Customer Analysis

The Analysis Engine successfully generated customer-performance insights.

Verified example:

Customer:
Okto Wibisono

Transactions:
2

Units:
17

Revenue:
144,500,000

The engine generated the finding:

Customer with the highest revenue in the analyzed batch was Okto Wibisono.

This finding is treated as batch-level analytical evidence, not as a full-dataset customer ranking.

Regional Analysis

Regional analysis returned:

status = NOT_AVAILABLE

Reason:

No dedicated regional field is available in the canonical dataset.

Available regional columns:

[]

This result is not an analytical failure.

The engine correctly avoided generating unsupported regional analysis because the canonical dataset does not contain a dedicated regional field.

9. ANALYSIS CHECKS

The Analysis Engine performed the following analytical checks.

Record Count Reconciliation
record_count_matches_input = true

Result: PASS

Duplicate Transaction ID
no_duplicate_transaction_ids = true

Result: PASS

Formula Validation
formula_failures = 0
no_formula_failures = true

Result: PASS

Negative Quantity Validation
negative_quantity_records = 0

Result: PASS

Negative Revenue Validation
negative_revenue_records = 0

Result: PASS

Transaction Date Validation
invalid_transaction_dates = 0

Result: PASS

Exception Validation
total_exception_flags = 0
status = PASS

Result: PASS

Financial Reconciliation
difference_revenue_vs_income = 0
status = MATCH

Result: PASS

10. ANALYSIS EVIDENCE

The verified Analysis Engine response contains evidence for:

Input Records
input_records = 100
Analysis Engine Records
analysis_engine_records = 100
Reconciliation
reconciliation_status = PASS
Exception Analysis
exception_status = PASS
Financial Reconciliation
total_revenue = 4,870,500,000
total_financial_income = 4,870,500,000
difference_revenue_vs_income = 0
status = MATCH
Data Reliability
formula_failures = 0
negative_quantity_records = 0
negative_revenue_records = 0
invalid_transaction_dates = 0
total_exception_flags = 0
status = PASS
11. EVIDENCE RESULTS
Record Count Evidence

Input records:

100

Analysis Engine records:

100

Result:

PASS

Duplicate Evidence

Duplicate transaction IDs:

0

Result:

PASS

Formula Evidence

Formula failures:

0

Result:

PASS

Negative Quantity Evidence

Negative quantity records:

0

Result:

PASS

Negative Revenue Evidence

Negative revenue records:

0

Result:

PASS

Date Evidence

Invalid transaction dates:

0

Result:

PASS

Exception Evidence

Total exception flags:

0

Result:

PASS

Financial Evidence

Revenue:

Rp4,870,500,000

Financial income:

Rp4,870,500,000

Difference:

Rp0

Result:

MATCH / PASS

12. FINAL API RESULT

The dedicated /analyze API successfully received requests from the n8n workflow and returned analytical responses.

Verified API result:

API STATUS            : SUCCESS
ANALYSIS STATUS       : COMPLETED
INPUT VALIDATION      : PASS
RECORD RECONCILIATION : PASS
EXCEPTION STATUS      : PASS
FINANCIAL STATUS      : MATCH

The API successfully executed the dedicated Data Analysis Engine against the records supplied by the n8n batch-processing workflow.

13. FINAL AUDIT RESULT

Final WF4 audit verified:

Audit Component	Status
Canonical Input	✅ PASS
Workflow Structure	✅ PASS
Loop Over Items	✅ PASS
Batch Size 100	✅ PASS
HTTP Request Integration	✅ PASS
/analyze API	✅ PASS
Analysis Engine	✅ COMPLETED
Input Validation	✅ PASS
Record Count Reconciliation	✅ PASS
Duplicate Transaction ID Check	✅ PASS
Formula Validation	✅ PASS
Negative Quantity Check	✅ PASS
Negative Revenue Check	✅ PASS
Transaction Date Check	✅ PASS
Financial Reconciliation	✅ MATCH
Exception Analysis	✅ PASS
Business Insight Generation	✅ PASS
Final Audit Conclusion

WF4 analytical execution successfully completed and passed the verified analytical checks.

14. FROZEN COMPONENTS

The following previously completed components remain frozen:

WF1

WF1 — Data Extraction

Status:

COMPLETE / FROZEN

WF2

WF2 — Data Cleaning

Status:

COMPLETE / FROZEN

WF3

WF3 — Data Quality Validation

Status:

COMPLETE / PASS / FROZEN

Canonical Dataset

Company_Data_Cleaned_n8n.csv

WF4 Analysis Engine

Data_Analysis_Report_Engine_n8n.py

WF4 Analysis Container

wf4-analysis-engine

WF4 API

POST /analyze

No modification should be made to completed components unless a verified defect or controlled enhancement is formally identified.

15. FINAL WF4 DECISION

WF_04_Data_Analysis_Report_n8n has successfully completed its configured analytical workflow execution.

Final verified status:

🟢 COMPLETE / PASS

WF4 successfully demonstrated:

Successful n8n execution
Batch processing with Batch Size 100
Successful /analyze API integration
Successful Analysis Engine execution
analysis_status = COMPLETED
input_validation = PASS
Record reconciliation = PASS
Financial reconciliation = MATCH
Exception analysis = PASS
Formula failures = 0
Negative quantity records = 0
Negative revenue records = 0
Invalid transaction dates = 0
Exception flags = 0
Successful analytical insight generation
Current Project Milestone
WF1  ✅ COMPLETE / FROZEN
WF2  ✅ COMPLETE / FROZEN
WF3  🟢 COMPLETE / PASS / FROZEN
WF4  🟢 COMPLETE / PASS
WF5  ⏳ NOT STARTED
16. AUDIT TRAIL NOTE

This document records the final execution state of:

WF_04_Data_Analysis_Report_n8n

following successful n8n integration and execution of the dedicated Data Analysis Report Engine.

The audit verification covered:

workflow architecture;
Loop Over Items configuration;
batch processing;
HTTP /analyze integration;
Analysis Engine execution;
input validation;
record reconciliation;
financial reconciliation;
exception analysis;
data reliability checks;
business insight generation.

All conclusions recorded in this document are based on verified execution evidence.

Batch-level analytical values are explicitly distinguished from full-dataset values.

The verified financial value of Rp4,870,500,000 is therefore recorded as a 100-record batch result and is not presented as the final 5,000-record project revenue.

Regional analysis is recorded as NOT AVAILABLE because no dedicated regional field exists in the canonical dataset. This is treated as a documented data-field limitation rather than an analytical engine failure.

WF4 uses the dedicated:

Data_Analysis_Report_Engine_n8n

through:

POST /analyze

and does not reuse the WF2 /clean endpoint for analytical processing.

The workflow completed successfully and all verified analytical checks returned PASS or MATCH where applicable.

FINAL WF4 STATUS
🟢 WF_04_Data_Analysis_Report_n8n
COMPLETE / PASS

Final Execution: 🟢 SUCCESS
Analysis Engine: 🟢 COMPLETED
Input Validation: 🟢 PASS
Reconciliation: 🟢 PASS
Exception Analysis: 🟢 PASS
Financial Reconciliation: 🟢 MATCH

17. POST-EXECUTION AUDIT ADDENDUM

Purpose

This section is added to document cross-module findings that became relevant after comparing the WF4 evidence with the Regional Analysis evidence.

This addition does not modify the WF4 execution result, which has been declared COMPLETE / PASS.

17.1 REGIONAL FIELD VALIDATION

WF4 Analysis Engine performs a verification of the availability of a dedicated regional field in the canonical dataset.

Verified result:

regional_analysis.status = NOT_AVAILABLE

Message:

No dedicated regional field is available in the canonical dataset.

Available regional columns:

[]

Audit Interpretation:

WF4 does not generate a canonical regional analysis because the canonical dataset does not contain a dedicated regional field.

Status:

🟢 WF4 REGIONAL FIELD CHECK = PASS

The NOT_AVAILABLE result represents a data field limitation and not a workflow failure.

17.2 RELATIONSHIP TO PREVIOUS REGIONAL EVIDENCE

The previous Regional Analysis evidence contains analytical outputs generated through derived location extraction from the customer address field.

The previous process uses:

alamat
   ↓
city extraction
   ↓
kota
   ↓
derived regional analysis

Therefore, the previous Regional Analysis outputs must be classified as:

DERIVED ANALYTICAL EVIDENCE

and not as:

CANONICAL REGIONAL DATA

This classification does not remove or invalidate the previous regional evidence. It only defines the appropriate analytical and data governance boundaries for the use of that evidence.

17.3 DISCREPANCY IN REGIONAL OUTPUTS

A discrepancy has been identified in the Regional Analysis evidence concerning the potential region result.

Output A:

Region_Analysis_Summary_n8n.json

Result:

Pariaman — Potential Score 107

Output B:

ODC_Bag8_FinalReport_05_REGION_Professional_n8n.json

Result:

Pekalongan — Potential Score 107

The score value is identical:

107

but the reported region name is different.

Status:

🟠 RECONCILIATION REQUIRED

This discrepancy is not classified as a WF4 execution failure because the differing values originate from the Regional Analysis evidence and not from the WF4 batch execution verified in this report.

The discrepancy must not be resolved based on an assumption or by selecting one of the results without reconciliation against the sources that produced both outputs.

17.4 CROSS-MODULE AUDIT INTERPRETATION

The WF4 evidence establishes:

Analysis Execution = COMPLETED
Input Validation = PASS
Record Reconciliation = PASS
Exception Status = PASS
Financial Reconciliation = MATCH
Dedicated Regional Field = NOT AVAILABLE

Meanwhile, the Regional Analysis evidence establishes:

Derived Regional Analysis = AVAILABLE
Canonical Dedicated Regional Field = NOT AVAILABLE
Potential Region Output = DISCREPANCY IDENTIFIED

Therefore, the correct cross-module interpretation is:

WF4 Analysis
        ↓
Dedicated Regional Field
        ↓
NOT AVAILABLE

Previous Regional Analysis
        ↓
Address-derived City
        ↓
DERIVED ANALYTICAL EVIDENCE
        ↓
Potential Region Discrepancy
        ↓
RECONCILIATION REQUIRED

17.5 GOVERNANCE DECISION

No modification is required to:

WF1
WF2
WF3
WF4 Analysis Engine
Canonical Dataset
WF4 API
WF4 Workflow Configuration

based solely on the Regional Analysis discrepancy.

The discrepancy is recorded as an audit finding and will be addressed during the final cross-module reconciliation stage.

17.6 FINAL WF4 ADDENDUM DECISION

WF4 Execution Status:

🟢 COMPLETE / PASS

WF4 Analytical Validation:

🟢 PASS

Dedicated Regional Field:

🔵 NOT AVAILABLE

Previous Address-Derived Regional Evidence:

🟡 DERIVED / NON-CANONICAL

Potential Regional Output:

🟠 RECONCILIATION REQUIRED

WF4 Defect Identified:

❌ NONE

Final Interpretation:

The regional limitation and the discrepancy in the Regional Analysis outputs do not invalidate the verified WF4 execution.

WF4 therefore retains the status:

🟢 COMPLETE / PASS

The regional findings are recorded as a cross-module audit finding and will be incorporated into the final project reconciliation without modifying the validated WF4 execution.

END OF WF4 POST-EXECUTION AUDIT ADDENDUM