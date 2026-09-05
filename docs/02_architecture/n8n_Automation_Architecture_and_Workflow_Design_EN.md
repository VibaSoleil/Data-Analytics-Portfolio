PROJECT DATA ANALYTICS AUTOMATION WORKFLOW (n8n)
FINAL AUTOMATION ARCHITECTURE & WORKFLOW DESIGN

Project: Project_01_Data_Analyst
Automation Platform: n8n
Database: perusahaan_db
Architecture Type: Modular Workflow + Master Orchestration
Final Workflow Chain: WF1 → WF2 → WF3 → WF4 → WF5
Master Workflow: WF_MASTER_Project_01_Data_Analyst

1. ARCHITECTURE OVERVIEW

Project Project_01_Data_Analyst uses a modular workflow-based automation architecture with n8n as the orchestration platform.

The architecture is designed so that each stage of data processing has a separate workflow and responsibility.

The final structure consists of:

DATA SOURCE
     |
     v
WF1 — Data Extraction
     |
     v
WF2 — Data Cleaning
     |
     v
WF3 — Data Quality Validation
     |
     v
WF4 — Data Analysis Report
     |
     v
WF5 — Data Visualization

All individual workflows can then be executed in an integrated manner through:

WF_MASTER_Project_01_Data_Analyst

The Master Workflow functions as the Orchestrator / Controller.

The Master does not replace the internal logic of WF1–WF5.

2. FINAL MASTER ORCHESTRATION

The final Master Workflow architecture is:

START
  |
  v
Start_Execute Master Workflow
  |
  v
HTTP Request
  |
  v
WF1 — Data Extraction
  |
  v
HTTP Request1
  |
  v
WF2 — Data Cleaning
  |
  v
HTTP Request2
  |
  v
WF3 — Data Quality Validation
  |
  v
HTTP Request3
  |
  v
WF4 — Data Analysis Report
  |
  v
HTTP Request4
  |
  v
WF5 — Data Visualization
  |
  v
END

The Master Workflow calls individual workflows through the Production Webhook mechanism.

With this approach, each workflow remains independent and can be maintained separately.

3. DATA SOURCE ARCHITECTURE

The primary data source comes from the MySQL database:

Database:

perusahaan_db

The database contains four main tables:

produk
pelanggan
transaksi
keuangan

Database verification results:

Table	Records
produk	5
pelanggan	2,002
transaksi	5,000
keuangan	5,000

The total number of transactions used as the main basis for analysis is:

5,000 transactions

Transaction period:

2025-07-08
to
2026-07-08

Total revenue:

Rp110,380,250,000

Average transaction:

Rp22,076,050
4. DATABASE STRUCTURE
4.1 Table produk

Structure:

id_produk
nama_produk
harga
stok

Primary Key:

id_produk
4.2 Table pelanggan

Structure:

id_pelanggan
nama_pelanggan
alamat
no_telepon

Primary Key:

id_pelanggan
4.3 Table transaksi

Structure:

id_transaksi
id_pelanggan
id_produk
tanggal_transaksi
jumlah
total_harga

Primary Key:

id_transaksi
4.4 Table keuangan

Structure:

id_keuangan
id_transaksi
tanggal
pemasukan
keterangan

Primary Key:

id_keuangan

id_transaksi has a relationship with table transaksi.

5. DATABASE RELATIONSHIP

The verified database relationship is:

pelanggan
    |
    | id_pelanggan
    v
transaksi
    |
    | id_produk
    v
produk

transaksi
    |
    | id_transaksi
    v
keuangan

Foreign keys:

transaksi.id_pelanggan
    → pelanggan.id_pelanggan

transaksi.id_produk
    → produk.id_produk

keuangan.id_transaksi
    → transaksi.id_transaksi

This relationship ensures that transaction data can be associated with customer, product, and financial records.

6. DATA INTEGRITY BASELINE

Validation of the transaction and financial relationships produced:

Total transactions              = 5,000
Transactions with finance       = 5,000
Transactions without finance    = 0
Value match                     = 5,000
Value mismatch                  = 0

Therefore, all transactions have a corresponding financial record, and all income values match the total_harga of the transactions in the verification performed.

7. WF1 — DATA EXTRACTION

WF1 is the first workflow in the pipeline.

Responsibility

WF1 is responsible for the data extraction process from the data source.

Architecture:

Trigger / Production Webhook
        |
        v
MySQL
        |
        v
Data Extraction
        |
        v
Output Dataset

Data used as the extraction source:

produk
pelanggan
transaksi
keuangan

