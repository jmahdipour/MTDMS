# Report Search & Retrieval Engine

Document ID : MTDMS-RE-013

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

The Report Search & Retrieval Engine provides rapid access to previously generated reports, certificates, and archived engineering documents.

The engine allows engineers, laboratory personnel, and quality managers to locate reports using engineering, customer, material, machine, or project information.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Search & Retrieval Engine shall

• Search archived reports

• Retrieve historical reports

• Support advanced filtering

• Preserve engineering traceability

• Improve laboratory productivity

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Engineering Report

↓

Archive

↓

Search

↓

Retrieve

Archived engineering documents remain unchanged.

---

# Workflow

```
Search Criteria

↓

SQLite Query

↓

Matching Reports

↓

Select Report

↓

Open
```

---

# Search Fields

Report Number

Certificate Number

Customer Name

Project

Material

Material Grade

Heat Number

Batch Number

Sample ID

Machine

Operator

Standard

Test Type

Revision

Issue Date

Archive ID

Administrator configurable.

---

# Date Search

Supported

Exact Date

Date Range

Month

Year

Quarter

Administrator configurable.

---

# Engineering Filters

The engine may filter reports by

Yield Strength

Ultimate Strength

Young's Modulus

Elongation

Maximum Force

Spring Constant

Ring Stiffness

Compression Strength

using validated engineering results stored in SQLite.

---

# Customer Filters

Customer

Customer Code

Project

Purchase Order

Order Number

Administrator configurable.

---

# Machine Filters

Machine

Load Cell

Extensometer

Software Version

Calibration Status

Administrator configurable.

---

# Result List

Displayed columns may include

Report Number

Certificate Number

Customer

Material

Test Type

Operator

Date

Revision

Status

Archive Location

---

# Sorting

Supported

Date

Report Number

Customer

Material

Machine

Operator

Revision

Ascending

Descending

---

# Retrieval

The selected report may be opened

Read Only

Editable (administrator only)

Exported

Printed

Administrator configurable.

---

# Batch Retrieval

Supported

Multiple Reports

Multiple Certificates

Customer Package

Project Package

Administrator configurable.

---

# Engineering Independence

The Search & Retrieval Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Archived Reports

Only retrieval operations are performed.

---

# SQLite Interaction

SQLite provides

Report Index

Certificate Index

Engineering Metadata

Archive Metadata

Search History (optional)

---

# Error Handling

No Results

↓

Display Empty List

Archive Missing

↓

Warning

File Missing

↓

Warning

SQLite Failure

↓

Abort

---

# Performance Targets

Typical Search

< 100 ms

Complex Search

< 500 ms

Open Report

< 500 ms

---

# Acceptance Criteria

✔ Advanced report search

✔ Engineering result filtering

✔ Customer filtering

✔ Machine filtering

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
