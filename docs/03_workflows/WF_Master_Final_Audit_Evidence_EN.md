WF MASTER — FINAL AUDIT & ORCHESTRATION EVIDENCE

Project: Project_01_Data_Analyst
Master Workflow: WF_MASTER_Project_01_Data_Analyst
Document: WF_Master_Final_Audit_Evidence_EN.md
Language: English
Document Type: Final Technical Audit & Orchestration Evidence
Status: FINAL
Scope: WF1 → WF5 End-to-End Orchestration

PART 1 — EXECUTIVE SUMMARY
1.1 Objective

WF_MASTER_Project_01_Data_Analyst was created as an orchestration layer / control layer to execute the entire Project_01_Data_Analyst workflow sequence in a structured manner from a single execution point.

The Master Workflow does not replace WF1–WF5 and does not combine all WF1–WF5 nodes into a single workflow.

Each workflow retains its own responsibilities and logic.

The orchestrated sequence is:

WF1
↓
WF2
↓
WF3
↓
WF4
↓
WF5
1.2 Final Result

After the creation, integration, troubleshooting, correction, and testing processes, the Master Workflow successfully executed the sequence:

Start_Execute Master Workflow
        ↓
HTTP Request
        ↓
HTTP Request1
        ↓
HTTP Request2
        ↓
HTTP Request3
        ↓
HTTP Request4

with the following mapping:

HTTP Request  → WF1
HTTP Request1 → WF2
HTTP Request2 → WF3
HTTP Request3 → WF4
HTTP Request4 → WF5

The final execution successfully reached WF5, and all executed nodes showed green status during the final test.

PART 2 — MASTER WORKFLOW ARCHITECTURE
2.1 Architectural Principle

The Master Workflow was designed as an Orchestrator / Controller.

The Master does not perform:

data cleaning;
data validation;
analysis;
visualization;
replacement of WF1–WF5 logic.

The Master only controls the workflow execution sequence.

Architecture:

MASTER
  │
  ├── WF1 — Data Extraction
  │
  ├── WF2 — Data Cleaning
  │
  ├── WF3 — Data Quality Validation
  │
  ├── WF4 — Data Analysis Report
  │
  └── WF5 — Data Visualization
PART 3 — ACTUAL MASTER WORKFLOW NODES
3.1 First Node

Node name:

Start_Execute Master Workflow

This node is the starting point of the Master Workflow execution.

Its function is to initiate the sequence of calls to WF1 through WF5.

3.2 Second Node

Actual node name:

HTTP Request

This node is used to call:

WF1 — Data Extraction
3.3 Third Node

Actual node name:

HTTP Request1

This node is used to call:

WF2 — Data Cleaning
3.4 Fourth Node

Actual node name:

HTTP Request2

This node is used to call:

WF3 — Data Quality Validation
3.5 Fifth Node

Actual node name:

HTTP Request3

This node is used to call:

WF4 — Data Analysis Report
3.6 Sixth Node

Actual node name:

HTTP Request4

This node is used to call:

WF5 — Data Visualization
PART 4 — FINAL MASTER MAPPING

Actual Master Workflow mapping:

Sequence	Master Node	Workflow
1	Start_Execute Master Workflow	Start
2	HTTP Request	WF1
3	HTTP Request1	WF2
4	HTTP Request2	WF3
5	HTTP Request3	WF4
6	HTTP Request4	WF5

Therefore, the final flow is:

Start_Execute Master Workflow
            ↓
       HTTP Request
            ↓
           WF1
            ↓
       HTTP Request1
            ↓
           WF2
            ↓
       HTTP Request2
            ↓
           WF3
            ↓
       HTTP Request3
            ↓
           WF4
            ↓
       HTTP Request4
            ↓
           WF5
PART 5 — PRODUCTION WEBHOOK INTEGRATION

Each workflow is used through a Production Webhook.

Integration pattern:

MASTER
   ↓
HTTP Request
   ↓
Production Webhook
   ↓
Target Workflow

The Production Webhook is used after the workflow has been published.

Therefore, the Master does not execute the internal logic of WF1–WF5 directly, but calls the Production Webhook endpoint of each workflow.

PART 6 — WF1 DATA EXTRACTION

WF1 is the first workflow in the Master sequence.

WF1 status before Master integration:

COMPLETE / FROZEN

The Master calls WF1 through:

HTTP Request

Flow:

MASTER
 ↓
HTTP Request
 ↓
WF1 Production Webhook
 ↓
WF1 Data Extraction

WF1 was successfully executed through the Master.

Status: PASS

PART 7 — WF2 DATA CLEANING