WF1 is not responsible for analysis or visualization.

Final Status

WF1 = COMPLETE / FROZEN
8. WF2 — DATA CLEANING

WF2 is the second workflow.

Architecture:

Trigger / Production Webhook
        |
        v
Read Dataset
        |
        v
Data Cleaning
        |
        v
Clean Dataset
        |
        v
Output

The cleaning process is performed using Python-based processing according to the project implementation.

WF2 is responsible for the data cleaning process and does not replace validation in WF3.

Final Status

WF2 = COMPLETE / FROZEN
9. WF3 — DATA QUALITY VALIDATION

WF3 is the third workflow.

WF3 has its own validation service:

wf3-validation-api

The service runs using the internal endpoint:

http://wf3-validation-api:8000/validate

Architecture:

WF2
 |
 v
WF3 Production Webhook
 |
 v
wf3-validation-api
 |
 v
Validation Result

Validation includes:

Missing values
Duplicate rows
Duplicate Transaction ID
Numeric validation
Date validation
Transaction formula
Financial consistency

Final validation results:

HTTP STATUS        = 200
api_status         = SUCCESS
validation_status  = PASS
total_records      = 5000
Missing values     = 0
Duplicate rows     = 0
Duplicate ID       = 0
Numeric validation = PASS
Date validation    = PASS
Transaction formula = PASS
Financial consistency = PASS
overall_status     = PASS

Final Status

WF3 = COMPLETE / PASS / FROZEN
10. WF4 — DATA ANALYSIS REPORT

WF4 is the fourth workflow.

WF4 uses its own analysis engine:

wf4-analysis-engine

Architecture:

WF3
 |
 v
WF4 Production Webhook
 |
 v
wf4-analysis-engine
 |
 v
Business Analysis
 |
 v
Analysis Report

WF4 is responsible for the business analysis process and generation of analysis results.

The analysis uses transaction data that has passed through the extraction, cleaning, and validation stages.

Final Status

WF4 = COMPLETE / PASS
11. WF5 — DATA VISUALIZATION

WF5 is the final workflow in the processing sequence.

Architecture:

WF4
 |
 v
WF5 Production Webhook
 |
 v
Dashboard / Visualization Engine
 |
 +--> Dashboard PNG
 |
 +--> Dashboard PDF
 |
 +--> Email Report

WF5 is responsible for the visualization and dashboard reporting processes.

Outputs that are part of the workflow include:

Dashboard PNG
Dashboard PDF
Email Report

WF5 uses the canonical transaction dataset as the dashboard input.

Canonical dataset:

/app/OUTPUT/Company_Data_Cleaned_n8n.csv

The dataset contains:

5,000 data records
14 columns

With the header row, the total number of lines in the file is:

5,001 lines

The tanggal_transaksi column is available and used by the dashboard processing.

Final Status

WF5 = COMPLETE / PASS
12. CANONICAL DATASET CONTROL

The canonical dataset must be distinguished from other artifacts or outputs that may be generated during workflow processing.

Canonical transaction dataset:

/app/OUTPUT/Company_Data_Cleaned_n8n.csv

Artifact previously found to be unsuitable for the dashboard:

/app/OUTPUT/DATA/Company_Data_Cleaned_n8n.csv

The artifact previously contained JSON validation output and therefore could not be used as the transaction dashboard input.

This finding became part of the WF5 troubleshooting and corrective action.

Final principle:

Dashboard
    |
    v
Canonical Transaction Dataset
    |
    v
5,000 records
    |
    v
14 columns
    |
    v
tanggal_transaksi available
13. BUSINESS ANALYSIS COMPONENTS

Business analysis in the project covers several main areas:

Data Understanding
Sales Analysis
Customer Analysis
Regional Analysis
Transaction Analysis
Financial Analysis

Scripts related to business analysis:

ODC_Bag1_DataUnderstanding.py
ODC_Bag2_DataCleaning.py
ODC_Bag3_SalesAnalysis.py
ODC_Bag4_CustomerAnalysis.py
ODC_Bag5_RegionalAnalysis.py
ODC_Bag6_TransactionAnalysis.py
ODC_Bag7_FinancialAnalysis.py

These scripts remain under the responsibility of their respective processing stages and are not moved into the Master Workflow logic.

14. VISUALIZATION COMPONENTS

Visualization is used to present analysis results in visual form.

The components designed in the architecture include:

Revenue Trend
Product Chart
Customer Chart
Region Chart
Pareto Analysis

The final dashboard uses:

ODC_Bag8_FinalReport_09_DASHBOARD.py

