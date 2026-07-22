# Backup and Restore Manager

Document ID : MTDMS-DB-018

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

The Backup and Restore Manager protects all configuration and historical data stored by MTDMS.

Engineering calculations are regenerated from the original TXT file.

Backups therefore protect

configuration

history

templates

libraries

audit trail

not the engineering calculations themselves.

---

# Objectives

The module shall

• Create manual backups

• Create automatic backups

• Restore databases

• Verify backup integrity

• Maintain backup history

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Report

↓

SQLite

↓

Backup

The TXT file remains the engineering master record.

SQLite protects application metadata.

---

# Backup Scope

Included

Configuration

Material Library

Customer Library

Machine Library

Operator Library

Standard Library

Templates

Audit Trail

Archive Records

Report History

Certificate History

Export History

Import History

Validation History

Database Version

Excluded

TXT files

Excel Reports

PDF Reports

Graph Images

These files remain in the archive folders.

---

# Backup Types

Automatic

Manual

Before Database Upgrade

Before Configuration Change

Administrator configurable.

---

# Default Backup Structure

```
Backup

│

├── Daily

├── Weekly

├── Monthly

├── Manual

└── BeforeUpgrade
```

---

# Backup Naming

Example

```
MTDMS_2026-07-21_103500.db
```

Format

DatabaseName

Date

Time

Extension

---

# Restore Scope

Complete Database

Configuration Only

Material Library

Customer Library

Templates

Audit Trail

Administrator configurable.

---

# Restore Rules

Before Restore

↓

Verify Backup

↓

Create Current Backup

↓

Restore

↓

Verify Database

↓

Continue

---

# Backup Verification

Every backup shall verify

SQLite structure

Database size

Integrity

Checksum

Readable status

---

# Table Name

tblBackupHistory

---

# Primary Key

BackupID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

BackupID

INTEGER

----------------------------

BackupGUID

TEXT

UUID

----------------------------

BackupDate

DATE

----------------------------

BackupTime

TIME

----------------------------

BackupType

TEXT

Examples

Automatic

Manual

Upgrade

Restore Point

----------------------------

BackupFile

TEXT

----------------------------

BackupFolder

TEXT

----------------------------

DatabaseVersion

TEXT

----------------------------

BackupSize

INTEGER

Bytes

----------------------------

SHA256

TEXT

----------------------------

BackupStatus

TEXT

Examples

Success

Failed

Cancelled

----------------------------

OperatorID

INTEGER

Nullable

----------------------------

Remarks

TEXT

Nullable

---

# SQLite Relationships

tblBackupHistory

↓

Referenced by

System Initialization

Database Upgrade

Audit Trail

---

# Backup Retention

Daily

30 copies

Weekly

26 copies

Monthly

24 copies

Manual

Unlimited

Administrator configurable.

---

# Engineering Independence

Backup

never stores

engineering calculations.

Engineering calculations

are regenerated

from the original TXT.

---

# Audit Trail

Store

Backup

Restore

Operator

Timestamp

Computer

Software Version

Result

---

# Permissions

Administrator

Backup

Restore

Delete Backup

Quality Manager

Manual Backup

Reviewer

Read

Operator

No Restore

---

# Error Handling

Backup Folder Missing

↓

Create Folder

Backup Failure

↓

Abort

Checksum Failure

↓

Reject Restore

Database Locked

↓

Retry

Restore Failure

↓

Restore Previous Backup

---

# Performance

Typical Backup

< 2 seconds

Typical Restore

< 5 seconds

Standard database

---

# Acceptance Criteria

✔ Automatic backup

✔ Manual backup

✔ Restore supported

✔ Integrity verification

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering data protected through TXT master files

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