WF2 is the second workflow.

WF2 status:

COMPLETE / FROZEN

The Master calls WF2 through:

HTTP Request1

Flow:

WF1
 ↓
HTTP Request1
 ↓
WF2 Production Webhook
 ↓
WF2 Data Cleaning

WF2 was successfully executed through the Master.

Status: PASS

PART 8 — WF3 DATA QUALITY VALIDATION
8.1 WF3 Integration

WF3 uses a Production Webhook to receive calls from the Master.

WF3 also uses a dedicated container:

wf3-validation-api

The validation service is accessed through:

http://wf3-validation-api:8000/validate
8.2 Initial WF3 Issue

During previous testing, the WF3 HTTP Request experienced:

ECONNREFUSED

The endpoint experiencing the issue was:

http://python-project-container:8002/validate

Error:

connect ECONNREFUSED 172.18.0.4:8002
8.3 Investigation

The investigation showed that WF3 has its own validation service:

wf3-validation-api

and that the service runs on the internal port:

8000
8.4 Correction

The WF3 endpoint was then adjusted to:

http://wf3-validation-api:8000/validate

After the service and network became available, the endpoint could be used by WF3.

8.5 Validation Result

The validation service test produced:

HTTP STATUS: 200
api_status: SUCCESS
validation_status: PASS
total_records: 5000
Missing values: 0
Duplicate rows: 0
Duplicate Transaction ID: 0
Numeric validation: PASS
Date validation: PASS
Transaction formula: PASS
Financial consistency: PASS
overall_status: PASS

Therefore:

WF3 = COMPLETE / PASS / FROZEN
PART 9 — WF4 DATA ANALYSIS REPORT
9.1 WF4 Architecture

WF4 has its own analysis engine in Docker:

wf4-analysis-engine

WF4 uses this service to execute the analysis process.

9.2 Initial Issue

During the initial Master test, execution stopped when reaching WF4.

The HTTP Request produced:

ENOTFOUND

with the message:

getaddrinfo ENOTFOUND wf4-analysis-engine
9.3 Payload Inspection

The payload sent to WF4 was inspected.

The transaction fields available included:

id_transaksi
tanggal_transaksi
id_produk
nama_produk
harga
jumlah
total_harga
id_pelanggan
nama_pelanggan
alamat
no_telepon
tanggal_keuangan
pemasukan
keterangan

Therefore, the request data format was not the root cause identified in that incident.

9.4 Root Cause

At the time of that test, the container:

wf4-analysis-engine

had not been activated.

As a result, the hostname:

wf4-analysis-engine

could not be resolved by the request.

9.5 Corrective Action

The container:

wf4-analysis-engine

was activated.

WF4 was then tested again.

9.6 Result

WF4 was successfully executed afterward.

WF4 = COMPLETE / PASS
PART 10 — WF5 DATA VISUALIZATION
10.1 WF5 Integration

WF5 is the final workflow called by the Master.

The Master calls WF5 through:

HTTP Request4

WF5 has its own Production Webhook.

Flow:

WF4
 ↓
HTTP Request4
 ↓
WF5 Production Webhook
 ↓
WF5 Data Visualization
10.2 Initial WF5 Issue

During the Master test, WF5 was successfully called, but the dashboard process failed.

The Dashboard Engine produced:

status = FAILED
return_code = 1
Rows = 0
Columns = 36

and the error:

KeyError: 'tanggal_transaksi'
10.3 Dataset Investigation

The Dashboard read:

/app/OUTPUT/DATA/Company_Data_Cleaned_n8n.csv

The file did not contain the expected transaction dataset.

The file contained validation result JSON.

As a result, the field:

tanggal_transaksi

was not available as a transaction column.

PART 11 — CANONICAL DATA VERIFICATION

The investigation identified the correct canonical file:

/app/OUTPUT/Company_Data_Cleaned_n8n.csv

The file was verified to contain:

5001 lines
14 columns

and to contain the column:

tanggal_transaksi

The correct transaction dataset is the dataset required by the Dashboard Engine.

11.1 Artifact Difference
Correct Dataset
/app/OUTPUT/Company_Data_Cleaned_n8n.csv

Status:

🟢 VALID

Characteristics:

5001 lines
14 columns
tanggal_transaksi available
Incorrect Artifact for Dashboard
/app/OUTPUT/DATA/Company_Data_Cleaned_n8n.csv

Status:

🔴 NOT SUITABLE FOR DASHBOARD INPUT

The content found was validation result JSON.

PART 12 — WF5 CORRECTION

The investigation was directed toward the file path and nodes related to the dataset output.

