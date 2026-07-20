# TXT Import Security Specification

Document ID : MTDMS-IMP-015

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines all security requirements for importing TXT files.

The objective is to ensure that imported test data remains authentic, traceable, protected, and compliant with ISO/IEC 17025.

The original TXT file shall never be modified.

---

# Security Objectives

✔ Data Integrity

✔ Data Authenticity

✔ Traceability

✔ Protection Against Accidental Modification

✔ Audit Trail

✔ Controlled Import

✔ Safe Recovery

---

# Security Workflow

```
Select TXT

↓

Read Only

↓

Checksum

↓

Validation

↓

Import

↓

Archive Metadata

↓

Audit Log
```

---

# File Access

TXT files shall always be opened as

Read Only

No write access shall ever be requested.

---

# Original File Protection

The original TXT file

Shall never

Be modified

Renamed

Reformatted

Compressed

Edited

Deleted

---

# Import Copy

Only the parsed data is stored.

Original TXT remains untouched.

---

# Checksum

Optional

SHA-256

or

MD5

Stored

SQLite

Purpose

Detect later modification of original TXT.

---

# Import Identity

Each import receives

Import ID

GUID

Example

```
IMP-2026-000015
```

---

# Import Timestamp

Recorded

Date

Time

Operator

Workbook Version

Machine

TXT Filename

---

# Operator Authentication

Current User

↓

Workbook Login

↓

Stored with Import

---

# Machine Identity

Imported Header shall store

Machine Name

Machine Model

Machine Serial Number

PLC Type

Software Version

if available.

---

# Project Association

Every imported TXT belongs to exactly one Project.

One Project

↓

Many Reports

↓

One Original TXT

---

# Duplicate Protection

Before import

System checks

Checksum

File Name

File Size

Timestamp

If duplicate detected

↓

Warning

↓

Operator decides

Import Again

or

Cancel

---

# Tamper Detection

If checksum differs

↓

Security Warning

↓

Original Import remains unchanged

↓

New Import receives new Import ID

---

# Audit Trail

Every import creates

Audit Record

Contains

Import ID

Project

Operator

Date

TXT Name

Checksum

Validation Status

Workbook Version

---

# Error Protection

Import failure

↓

Rollback

↓

No partial data remains

↓

No orphan database records

---

# SQLite Protection

Imported data

Stored inside transaction.

Commit only after successful validation.

Rollback on failure.

---

# Workbook Protection

Import worksheets

Hidden

Protected

Users cannot edit raw imported data.

---

# Raw Data Lock

tblRawData

Read Only

Engineering Engine

Read Only

Reports

Read Only

Only Import Controller may create new records.

---

# Logging

Security Log

Contains

Failed Imports

Duplicate Files

Modified Files

Unauthorized Access

Checksum Errors

---

# Administrator Permissions

Administrator may

View Logs

Restore Imports

Rebuild Database

Cannot modify original imported records.

---

# Backup Strategy

Before major update

SQLite Backup

Workbook Backup

Configuration Backup

---

# Recovery

If workbook crashes

Last completed import remains valid.

Incomplete imports are discarded automatically.

---

# Future Security

Digital Signature

Machine Certificate

Encrypted Archive

Cloud Audit

Electronic Signature

Reserved

---

# Acceptance Criteria

✔ TXT always opened Read Only

✔ Original TXT never modified

✔ Import completely traceable

✔ Audit trail maintained

✔ SQLite transaction safe

✔ Rollback supported

✔ Duplicate detection available

✔ ISO 17025 compliant

---

End of Document
