# Project Folder Structure v2

## Project Overview

This project is structured as a professional data analytics and automation environment integrating:

* MySQL database
* Python data processing and analysis
* n8n workflow automation
* Master data generation
* Data validation
* Audit and reconciliation
* Visualization and dashboarding
* Business reporting

The folder architecture separates **source data, processing logic, validated outputs, master data, audit evidence, reconciliation, and business deliverables** to maintain traceability, consistency, and controlled project execution.

---

# Root Directory

```text
D:\
│
├── Download
│   └── Temporary download and external source files
│
├── AI_Project_Documentation
│   │
│   ├── Core Documentation
│   │   ├── Business Analysis & Case Study Requirements
│   │   ├── Database Schema Documentation
│   │   ├── Docker Project Architecture
│   │   ├── n8n Automation Architecture & Workflow Design
│   │   ├── n8n MySQL Connection Documentation
│   │   ├── Project Folder Structure
│   │   └── Technical Troubleshooting Documentation
│   │
│   ├── AUDIT
│   │   └── Manual Python Audit Documentation
│   │
│   ├── KETERANGAN
│   │   ├── AUDIT FINDING
│   │   ├── Financial Source Alignment
│   │   ├── Root Cause / Revenue Inconsistency Findings
│   │   └── Supporting Audit Notes
│   │
│   ├── RECONCILIATION
│   │   ├── 01_PYTHON_MANUAL_VS_MASTER_RECONCILIATION
│   │   ├── 02_PYTHON_MANUAL_VS_N8N_RECONCILIATION
│   │   └── 03_MASTER_VS_N8N_RECONCILIATION
│   │
│   └── WORKFLOW_N8N
│       ├── WF_01_Final_Audit_Evidence
│       ├── WF_02_Final_Audit_Evidence
│       ├── WF_03_Final_Audit_Evidence
│       ├── WF_04_Final_Audit_Evidence
│       ├── WF_05_Final_Audit_Evidence
│       ├── WF_05_Final_Business_Email_Report
│       └── WF_Master_Final_Audit_Evidence
│
└── Project_01_Data_Analyst
    │
    ├── ARCHIVE
    │   ├── LEGACY_OUTPUT
    │   ├── OLD_PROBLEMATIC_FILES
    │   ├── OLD_REPORT
    │   └── OLD_SCRIPT
    │
    ├── DATA_RAW
    │   └── Original source data before processing
    │
    ├── DATABASE
    │   └── MySQL database definition / SQL source
    │
    ├── SCRIPT
    │   ├── Data Cleaning
    │   ├── Data Quality Validation
    │   ├── Data Analysis
    │   ├── Master Data Generation
    │   ├── Final Business Analysis
    │   ├── Final Dashboard
    │   ├── AUDIT
    │   ├── FINALAUDIT_MASTER
    │   └── FINALAUDIT_N8N
    │
    ├── OUTPUT
    │   │
    │   ├── DATA
    │   │   └── Processed and analytical datasets
    │   │
    │   ├── VALIDATION
    │   │   └── Data quality and validation evidence
    │   │
    │   ├── MASTER
    │   │   ├── CUSTOMER_MASTER
    │   │   ├── FINANCIAL_MASTER
    │   │   ├── PRODUCT_MASTER
    │   │   ├── SALES_MASTER
    │   │   └── TRANSACTION_MASTER
    │   │
    │   ├── AUDIT
    │   │   ├── FinalAudit_Manual_Python
    │   │   ├── FinalAudit_Master
    │   │   ├── FinalAudit_n8n
    │   │   └── RECONCILIATION
    │   │
    │   ├── REPORT
    │   │   └── Analytical and final business reports
    │   │
    │   ├── VISUALIZATION
    │   │   └── Analytical charts and supporting visualizations
    │   │
    │   └── DASHBOARD
    │       └── Final business dashboard outputs
    │
    ├── docker
    │   └── Docker-related project configuration
    │
    └── README.md
        └── Project overview and operational guidance
```

---

# Architectural Principles

## 1. Separation of Concerns

Each project layer has a defined responsibility:

```text
DATA_RAW
    ↓
DATABASE
    ↓
SCRIPT / AUTOMATION
    ↓
VALIDATION
    ↓
MASTER DATA
    ↓
ANALYSIS
    ↓
VISUALIZATION
    ↓
DASHBOARD
    ↓
BUSINESS REPORT
```

This separation prevents raw data, processing logic, validation evidence, and final deliverables from being mixed together.

---

## 2. Dual Processing and Automation

The project supports both:

* Manual Python processing and analysis
* Automated n8n processing and orchestration

This architecture allows analytical results to be independently compared and validated.

---

## 3. Master Data Layer

The `MASTER` layer provides controlled reference datasets for:

* Customer
* Financial
* Product
* Sales
* Transaction

Master outputs serve as a stable analytical reference for downstream analysis, audit, and reconciliation.

---

## 4. Validation and Auditability

The project maintains dedicated layers for:

* Data quality validation
* Manual Python audit
* Master audit
* n8n audit
* Final audit evidence
* Audit findings

This provides traceability from processed data to final analytical conclusions.

---

## 5. Reconciliation Framework

Three independent reconciliation paths are maintained:

```text
Python Manual
      ↕
    MASTER

Python Manual
      ↕
      n8n

MASTER
      ↕
      n8n
```

The purpose is to identify discrepancies, verify consistency, and establish confidence in the final analytical results.

---

## 6. Archive and Controlled History

The `ARCHIVE` directory isolates legacy, obsolete, problematic, and historical project files from the active project structure.

Archived files are retained for traceability without being treated as current production outputs.

---

# Documentation Language Structure

Core project documentation may be maintained in:

* Indonesian — `ID`
* English — `EN`
* French — `FR`

The multilingual documentation supports international portfolio presentation while preserving a consistent technical structure.

---

# Final Project Flow

```text
SOURCE DATA
     ↓
DATABASE
     ↓
PYTHON / n8n PROCESSING
     ↓
DATA VALIDATION
     ↓
MASTER DATA
     ↓
ANALYSIS
     ↓
RECONCILIATION
     ↓
AUDIT
     ↓
VISUALIZATION
     ↓
DASHBOARD
     ↓
BUSINESS REPORT
```

---

# Governance Statement

This folder structure is designed to maintain **clarity, traceability, reproducibility, auditability, and separation between active outputs and historical files**.

Only relevant production scripts and final analytical artifacts are represented in the active project structure. Temporary, duplicated, backup, obsolete, and problematic files are excluded from the primary architecture and retained separately when necessary.

The structure therefore represents the **controlled and professional state of the project**, rather than a complete historical inventory of every file created during development.
