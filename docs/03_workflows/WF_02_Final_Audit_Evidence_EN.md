WF2 — DATA CLEANING
FINAL STATUS & AUDIT SUMMARY

Project: Project_01_Data_Analyst
Workflow: WF2 — Data Cleaning
Status Date: 14 August 2026
Final Execution Status: 🟢 SUCCESS
Cleaning API Status: 🟢 OPERATIONAL
Output Verification Status: 🟢 PASS
Audit Status: 🟢 VERIFIED

1. EXECUTIVE SUMMARY

WF2 — Data Cleaning was successfully executed through n8n using a FastAPI-based cleaning service.

WF2 is designed to receive the dataset produced by WF1, execute the defined cleaning process, and produce the canonical cleaned dataset for use by subsequent workflows.

During the execution verified on 14 August 2026, all WF2 nodes executed successfully with status SUCCESS.

The WF2 HTTP Request node successfully called:

POST /clean

and received:

HTTP 200 OK

The cleaning service recorded:

5,000 records

and:

REVENUE MASUK = Rp110,380,250,000

The generated canonical output is:

Company_Data_Cleaned_n8n.csv

The output was subsequently verified directly from python-project-container.

Verification results:

Total records: 5,000
Total columns: 14
Missing values in output: 0
Duplicate rows in output: 0
Total revenue based on total_harga: Rp110,380,250,000
The output file is available at the designated location.

Based on all evidence reviewed, WF2 is declared:

🟢 SUCCESS / VERIFIED

2. WORKFLOW STATUS
Workflow	Function	Final Status
WF1	Data Extraction	✅ COMPLETE / FROZEN
WF2	Data Cleaning	🟢 SUCCESS / VERIFIED
WF3	Data Quality Validation	🟢 COMPLETE / PASS / FROZEN
WF4	Data Analysis Report	🟢 COMPLETE / PASS
WF5	Data Visualization	⏳ NOT STARTED
Current Project Milestone

WF1 → COMPLETE / FROZEN
WF2 → SUCCESS / VERIFIED
WF3 → COMPLETE / PASS / FROZEN
WF4 → COMPLETE / PASS
WF5 → NOT STARTED

3. WF2 OBJECTIVE

WF2 is intended to provide a consistent and controlled Data Cleaning process before the dataset is used by the validation and analysis workflows.

The WF2 process includes:

receiving the CSV file through the API;
reading the dataset;
checking the number of records and columns;
identifying missing values;
identifying duplicate rows;
removing duplicate rows;
handling missing values in designated fields;
resetting the index;
saving the canonical cleaned dataset;
returning the cleaned CSV to n8n.

WF2 is exclusively responsible for the Data Cleaning process.

The Data Quality Validation process is performed by WF3, while the Data Analysis Report process is performed by WF4.

4. WF2 INPUT

WF2 receives the file through an HTTP Request using Form-Data.

The body configuration used is:

Body Content Type: Form-Data

Body:

file

Type:

n8n Binary File

Name:

file

Input Data Field Name:

DATA

This configuration was successfully used during the verified WF2 execution.

The Docker logs show:

ROWS MASUK: 5000

and:

REVENUE MASUK: 110380250000.0

The API then returned:

POST /clean HTTP/1.1" 200 OK

5. CLEANING SERVICE

The WF2 cleaning service is executed through:

Container:

python-project-container

Container Port:

8000

Host Port:

8001

API Endpoint:

POST /clean

The cleaning process implementation is located at:

/app/SCRIPT/main.py

The service uses:

FastAPI
Uvicorn
Pandas

The cleaning service operates separately from n8n as an API service.

6. WF2 ARCHITECTURE

WF2 architecture:

n8n
 │
 └── HTTP Request
       │
       │ POST /clean
       ▼
python-project-container
       │
       ├── FastAPI
       │
       ├── /clean
       │
       ├── Read CSV
       │
       ├── Duplicate Handling
       │
       ├── Missing Value Handling
       │
       ├── Save Cleaned CSV
       │
       └── Return CSV

Host mapping:

localhost:8001
       ↓
python-project-container:8000
7. WF2 INTEGRATION WITH n8n

The WF2 HTTP Request node uses the following configuration:

Method:

POST

URL:

http://host.docker.internal:8001/clean

Authentication:

None

Send Query Parameters:

OFF

Send Headers:

OFF

