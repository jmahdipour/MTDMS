# Database Maintenance

Document ID : MTDMS-DB-021

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

This document defines preventive maintenance procedures for the MTDMS SQLite database.

The objective is to maintain

Performance

Integrity

Reliability

Traceability

without affecting engineering data.

---

# Objectives

The maintenance system shall

• Verify database integrity

• Detect corruption

• Optimize performance

• Verify indexes

• Verify relationships

• Verify backups

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

SQLite

↓

Maintenance

Database maintenance

never modifies

engineering calculations.

---

# Maintenance Categories

Daily

Weekly

Monthly

Yearly

Administrator configurable.

---

# Daily Maintenance

Verify SQLite integrity

Verify database availability

Verify backup creation

Verify archive folders

Verify free disk space

Verify application version

---

# Weekly Maintenance

Run

PRAGMA integrity_check

Verify indexes

Verify foreign keys

Verify audit trail

Verify backup history

Verify report history

---

# Monthly Maintenance

Run

VACUUM

Run

ANALYZE

Optimize indexes

Check archive references

Check orphan records

Verify configuration

---

# Yearly Maintenance

Archive old backups

Verify database version

Verify migration history

Verify storage capacity

Generate maintenance report

---

# SQLite Commands

Integrity Check

```
PRAGMA integrity_check;
```

---

Foreign Key Check

```
PRAGMA foreign_key_check;
```

---

Optimize

```
ANALYZE;
```

---

Reclaim Space

```
VACUUM;
```

---

# Database Integrity

The following shall be verified

Primary Keys

Foreign Keys

Unique Constraints

Indexes

Schema Version

Backup Availability

---

# Relationship Verification

Verify

Import

↓

Report

↓

Certificate

↓

Archive

No broken references

shall exist.

---

# Engineering Independence

Maintenance

shall never

modify

Imported TXT

Engineering Results

Engineering Tables

Graph Data

Report Values

---

# Maintenance Log

Table

tblMaintenanceHistory

---

# Primary Key

MaintenanceID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

MaintenanceID

INTEGER

----------------------------

MaintenanceDate

DATE

----------------------------

MaintenanceTime

TIME

----------------------------

MaintenanceType

TEXT

Examples

Daily

Weekly

Monthly

Yearly

----------------------------

OperatorID

INTEGER

Nullable

----------------------------

IntegrityStatus

TEXT

----------------------------

BackupStatus

TEXT

----------------------------

IndexStatus

TEXT

----------------------------

RelationshipStatus

TEXT

----------------------------

DatabaseSize

INTEGER

Bytes

----------------------------

Duration

REAL

Seconds

----------------------------

Remarks

TEXT

Nullable

---

# Error Handling

Integrity Failure

↓

Stop

Backup Failure

↓

Warning

Foreign Key Failure

↓

Reject

Corrupted Database

↓

Restore Backup

Disk Full

↓

Abort

---

# Automatic Maintenance

Supported

Application Startup

Daily

Weekly

Monthly

Administrator configurable.

---

# Performance Targets

Integrity Check

< 5 seconds

Analyze

< 3 seconds

Vacuum

Depends on database size

---

# Audit Trail

Store

Maintenance Type

Operator

Timestamp

Result

Computer Name

Software Version

---

# Permissions

Administrator

Full Access

Quality Manager

Execute Maintenance

Reviewer

Read

Operator

Read Only

---

# Acceptance Criteria

✔ Integrity verified

✔ Backups verified

✔ Relationships verified

✔ SQLite optimized

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete maintenance history

---

End of Document
