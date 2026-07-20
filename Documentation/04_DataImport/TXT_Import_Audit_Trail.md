# TXT Import Audit Trail Specification

Document ID : MTDMS-IMP-034

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Database

SQLite

Compliance

ISO/IEC 17025

ISO 9001

21 CFR Part 11 (Future Ready)

---

# Purpose

This document defines the complete audit trail generated during TXT import.

Every action affecting imported data shall be permanently recorded.

The audit trail shall be immutable.

No audit record may be edited or deleted.

---

# Philosophy

Operator

↓

Ribbon

↓

TXT Import

↓

Audit Record

↓

SQLite

↓

Permanent History

---

# Objectives

Complete Traceability

Data Integrity

Operator Accountability

Import History

Engineering History

Regulatory Compliance

---

# Audit Scope

The following events shall be audited

Project Creation

TXT Selection

TXT Import

Validation

Unit Conversion

Material Recognition

Standard Recognition

Machine Profile Selection

Engineering Calculation

Graph Correction

Report Generation

Operator Override

Recalculation

Export

Backup

Restore

---

# Audit Workflow

```
Action

↓

Timestamp

↓

Operator

↓

Project

↓

Session

↓

Result

↓

Audit Database
```

---

# SQLite Table

```
tblAuditTrail
```

---

# Table Structure

| Field | Type | Description |
|--------|------|-------------|
| AuditID | INTEGER | Primary Key |
| ProjectID | INTEGER | Project Reference |
| SessionID | INTEGER | Import Session |
| EventType | TEXT | Action Type |
| EventCode | TEXT | Internal Code |
| Operator | TEXT | Logged User |
| Machine | TEXT | Machine Name |
| Timestamp | DATETIME | Event Time |
| Description | TEXT | Detailed Description |
| Status | TEXT | Success / Warning / Error |
| OldValue | TEXT | Previous Value |
| NewValue | TEXT | Current Value |
| ComputerName | TEXT | Workstation |
| WorkbookVersion | TEXT | Software Version |

---

# Event Types

PROJECT_CREATED

TXT_SELECTED

TXT_IMPORTED

HEADER_VALIDATED

COLUMN_MAPPED

UNITS_CONVERTED

RAWDATA_STORED

ENGINEERING_STARTED

ENGINEERING_COMPLETED

GRAPH_CORRECTED

REPORT_CREATED

REPORT_PRINTED

REPORT_EXPORTED

PROJECT_ARCHIVED

BACKUP_CREATED

RESTORE_COMPLETED

USER_OVERRIDE

ERROR

WARNING

---

# Event Codes

```
AUD-0001

Project Created
```

```
AUD-0101

TXT Imported
```

```
AUD-0201

Header Validated
```

```
AUD-0301

Engineering Started
```

```
AUD-0401

Graph Corrected
```

```
AUD-0501

Report Generated
```

---

# Import Audit Example

```
AuditID

1542

Project

2026-00014

Operator

Mahdipour

Action

TXT Imported

Machine

Shimadzu AG-25TB

Time

2026-07-20

14:32:11

Status

Success
```

---

# Operator Override

Every manual action shall be recorded.

Examples

Material Changed

Yield Point Moved

Machine Profile Changed

Standard Changed

Area Changed

Graph Reset

---

# Error Logging

Every failure records

Error Code

Module

Operator

Project

Timestamp

Description

Recovery Action

---

# Warning Logging

Warnings do not stop import.

Examples

Unknown Material

Unknown Standard

Area Difference

Large File

Duplicate TXT

---

# Security

Audit records are

Append Only

UPDATE

Not Allowed

DELETE

Not Allowed

INSERT

Allowed

---

# Retention

Audit records shall remain available

For the entire life of the project.

No automatic deletion.

---

# Search

Operator may search by

Project

Operator

Machine

Date

Event

Status

---

# Reports

Audit Report may include

Timeline

Operator Actions

Import History

Validation History

Graph Corrections

Report History

---

# Backup

Audit Trail included in

SQLite Backup

Workbook Backup

Archive Package

---

# Future Features

Electronic Signature

Digital Certificate

Cloud Audit

Blockchain Verification

Reserved

---

# Acceptance Criteria

✔ Every important action logged

✔ Immutable records

✔ SQLite compatible

✔ Searchable

✔ ISO 17025 compliant

✔ Operator accountability maintained

✔ Complete project history available

---

End of Document