The nodes inspected included:

Read File from Disk 1

with the File Selector:

/data/project/OUTPUT/DATA/Company_Data_Cleaned_n8n.csv

This node is a Read operation and therefore was not considered a file writer based on the inspection performed.

The investigation was then directed toward identifying the process that produced the incorrect CSV artifact.

Correction objective:

WF5 Dashboard
      ↓
canonical transaction dataset
      ↓
5000 records
      ↓
14 columns
      ↓
tanggal_transaksi available

After correction and retesting, WF5 was able to complete its process.

PART 13 — WF5 OUTPUT

WF5 is responsible for visualization and report outputs.

The outputs that form part of the WF5 workflow include:

Dashboard PNG
Dashboard PDF
Email Report

WF5 also has an English report delivery path that had been verified previously.

For the multilingual enhancement, the French Final Report was prepared with the file:

WF_05_Data_Visualization_Email_Final_Report_20260817_FR.md

The French enhancement is part of WF5 delivery and does not change the WF5 analysis logic.

PART 14 — END-TO-END MASTER EXECUTION

After the issues in WF3, WF4, and WF5 were addressed, the Master Workflow was tested again.

Final flow:

Start_Execute Master Workflow
            ↓
        HTTP Request
            ↓
           WF1
            ↓
        HTTP Request1
            ↓
           WF2
            ↓
        HTTP Request2
            ↓
           WF3
            ↓
        HTTP Request3
            ↓
           WF4
            ↓
        HTTP Request4
            ↓
           WF5

During the final test, the entire sequence was able to run to completion.

The executed nodes showed green status.

MASTER END-TO-END EXECUTION = PASS
PART 15 — ORCHESTRATION EVIDENCE

Visual evidence was captured during the creation and testing process of the Master Workflow.

The evidence includes, among others:

Master Workflow Canvas.
Start_Execute Master Workflow node.
HTTP Request for WF1.
HTTP Request1 for WF2.
HTTP Request2 for WF3.
HTTP Request3 for WF4.
HTTP Request4 for WF5.
Production Webhook.
WF3 error.
WF3 endpoint correction.
WF4 error.
wf4-analysis-engine activation.
WF5 investigation.
Final end-to-end execution.

These evidence items form part of the audit trail for the creation of the Master Workflow.

PART 16 — TROUBLESHOOTING AUDIT TRAIL
Workflow	Issue	Root Cause	Action	Result
WF3	ECONNREFUSED	Endpoint/service routing was not appropriate	Using http://wf3-validation-api:8000/validate and ensuring the service was available	🟢 PASS
WF4	ENOTFOUND wf4-analysis-engine	wf4-analysis-engine was not active	Activating the container	🟢 PASS
WF5	KeyError: 'tanggal_transaksi'	Dashboard received an unsuitable CSV artifact	Tracing and correcting the dataset path	🟢 PASS
MASTER	Execution stopped at child workflow	Child workflow experienced a dependency/input issue	Child workflow was corrected and the Master was tested again	🟢 PASS
PART 17 — DATA INTEGRITY & CHANGE CONTROL

During the creation of the Master Workflow, the following principles were maintained:

WF1 = FROZEN
WF2 = FROZEN
WF3 = FROZEN

WF4 and WF5 logic remains within their respective workflows.

The Master is not used to perform:

repeated cleaning;
repeated validation;
repeated analysis;
repeated visualization;
changes to Master Data;
replacement of individual workflow logic.

The Master only functions as an orchestration layer.

PART 18 — FINAL STATUS MATRIX
Component	Final Status
WF1 — Data Extraction	🟢 COMPLETE / FROZEN
WF2 — Data Cleaning	🟢 COMPLETE / FROZEN
WF3 — Data Quality Validation	🟢 COMPLETE / PASS / FROZEN
WF4 — Data Analysis Report	🟢 COMPLETE / PASS
WF5 — Data Visualization	🟢 COMPLETE / PASS
WF MASTER	🟢 COMPLETE / PASS
End-to-End Orchestration	🟢 PASS
PART 19 — FINAL AUDIT SCOPE

The Master final audit covers:

19.1 Workflow Status

WF1–WF5 status was verified through the orchestration and execution process.

19.2 Canonical Data Status

The canonical dataset remains on the verified dataset path.

19.3 Reconciliation

Reconciliation remains the responsibility of the workflows performing validation and analysis.

The Master does not perform reconciliation recalculation.

19.4 Output

Outputs are generated by the workflows responsible for each respective process.

19.5 Business Evidence

Business evidence originates from the analysis and reporting workflows.

