# Data Integrity Manager

Document ID : MTDMS-DAT-005

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Data Management

Status

Production

---

# Purpose

The Data Integrity Manager guarantees that imported test data remains complete, unchanged and traceable throughout its entire lifecycle.

This module protects the integrity of the original exported machine file and every internally generated dataset.

The module shall never modify engineering calculations.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 27001 (Recommended)

---

# Objectives

The Data Integrity Manager shall

• Detect file corruption

• Detect unauthorized modification

• Preserve original exported files

• Verify imported datasets

• Verify database consistency

• Maintain complete traceability

---

# Integrity Workflow

```
Machine Export File

↓

Checksum

↓

Import

↓

Normalization

↓

SQLite Storage

↓

Verification

↓

Engineering Engine

↓

Report

↓

Archive
```

---

# Protected Objects

Original File

Parsed Data

Normalized Data

Engineering Dataset

Graphs

Reports

PDF

SQLite Records

Configuration Files

---

# Integrity Levels

Level 1

Original File

↓

Level 2

Imported Dataset

↓

Level 3

SQLite Record

↓

Level 4

Report

↓

Level 5

Archive

---

# Checksum Algorithms

Supported

CRC32

SHA-256 (Preferred)

Future

SHA-512

Administrator configurable.

---

# Original File Protection

Original exported files

shall

Never Be Modified

Never Be Renamed

Never Be Rewritten

Only copied to archive.

---

# Internal Dataset Verification

Verify

Row Count

Column Count

Checksum

Header

Metadata

Channel Definitions

Sample Count

---

# Database Integrity

Verify

Primary Keys

Foreign Keys

Record Count

Checksum

Schema Version

Table Consistency

---

# Record Fingerprint

Each imported dataset receives

Integrity ID

SHA-256

Import Timestamp

Operator

Database Version

---

# Verification Events

Verification occurs

After Import

Before Engineering Calculation

Before Report Generation

Before PDF Export

Before Archive

During Restore

---

# Integrity Status

Verified

Warning

Failed

Corrupted

Archived

---

# Corruption Detection

Examples

Modified TXT File

Missing Rows

Modified Metadata

Unexpected Record Count

Checksum Mismatch

Database Corruption

---

# Integrity Actions

Verification Passed

↓

Continue

Verification Warning

↓

Log Warning

Verification Failed

↓

Abort Engineering

---

# Data Locking

After report approval

Engineering dataset

becomes

Read Only

Any modification requires

New Revision

---

# SQLite Database

Tables

```
tblIntegrity

tblChecksum

tblIntegrityHistory

tblVerification
```

---

# Audit Trail

Every verification stores

Integrity ID

Timestamp

Operator

Checksum

Status

Verification Result

Computer Name

---

# Permissions

Administrator

Full Access

Quality Manager

Verification

Operator

Read Only

---

# Error Handling

Checksum Failure

↓

Reject

Database Mismatch

↓

Abort

Corrupted Record

↓

Restore Backup

Verification Timeout

↓

Retry

---

# Future Enhancements

Blockchain Verification

Digital Fingerprint

Cloud Verification

Automatic Integrity Monitor

Reserved

---

# Acceptance Criteria

✔ Original files preserved

✔ SHA-256 verification

✔ Database integrity verification

✔ Engineering data protected

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
