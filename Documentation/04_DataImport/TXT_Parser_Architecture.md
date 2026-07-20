# TXT Parser Architecture

Document ID : MTDMS-IMP-011

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document describes the architecture of the TXT Parser.

The parser is responsible only for importing machine-generated TXT files.

It never performs engineering calculations.

It never creates reports.

It only converts TXT into the internal data model.

---

# Design Philosophy

TXT

↓

Parser

↓

Universal Data Model

↓

Engineering Engine

↓

Graph Engine

↓

Report Engine

---

# Responsibilities

The Parser SHALL

✔ Open TXT

✔ Detect Encoding

✔ Read Header

✔ Read Data

✔ Detect Units

✔ Validate

✔ Normalize

✔ Store Raw Data

✔ Return Result

---

The Parser SHALL NOT

✘ Calculate Stress

✘ Calculate Strain

✘ Calculate Young's Modulus

✘ Detect Yield

✘ Draw Charts

✘ Generate Reports

✘ Access Worksheets directly

---

# Architecture

```
TXTParser

│

├── FileReader

├── HeaderParser

├── ColumnDetector

├── UnitDetector

├── Validator

├── DataNormalizer

├── RawDataStore

└── ParserLogger
```

---

# FileReader

Responsibilities

Open TXT

Read Encoding

Load File

Split Lines

Return Array

---

# HeaderParser

Responsibilities

Locate Header

Extract Metadata

Verify Required Fields

Return Header Object

---

# ColumnDetector

Responsibilities

Find

Time

Force

Stroke

Extension

Stress

Strain

Temperature

Return Column Map

---

# UnitDetector

Responsibilities

Read Units

Verify Units

Convert Units

Return Conversion Factors

---

# Validator

Responsibilities

Header Validation

Column Validation

Unit Validation

Data Validation

Engineering Validation

Return Validation Result

---

# DataNormalizer

Responsibilities

Remove Blank Rows

Remove Duplicate Rows

Normalize Decimal Separator

Normalize Units

Create Internal Records

---

# RawDataStore

Responsibilities

Store Imported Data

Populate tblRawData

Create Import Session

Return Record Count

---

# ParserLogger

Responsibilities

Write

Import Log

Validation Log

Error Log

Performance Log

---

# Internal Data Flow

```
TXT

↓

String Array

↓

Header Object

↓

Column Map

↓

Validation

↓

Normalized Data

↓

tblRawData

↓

Engineering Engine
```

---

# Parser Output

Parser returns

ImportResult

Contains

Header

Units

Columns

Row Count

Warnings

Errors

Import Time

Status

---

# ImportResult Example

```
Status

VALID

Rows

15428

Warnings

1

Errors

0

Header

Valid

Units

Converted

ImportTime

1.34 sec
```

---

# Failure Handling

Any failure

↓

Parser stops

↓

ImportResult

Status

INVALID

↓

Ribbon displays error

↓

Engineering Engine not started

---

# Performance

Parser shall process

100000 rows

↓

Less than

5 seconds

---

# Memory Strategy

TXT loaded

Once

↓

Variant Array

↓

Processed

↓

Released

No duplicate arrays allowed.

---

# Error Recovery

Parser can restart

Without reopening workbook.

No worksheet cleanup required.

---

# Thread Safety

Current Version

Single Thread

Future

DLL Parser

Multi-threaded

Reserved.

---

# Future Extensions

Machine Profiles

Compressed TXT

Streaming Parser

Binary Reader

Cloud Import

Reserved.

---

# Acceptance Criteria

✔ Modular

✔ Independent

✔ Reusable

✔ No Engineering Logic

✔ No Worksheet Dependency

✔ High Performance

✔ Easy Maintenance

---

End of Document