Send Body:

ON

Body Content Type:

Form-Data

Body:

file
├── Type → n8n Binary File
├── Name → file
└── Input Data Field Name → DATA

The actual execution confirms that all WF2 nodes executed successfully.

Status: 🟢 SUCCESS

8. DATA CLEANING PROCESS

Based on the examination of /app/SCRIPT/main.py, WF2 performs the following steps.

8.1 Temporary Input File Storage

The file received by the API is temporarily stored at:

/tmp/{file.filename}

8.2 CSV Reading

The dataset is read using Pandas with:

sep="\t"

8.3 Initial Data Validation

The process calculates:

total records;
number of columns;
missing values;
duplicate rows.
8.4 Duplicate Handling

The cleaning process uses:

df.drop_duplicates()

to remove duplicate rows.

8.5 Missing Value Handling

For the column:

alamat

missing values are replaced with:

Tidak Diketahui

For the column:

no_telepon

missing values are replaced with:

Tidak Diketahui

This approach handles missing values in these two fields without deleting the affected transactions.

8.6 Index Reset

After cleaning, the index is reset using:

reset_index(drop=True)

8.7 Output Creation

The cleaned dataset is saved to:

/app/OUTPUT/Company_Data_Cleaned_n8n.csv

The file is then returned to n8n using FileResponse.

9. WF2 EXECUTION RESULTS

Verified WF2 execution results:

Parameter	Result
Records received by API	5,000
Records in output	5,000
Columns in output	14
Missing values in output	0
Duplicate rows in output	0
Revenue total_harga	Rp110,380,250,000
HTTP Response	200 OK
10. OUTPUT DATA STRUCTURE

The canonical output contains the following 14 columns:

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

This structure has been verified directly from the canonical output.

11. OUTPUT FILE VERIFICATION

Canonical output:

Company_Data_Cleaned_n8n.csv

Host location:

D:\Project_01_Data_Analyst\OUTPUT

The latest output file generated by the verified WF2 execution has:

Date: 14/08/2026
Time: 20:17
Size: 923.746 bytes

The file was subsequently read directly using Python inside:

python-project-container

Verification results:

ROWS: 5000
COLUMNS: 14
REVENUE: 110380250000.0
MISSING_TOTAL: 0
DUPLICATE_ROWS: 0
12. HTTP RESPONSE VERIFICATION

The WF2 HTTP Request received 1 item containing the CSV result.

The response contains the field:

data

which contains the cleaned CSV data.

This is consistent with the API implementation because the /clean endpoint uses:

FileResponse

with:

media_type="text/csv"

and:

filename="Company_Data_Cleaned_n8n.csv"

Therefore, the CSV response is the expected behavior of the API and is not an error.

13. DATA RECONCILIATION

Based on the available evidence:

Records received by API:

5,000

Records in canonical output:

5,000

Difference:

0

Result

RECORD COUNT RECONCILIATION = MATCH

Revenue Reconciliation

Revenue recorded by the API:

Rp110,380,250,000

Revenue in the canonical output based on total_harga:

Rp110,380,250,000

Difference:

Rp0

Result

REVENUE VALUE RECONCILIATION = MATCH

This reconciliation compares only the values actually obtained from the API logs and the verified canonical output.

14. OUTPUT CHECK RESULTS

Direct verification of the canonical output produced:

Missing values = 0

Duplicate rows = 0

These results show that the current canonical output contains no missing values or duplicate rows based on the checks performed.

However, these results are not used to claim how many missing values or duplicate rows existed in the input before cleaning, because those input-level quantities are not available as separate evidence in the execution currently being verified.

This approach is used to maintain audit accuracy and prevent unsupported conclusions.

15. WF2 EVIDENCE

The evidence used for WF2 verification consists of:

A. Docker Execution Evidence

Log:

docker logs --tail 100 python-project-container

Evidence:

the API is running successfully;
/clean received the request;
ROWS MASUK: 5000;
REVENUE MASUK: 110380250000.0;
POST /clean returned 200 OK.
B. Output File Evidence

File:

Company_Data_Cleaned_n8n.csv

Evidence:

file is available;
latest timestamp verified;
5,000 records;
14 columns;
missing values = 0;
duplicate rows = 0;
revenue = Rp110,380,250,000.
C. API Implementation Evidence

File:

/app/SCRIPT/main.py

Evidence:

/clean endpoint;
file reception through UploadFile;
duplicate handling;
missing value handling;
output path;
FileResponse.
D. n8n Execution Evidence

Evidence:

HTTP Request succeeded;
Form-Data was successfully sent;
binary file was transmitted through the file field;
Input Data Field Name = DATA;
CSV response was successfully received.
16. TECHNICAL OBSERVATION

During examination of /app/SCRIPT/main.py, two identical FileResponse blocks were identified.

The second block is located after the first return statement and therefore cannot be executed.

This observation:

Does not affect the verified WF2 execution, because:

the first FileResponse block executes successfully;
the API returns HTTP 200 OK;
the output file is successfully created;
n8n successfully receives the CSV.

This observation is classified as:

Technical Code Observation — Non-blocking

No changes were made to WF2 during this verification.

17. IMPORTANT AUDIT NOTE

This report uses the latest evidence actually verified on 14 August 2026.

The current result is:

5,000 records input → 5,000 records output

Therefore, values from older executions or historical workflow versions are not used as the current WF2 result when they are not supported by the latest execution evidence.

In particular, this report does not state that WF2 currently reduces the dataset from 5,000 to 4,745 records.

The currently verified canonical output contains:

5,000 records

This approach prevents historical execution results from being mixed with the current canonical workflow state.

18. FROZEN COMPONENTS

The following WF2 components are maintained as frozen components following successful execution and verification:

Workflow

WF2 — Data Cleaning

Cleaning API

POST /clean

Container

python-project-container

Cleaning Script

/app/SCRIPT/main.py

Canonical Output

Company_Data_Cleaned_n8n.csv

Changes to these components should only be made if there is:

a verified defect;
a reproducible failure; or
a documented controlled enhancement.
19. FINAL AUDIT RESULT
Component	Result
n8n Workflow Execution	🟢 PASS
HTTP Request Integration	🟢 PASS
Form-Data Upload	🟢 PASS
Binary File Transfer	🟢 PASS
/clean API	🟢 PASS
HTTP Response	🟢 200 OK
Input Record Reception	🟢 5,000
Output Record Count	🟢 5,000
Output Column Count	🟢 14
Output Missing Values	🟢 0
Output Duplicate Rows	🟢 0
Revenue Verification	🟢 MATCH
Canonical Output File	🟢 VERIFIED
Cleaning Process	🟢 VERIFIED
Audit Conclusion

WF2 FINAL AUDIT = PASS / VERIFIED

20. FINAL WF2 DECISION

Based on the successful n8n execution, successful /clean API execution, Docker execution logs, canonical output verification, data structure verification, missing value checks, duplicate row checks, revenue reconciliation, and API implementation review:

🟢 WF2 — DATA CLEANING

FINAL STATUS: SUCCESS / VERIFIED

WF2 successfully:

received the file through n8n;
sent the file using Form-Data;
used n8n Binary File;
called the POST /clean endpoint;
received HTTP 200 OK;
processed 5,000 records;
produced the canonical output;
produced 5,000 records in the output;
retained 14 columns;
produced 0 missing values in the output;
produced 0 duplicate rows;
produced total_harga revenue of Rp110,380,250,000;
returned the CSV result to n8n.
21. AUDIT TRAIL NOTE

This document records the final state of WF2 following successful execution and verification on 14 August 2026.

Verification was performed using multiple sources of evidence:

n8n workflow execution;
Docker container status;
Docker application logs;
canonical output file verification;
direct dataset verification from python-project-container;
HTTP response verification;
/clean source code verification.

The verification results show that WF2 received 5,000 records through the cleaning service, executed the cleaning process, produced the canonical cleaned dataset, and successfully returned the cleaned CSV to n8n.

The verified canonical output contains:

5,000 records
14 columns
0 missing values
0 duplicate rows

Revenue based on total_harga:

Rp110,380,250,000

The reconciliation between the revenue recorded in the API logs and the canonical output is:

Rp110,380,250,000 = Rp110,380,250,000

with:

Difference = Rp0

This report clearly distinguishes the latest execution evidence from historical results.

No claim is made regarding the number of records removed during a previous execution when such a claim cannot be supported by verifiable evidence.

No changes were made to the WF2 workflow or cleaning service during the verification process.

FINAL WF2 STATUS

🟢 SUCCESS / VERIFIED

Audit Status: 🟢 PASS