19.6 Dashboard

The Dashboard is the responsibility of WF5.

19.7 Orchestration Evidence

The Master provides evidence that the workflows were executed in the sequence:

WF1 → WF2 → WF3 → WF4 → WF5
19.8 Final Decision

Final result:

WF MASTER = COMPLETE / PASS
PART 20 — FINAL ARCHITECTURAL DECISION

The final implementation establishes:

MASTER
   ↓
WF1
   ↓
WF2
   ↓
WF3
   ↓
WF4
   ↓
WF5

as the Project_01_Data_Analyst orchestration chain.

The Master Workflow does not replace the individual workflows.

Each workflow remains independent and responsible for its respective process.

Therefore, the architecture fulfills the following principles:

modular;
separated by responsibility;
traceable;
testable;
maintainable;
auditable.
PART 21 — FINAL DECISION

Based on the implementation results, troubleshooting, corrective actions, retesting, and final end-to-end execution:

WF1 Execution              = PASS
WF2 Execution              = PASS
WF3 Execution              = PASS
WF4 Execution              = PASS
WF5 Execution              = PASS


Production Webhook         = PASS
Master Orchestration       = PASS
End-to-End Execution       = PASS


FINAL MASTER STATUS        = COMPLETE / PASS
AUDIT DECISION
WF_MASTER_Project_01_Data_Analyst

is declared:

COMPLETE / PASS

as the orchestration layer for executing the WF1 → WF5 sequence end-to-end.

The implementation went through the following process:

PLANNING
     ↓
CREATION
     ↓
INTEGRATION
     ↓
TESTING
     ↓
ERROR IDENTIFICATION
     ↓
ROOT CAUSE ANALYSIS
     ↓
CORRECTIVE ACTION
     ↓
RETEST
     ↓
END-TO-END VALIDATION
     ↓
FINAL PASS
PART 22 — EVIDENCE REGISTER

Master Workflow evidence to be retained:

EVIDENCE-MASTER-01
Master Workflow Canvas


EVIDENCE-MASTER-02
Start_Execute Master Workflow


EVIDENCE-MASTER-03
WF1 Production Execution


EVIDENCE-MASTER-04
WF2 Production Execution


EVIDENCE-MASTER-05
WF3 Production Execution


EVIDENCE-MASTER-06
WF3 ECONNREFUSED Investigation


EVIDENCE-MASTER-07
WF3 Corrected Validation Endpoint


EVIDENCE-MASTER-08
WF4 Production Execution


EVIDENCE-MASTER-09
WF4 ENOTFOUND Investigation


EVIDENCE-MASTER-10
wf4-analysis-engine Activation


EVIDENCE-MASTER-11
WF5 Production Execution


EVIDENCE-MASTER-12
WF5 Dashboard Investigation


EVIDENCE-MASTER-13
Canonical Dataset Verification


EVIDENCE-MASTER-14
Final Master End-to-End Execution


EVIDENCE-MASTER-15
Final All-Green Execution Evidence

The evidence numbers above function as the documentation register. Actual screenshot filenames may be mapped later without changing the audit content.

PART 23 — CLOSURE STATEMENT

The Master Workflow has completed the implementation and end-to-end validation stage.

The creation process did not only include node configuration, but also included troubleshooting of the dependency and integration issues identified in WF3, WF4, and WF5.

Each issue was handled using the following approach:

ERROR
 ↓
INVESTIGATION
 ↓
ROOT CAUSE
 ↓
CORRECTION
 ↓
RETEST
 ↓
PASS

The final result demonstrates that the Master can function as a single orchestration point for executing:

WF1 → WF2 → WF3 → WF4 → WF5

without combining the internal logic of the individual workflows into the Master.

FINAL RECORD
PROJECT
Project_01_Data_Analyst


MASTER WORKFLOW
WF_MASTER_Project_01_Data_Analyst


DOCUMENT
WF_Master_Final_Audit_Evidence_ID.md


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


WF5 INCORRECT ARTIFACT INVESTIGATED
/app/OUTPUT/DATA/Company_Data_Cleaned_n8n.csv


FINAL EXECUTION
SUCCESS


ORCHESTRATION STATUS
PASS


FINAL MASTER STATUS
COMPLETE / PASS
AUDIT CLOSING

This document serves as the final record of the actual Master Workflow implementation journey based on the processes that were performed, including integration, testing, troubleshooting, corrective action, and end-to-end validation.

Final Decision:

🟢 WF_MASTER_PROJECT_01_DATA_ANALYST
   COMPLETE / PASS

END OF DOCUMENT