Regional Analysis continues to follow data availability and the logic established in the final workflow.

15. WORKFLOW RESPONSIBILITY MATRIX
Workflow	Primary Responsibility	Final Status
WF1	Data Extraction	COMPLETE / FROZEN
WF2	Data Cleaning	COMPLETE / FROZEN
WF3	Data Quality Validation	COMPLETE / PASS / FROZEN
WF4	Data Analysis Report	COMPLETE / PASS
WF5	Data Visualization	COMPLETE / PASS
WF_MASTER	Orchestration / Controller	COMPLETE / PASS
16. MASTER WORKFLOW RESPONSIBILITY

Master Workflow:

WF_MASTER_Project_01_Data_Analyst

The Master functions as:

ORCHESTRATOR / CONTROLLER

The Master is responsible for managing the execution sequence:

WF1
 ↓
WF2
 ↓
WF3
 ↓
WF4
 ↓
WF5

The Master does not perform:

Data Cleaning
Data Validation
Business Analysis
Data Visualization
Reconciliation Calculation
Replacement of Individual Workflow Logic

Thus, the Master remains at the orchestration layer and does not take over the responsibilities of the individual workflows.

17. MASTER NODE MAPPING

Final Master Workflow mapping:

Order	Master Node	Target
1	Start_Execute Master Workflow	Start
2	HTTP Request	WF1
3	HTTP Request1	WF2
4	HTTP Request2	WF3
5	HTTP Request3	WF4
6	HTTP Request4	WF5

Final architecture:

Start_Execute Master Workflow
            |
            v
       HTTP Request
            |
            v
           WF1
            |
            v
       HTTP Request1
            |
            v
           WF2
            |
            v
       HTTP Request2
            |
            v
           WF3
            |
            v
       HTTP Request3
            |
            v
           WF4
            |
            v
       HTTP Request4
            |
            v
           WF5
18. PRODUCTION WEBHOOK ARCHITECTURE

Each individual workflow is used through a Production Webhook for Master integration.

Integration pattern:

MASTER
   |
   v
HTTP Request
   |
   v
Production Webhook
   |
   v
Target Workflow

With this pattern, the Master does not need to copy the nodes or internal logic of WF1–WF5.

Architecture advantages:

Modular
Traceable
Testable
Maintainable
Auditable
19. TROUBLESHOOTING ARCHITECTURE

During implementation, several integration issues were identified and resolved.

19.1 WF3 — ECONNREFUSED

Initial issue:

ECONNREFUSED

Previous endpoint:

http://python-project-container:8002/validate

The endpoint was then adjusted to:

http://wf3-validation-api:8000/validate

The change was made based on the actual service architecture used by WF3.

Result:

WF3 = PASS
19.2 WF4 — ENOTFOUND

Issue:

ENOTFOUND wf4-analysis-engine

Root cause:

wf4-analysis-engine

was not active at the time of that test.

Corrective action:

Activate wf4-analysis-engine

After the engine became available, WF4 was successfully executed.

Result:

WF4 = PASS
19.3 WF5 — Incorrect Dataset Artifact

Issue:

KeyError: 'tanggal_transaksi'

Root cause:

The Dashboard received an incorrect CSV artifact as input.

The canonical dataset was then verified and the input path was corrected.

Result:

WF5 = PASS
20. DOCKER RUNTIME ARCHITECTURE

The Docker environment used in the project includes:

mysql-server
n8n
python-project-container
wf3-validation-api
wf4-analysis-engine

The main runtime active during the last inspection:

python-project-container
n8n
mysql-server

Containers:

wf3-validation-api
wf4-analysis-engine

are dedicated services used in their respective workflows, and their runtime status during the last inspection was not used as a substitute for evidence of previous workflow execution.

Docker network used:

n8n-network

The network connects the runtime components required for internal communication between services.

21. PROJECT DIRECTORY ARCHITECTURE

Main project structure:

Project_01_Data_Analyst
├── DATA_RAW
├── DATABASE
├── SCRIPT
├── OUTPUT
└── README.md

The canonical data output is located within the established project structure.

Final canonical n8n dataset:

D:\Project_01_Data_Analyst\OUTPUT\DATA\Company_Data_Cleaned_n8n.csv

This path is the project host path associated with the n8n dataset.

22. SECURITY & CREDENTIAL HANDLING

Database credentials and service authentication are not included in the architecture documentation.

Sensitive information such as:

Password
Credential
Authentication Secret
API Key

is not part of the technical documentation.

Credentials are managed through the appropriate environment or credential management mechanism at runtime.

