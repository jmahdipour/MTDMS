# File Architecture

Document ID

MTDMS-FILE-001

Version

1.0

Status

Core Architecture

Platform

Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines every file handled by MTDMS.

Files are divided into

Input

Temporary

Output

Archive

Configuration

Database

---

# Architecture

Device TXT

↓

Engineering Dataset

↓

Calculation

↓

Report

↓

Archive

---

# File Types

Input

Temporary

Output

Archive

Configuration

Database

Log

Backup

---

# Input Files

TXT

Device Export

Read Only

Never Modified

---

# Temporary Files

Session Cache

Undo Cache

Graph Cache

Temporary CSV

Deleted after session.

---

# Output Files

Excel Report

PDF Report

CSV Curve

JSON Metadata (Future)

---

# Archive Files

Curve Binary

Curve CSV

Curve JSON (Future)

Image Export

Digital Signature

---

# Configuration Files

Settings.db

Ribbon.xml

Material Library

Standards Library

Logo

Language Files

---

# Database Files

SQLite

Only

Metadata

Results

Audit

Configuration

No Engineering Arrays

---

# Log Files

Execution Log

Import Log

Calculation Log

Error Log

Audit Log

---

# Backup Files

Automatic

Daily

Weekly

Monthly

Administrator configurable.

---

# Directory Structure

MTDMS

│

├── Database

│

├── Settings

│

├── Materials

│

├── Standards

│

├── Reports

│

├── Curves

│

├── Logs

│

├── Backup

│

├── Templates

│

└── Temporary

---

# Curve Files

Recommended

```
Curve_YYYYMMDD_HHMMSS_TestID.bin
```

Example

```
Curve_20260726_145325_12548.bin
```

---

# Report Files

```
Report_TestID.pdf

Report_TestID.xlsx
```

---

# Metadata Files

Future

```
TestID.json
```

---

# File Naming Rule

Every generated file receives

Project ID

Test ID

Timestamp

Revision

Operator

if required.

---

# Integrity

Every archive file receives

SHA256 Hash

Stored inside SQLite.

---

# Read Rule

Only

Import Engine

reads TXT.

No other engine reads device files.

---

# Write Rule

Only

Report Engine

writes reports.

Only

Archive Engine

writes archive files.

---

# Delete Rule

Temporary files

↓

Automatic

Reports

↓

Manual

Archive

↓

Never automatically deleted

---

# Acceptance

✔ Structured

✔ Traceable

✔ ISO 17025 Ready

✔ Backup Ready

✔ High Performance

✔ Expandable

---

End Of Document
