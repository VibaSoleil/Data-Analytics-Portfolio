DOCKER PROJECT ARCHITECTURE — FINAL
1. Document Information

Project: Project_01_Data_Analyst
Project Scope: ODC Bag 8 — Data Analytics Automation
Document Type: Technical Architecture Documentation
Status: FINAL
Primary Language: English

2. Objective

This document documents the Docker architecture used to support the Data Analytics Automation project.

The architecture is designed to separate the main components according to their functions:

workflow orchestration,
database,
Python data processing and API service,
as well as analysis output results.

The separation of components through Docker helps maintain a modular, isolated, easily testable, and easier-to-maintain working environment.

3. Docker Network

The project uses the Docker network:

n8n-network

Verified network configuration:

Driver      : bridge
IPv4        : enabled
IPv6        : disabled
Subnet      : 172.18.0.0/16
Gateway     : 172.18.0.1

The network functions as an internal communication channel between containers that are part of the project runtime.

4. Active Runtime Containers

Based on the Docker inspection performed in the project environment, the following three containers are connected to n8n-network and are currently active.

4.1 n8n

Container: n8n

Image:

docker.n8n.io/n8nio/n8n:latest

Port:

5678 → 5678

Status: Running

Role:

Workflow orchestration
Running workflow automation
Managing process sequence
Connecting different pipeline stages
Managing requests to required services
Handling automation processes and workflow outputs
4.2 MySQL Server

Container: mysql-server

Image:

mysql:8.4

Port:

3306 → 3306

Status: Running

Role:

Providing the MySQL database
Storing the project's data sources
Providing data for extraction and analysis processes

Main database used:

perusahaan_db

Main tables:

produk
pelanggan
transaksi
keuangan
4.3 Python Project Container

Container: python-project-container

Image:

python:3.12-slim

Port:

8001 → 8000

Status: Running

Main components used in the Python environment:

Python 3.12
pandas
numpy
FastAPI
Uvicorn

Role:

Data processing
Data cleaning
Python-based analysis
Providing API endpoints for communication with the workflow
Processing datasets and providing results for the next stage
5. Current Docker Architecture

The active runtime architecture can be represented as follows:

                    n8n-network
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
        n8n        mysql-server    python-project-container
          │              │              │
          │              │              │
          │         perusahaan_db        │
          │              │              │
          │              ▼              │
          │      ┌───────┼────────┐      │
          │      │       │        │      │
          │   produk pelanggan transaksi keuangan
          │                       │
          └───────────┬───────────┘
                      │
                      ▼
              Data Processing
                & Analysis
                      │
                      ▼
                Output / Report
6. Data Processing Flow

The conceptual data processing flow is as follows:

Raw / Source Data
       │
       ▼
MySQL / Data Source
       │
       ▼
n8n Workflow
       │
       ▼
Python Processing / API
       │
       ├── Data Cleaning
       ├── Data Validation
       ├── Data Analysis
       └── Data Processing
       │
       ▼
Clean / Validated Dataset
       │
       ▼
Analysis Output
       │
       ▼
Visualization / Dashboard / Report

The final project implementation is then organized into the following workflows:

WF1 → Data Extraction
WF2 → Data Cleaning
WF3 → Data Quality Validation
WF4 → Data Analysis
WF5 → Data Visualization
WF_MASTER → Workflow Orchestration
7. Database Integration

The main database of the project is:

perusahaan_db

Main structure:

produk
    │
    └── id_produk
           │
           ▼
       transaksi
           │
           ├── id_produk
           ├── id_pelanggan
           └── id_transaksi
                    │
                    ▼
                keuangan

Customer relationship:

pelanggan
    │
    └── id_pelanggan
             │
             ▼
         transaksi

The complete database structure is documented separately in:

Database_Schema_Perusahaan_DB.md
8. Workflow Integration

Docker is used as the infrastructure layer, while the project workflows are managed through n8n.

Conceptually:

Docker
  │
  ├── n8n
  │      └── Workflow Orchestration
  │
  ├── MySQL
  │      └── Data Source
  │
  └── Python
         └── Data Processing / API

This approach gives each component a clearly defined responsibility.

n8n

Responsible for:

orchestration,
workflow execution,
service communication,
file handling,
automation logic.
MySQL

Responsible for:

data storage,
relational data source,
structured data retrieval.
Python

Responsible for:

data processing,
cleaning,
analytical computation,
API-based processing.
9. Workflow-Specific Services

During project development and validation, additional services/containers were used for specific workflow requirements, including:

wf3-validation-api
wf4-analysis-engine

At the time this document was created, these two containers were not active and were not listed as containers connected to n8n-network.

Therefore, they are not categorized as Active Runtime Containers in this documentation.

This information is retained as part of the historical/workflow-specific technical context and is not considered to represent services that are always active.

10. Historical / Obsolete Containers

The environment inspection also identified several old containers or test containers that are not part of the active runtime:

python-container
peaceful_yalow
flamboyant_mahavira

These containers are not used as active components in the final runtime architecture documented here.

11. Architecture Design Principles

The project architecture applies several principles:

11.1 Separation of Responsibility

Each service has a distinct responsibility:

n8n       → Orchestration
MySQL     → Data Storage
Python    → Processing & Analysis
11.2 Modularity

The workflows are separated into several stages so that each process can be tested and validated independently.

11.3 Reproducibility

Processes are executed in an isolated environment through Docker, allowing dependencies and runtime to be controlled more consistently.

11.4 Traceability

Each stage produces an output that can be used as evidence for validation and reconciliation.

11.5 Quality Assurance

Automation output is not accepted solely based on successful execution.

The results are also compared with:

Manual Python
      ↓
Master Dataset
      ↓
n8n Pipeline
      ↓
Reconciliation
      ↓
Final Audit

This approach helps ensure that the automation produces output consistent with previously validated references.

12. Security and Credential Handling

Database credentials, passwords, API keys, tokens, and other confidential information are not documented in this architecture file.

Credential information is only used within the appropriate configuration environment.

The architecture documentation only describes the relationships and functions between components without exposing secrets.

13. Current Architecture Status
Component	Status
Docker Network	✅ VERIFIED
n8n	✅ RUNNING
MySQL Server	✅ RUNNING
Python Project Container	✅ RUNNING
Database perusahaan_db	✅ DEFINED
Workflow Architecture	✅ IMPLEMENTED
WF1–WF5	✅ COMPLETED
WF_MASTER	✅ COMPLETED
Reconciliation	✅ COMPLETED
Final Audit	✅ COMPLETED
14. Final Assessment

The project's Docker architecture provides a separate infrastructure layer for workflow orchestration, database management, and Python-based data processing.

With the combination of:

Docker
+
n8n
+
MySQL
+
Python / FastAPI
+
Data Validation
+
Reconciliation
+
Final Audit

the project does not focus solely on automation, but also on reproducibility, traceability, validation, and quality assurance.

This architecture supports the complete project lifecycle:

Data Source
    ↓
Extraction
    ↓
Cleaning
    ↓
Validation
    ↓
Analysis
    ↓
Visualization
    ↓
Reconciliation
    ↓
Audit
    ↓
Final Output

Final Status: VERIFIED / DOCUMENTED