23. ARCHITECTURAL DESIGN PRINCIPLES

The final architecture follows these principles:

23.1 Modularity

Each workflow has a clearly defined function.

23.2 Separation of Responsibility

Extraction, cleaning, validation, analysis, and visualization are not combined into a single large logic.

23.3 Traceability

Each stage can be traced through its respective workflow and execution.

23.4 Testability

Individual workflows can be tested before and after being integrated through the Master.

23.5 Maintainability

Changes to one workflow do not necessarily require changes to all other workflows.

23.6 Auditability

Execution, troubleshooting, corrective action, and final status can be documented.

24. FINAL EXECUTION ARCHITECTURE

Final end-to-end execution:

WF_MASTER_Project_01_Data_Analyst
                |
                v
               WF1
                |
                v
               WF2
                |
                v
               WF3
                |
                v
               WF4
                |
                v
               WF5
                |
                v
              END

During the final execution, the sequence successfully ran through WF5.

Execution evidence shows that all executed nodes were in a successful state.

Final result:

WF1 Execution = PASS
WF2 Execution = PASS
WF3 Execution = PASS
WF4 Execution = PASS
WF5 Execution = PASS

Master Orchestration = PASS

End-to-End Execution = PASS
25. FINAL ARCHITECTURAL STATUS
Component	Status
Database Source	VERIFIED
Database Structure	VERIFIED
Data Relationship	VERIFIED
Data Integrity	VERIFIED
WF1 — Data Extraction	COMPLETE / FROZEN
WF2 — Data Cleaning	COMPLETE / FROZEN
WF3 — Data Quality Validation	COMPLETE / PASS / FROZEN
WF4 — Data Analysis Report	COMPLETE / PASS
WF5 — Data Visualization	COMPLETE / PASS
Master Workflow	COMPLETE / PASS
End-to-End Orchestration	PASS
26. FINAL ARCHITECTURAL DECISION

The final implementation establishes the following architecture:

                    MASTER
                      |
                      v
                     WF1
              Data Extraction
                      |
                      v
                     WF2
               Data Cleaning
                      |
                      v
                     WF3
          Data Quality Validation
                      |
                      v
                     WF4
           Data Analysis Report
                      |
                      v
                     WF5
            Data Visualization

The Master Workflow remains as the orchestration layer.

Individual workflows remain responsible for their respective logic and processes.

The final architecture does not use a monolithic workflow approach that combines all WF1–WF5 logic into the Master.

27. FINAL RECORD
PROJECT
Project_01_Data_Analyst

DATABASE
perusahaan_db

MASTER WORKFLOW
WF_MASTER_Project_01_Data_Analyst

MASTER ROLE
ORCHESTRATOR / CONTROLLER

START NODE
Start_Execute Master Workflow

WF1 NODE
HTTP Request

WF2 NODE
HTTP Request1

WF3 NODE
HTTP Request2

WF4 NODE
HTTP Request3

WF5 NODE
HTTP Request4

WF3 VALIDATION SERVICE
wf3-validation-api

WF3 VALIDATION ENDPOINT
http://wf3-validation-api:8000/validate

WF4 ANALYSIS ENGINE
wf4-analysis-engine

WF5 CANONICAL DATASET
/app/OUTPUT/Company_Data_Cleaned_n8n.csv

TOTAL TRANSACTIONS
5000

TOTAL REVENUE
110380250000.00

AVERAGE TRANSACTION
22076050.000000

FINAL EXECUTION
SUCCESS

MASTER ORCHESTRATION
PASS

END-TO-END EXECUTION
PASS

FINAL MASTER STATUS
COMPLETE / PASS
28. CLOSURE

The Project_01_Data_Analyst architecture has evolved from an initial automation design into a modular implementation consisting of WF1–WF5 and one Master Workflow as the orchestration layer.

The final implementation maintains the separation of responsibilities between:

Data Extraction
        ↓
Data Cleaning
        ↓
Data Quality Validation
        ↓
Data Analysis Report
        ↓
Data Visualization

The Master Workflow manages the execution chain without taking over the internal logic of the individual workflows.

The architecture has undergone implementation, integration testing, troubleshooting, corrective action, retesting, and final end-to-end execution.

Final results:

WF1 → PASS
WF2 → PASS
WF3 → PASS
WF4 → PASS
WF5 → PASS

MASTER → PASS

END-TO-END → PASS

Therefore, the final architecture of Project_01_Data_Analyst is declared implemented, validated, modular, traceable, maintainable, and auditable based on the evidence and test results obtained.

END OF DOCUMENT


