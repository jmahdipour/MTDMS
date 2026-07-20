# TXT Import Workflow

Document ID : MTDMS-IMP-002

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

Input

TXT Only

---

# Purpose

This document defines the complete TXT import process.

The workflow guarantees that every imported test file is

• Verified

• Traceable

• Recoverable

• Compatible with ISO 17025

---

# Import Workflow

```
Browse

↓

Select TXT

↓

Open File

↓

Read Header

↓

Read Data

↓

Detect Units

↓

Validate

↓

Preview

↓

Import

↓

Engineering

↓

SQLite

↓

Ready
```

---

# Step 1

Browse

Ribbon

IMPORT

↓

Browse TXT

File Dialog

↓

Select TXT

Allowed Extension

```
*.txt
```

---

# Step 2

Read File

System reads

Header

↓

Data

↓

Footer (if exists)

No worksheet modification yet.

---

# Step 3

Header Validation

Checks

Machine

Date

Operator

Material

Specimen

Area

Gauge Length

Units

Standard

Missing fields

↓

Warning

Critical missing fields

↓

Import blocked

---

# Step 4

Column Detection

Columns detected automatically.

Expected

Time

Force

Stroke

Optional

Extension

Stress

Strain

Temperature

Cycle

---

# Step 5

Unit Detection

Recognized

Force

kgf

N

kN

Length

mm

Stress

MPa

Strain

mm/mm

Automatic conversion if necessary.

---

# Step 6

Data Validation

Checks

Blank rows

Duplicate rows

Non-numeric values

Negative time

Missing force

Missing stroke

NaN

Overflow

---

# Step 7

Preview

Display

First 100 rows

Statistics

Rows

Columns

Units

File Size

Warnings

Operator confirms import.

---

# Step 8

Import

Destination

```
tblRawData
```

Data stored exactly as received.

No engineering calculation.

---

# Step 9

Engineering Initialization

Raw Data

↓

Engineering Controller

↓

Stress

↓

Strain

↓

Elastic Region

↓

Ready

---

# Step 10

Database

SQLite stores

Project Metadata

Import Date

TXT Name

Operator

Machine

Checksum

---

# Error Handling

Invalid TXT

↓

Abort

↓

Write ERROR_LOG

↓

Display reason

---

# Recovery

Operator may

Reload

Select another TXT

Correct settings

Repeat validation

---

# Progress Indicator

Status Bar

Examples

Reading Header...

Reading Data...

Validating...

Importing...

Completed

---

# Performance Targets

Open TXT

< 1 sec

Read Header

< 100 ms

Read 100000 Rows

< 5 sec

Validation

< 2 sec

Import

< 1 sec

---

# Logging

Every import writes

Import Timestamp

Project ID

TXT Name

File Size

Row Count

Operator

Result

---

# Import Restrictions

Only one TXT per project.

Re-import requires confirmation.

Original TXT is never modified.

Imported data is immutable.

---

# Future Support

Automatic machine recognition

Automatic material suggestion

Automatic standard suggestion

Multiple TXT merge

Batch Import

---

End of Document
