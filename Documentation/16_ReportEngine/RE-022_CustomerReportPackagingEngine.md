# Customer Report Packaging Engine

Document ID : MTDMS-RE-022

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Customer Report Packaging Engine prepares complete delivery packages for customers by collecting all approved documents, engineering graphs, and optional supporting files into a single organized package.

The package contains copies of validated engineering information only.

The engine performs **no engineering calculations**.

---

# Objectives

The Customer Report Packaging Engine shall

• Create customer delivery packages

• Organize multiple documents

• Preserve engineering traceability

• Support configurable package contents

• Standardize customer deliveries

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Approved Documents

↓

Packaging

↓

Customer Package

The package is a distribution container only.

---

# Workflow

```
Approved Documents

↓

Select Customer Profile

↓

Collect Files

↓

Create Package

↓

Verify

↓

Ready for Distribution
```

---

# Supported Package Contents

Engineering Report (PDF)

Engineering Report (Excel)

Laboratory Certificate

Engineering Graphs

CSV Export

Original TXT File (optional)

Cover Letter (optional)

Inspection Checklist (optional)

Administrator configurable.

---

# Package Structure

Example

```
Customer Package

│

├── Report

│   └── TR-2026-00125.pdf

│

├── Certificate

│   └── TC-2026-00125.pdf

│

├── Graphs

│   ├── StressStrain.png

│   └── ForceDisplacement.png

│

├── Data

│   ├── Results.csv

│   └── Original.txt

│

└── Readme.txt
```

Administrator configurable.

---

# Package Naming

Recommended

```
Customer_Project_ReportNumber
```

Example

```
ABCSteel_Project15_TR-2026-00125
```

Administrator configurable.

---

# Compression

Optional

ZIP Package

Uncompressed Folder

Administrator configurable.

---

# Customer Profiles

Each customer may specify

Preferred Language

Preferred File Formats

Preferred Folder Structure

Include TXT

Include CSV

Include Graphs

Administrator configurable.

---

# Verification

Before packaging

The engine verifies

Report Exists

Certificate Exists

Graphs Exist

Engineering Results Approved

No Missing Mandatory Files

---

# Package Metadata

Stored information

Package ID

Customer

Project

Report Number

Operator

Creation Date

Revision

Package Contents

---

# Engineering Independence

The Packaging Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Reports

Certificates

It creates distribution copies only.

---

# SQLite Interaction

SQLite stores

Package History

Package Configuration

Customer Preferences

Package Contents

Audit History

---

# Error Handling

Missing Report

↓

Abort

Missing Certificate

↓

Warning

Missing Graph

↓

Continue (configurable)

Package Creation Failure

↓

Retry

---

# Performance Targets

Typical Package

< 2 s

ZIP Creation

< 5 s

Verification

< 200 ms

---

# Acceptance Criteria

✔ Customer package generation

✔ Configurable package contents

✔ ZIP support

✔ Verification before packaging

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
