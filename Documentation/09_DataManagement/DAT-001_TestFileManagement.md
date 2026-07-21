# Test File Management

Document ID : MTDMS-DAT-001

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

The Test File Management module is responsible for managing all files imported from testing machines.

This module does NOT communicate with the testing machine.

It only manages files that have already been exported from the testing machine.

---

# Scope

Supported operations

Import

Archive

Copy

Move

Rename

Index

Search

Restore

Export

Delete (Logical)

---

# Supported File Types

TXT

CSV

DAT

XML (Future)

JSON (Future)

Administrator configurable.

---

# Source

Machine Export Folder

USB Flash Drive

Network Folder

Local Folder

Shared Folder

---

# Import Workflow

```
Select Folder

↓

Scan Files

↓

Validate File

↓

Read Header

↓

Read Data

↓

Generate Internal ID

↓

Store Metadata

↓

Archive Original

↓

Ready
```

---

# Original File Policy

Original machine files

shall NEVER

be modified.

The original file is stored exactly as received.

---

# Internal Storage

Each imported file receives

Internal File ID

Original File Name

Import Date

Import Time

Operator

Machine Type

File Size

Checksum

Status

---

# File Status

Imported

Validated

Processed

Reported

Archived

Rejected

Deleted (Logical)

---

# Folder Structure

```
MTDMS

 ├── Import

 ├── Archive

 ├── Reports

 ├── PDF

 ├── Backup

 ├── Temp

 ├── Logs

 └── Database
```

Folder names configurable.

---

# Archive Policy

After successful import

Original File

↓

Archive Folder

File name remains unchanged.

---

# Duplicate Detection

Duplicate detection based on

Checksum

OR

Original File Name

OR

Internal File ID

Administrator configurable.

---

# Checksum

Supported

CRC32

SHA-256 (Preferred)

Used for

Duplicate Detection

Integrity Verification

Archive Verification

---

# Metadata

Stored information

Original Name

Extension

Creation Date

Import Date

Operator

Material

Machine

Sample ID

Certificate ID

File Size

Checksum

---

# Search

Search by

File Name

Sample ID

Material

Certificate

Import Date

Operator

Machine

Status

---

# Rename Policy

Original File

Never Renamed

Internal Display Name

May be changed.

---

# Logical Delete

Files are never physically deleted.

Status becomes

Deleted

Administrator may restore.

---

# Restore

Restore from

Archive

Backup

Logical Delete

---

# Export

Supported

Original File

CSV

Engineering CSV

ZIP Package

---

# SQLite Database

Tables

```
tblImportedFile

tblFileArchive

tblFileHistory
```

---

# Audit Trail

Every action records

User

Action

Timestamp

Computer

Old Status

New Status

Reason

---

# Validation

Invalid Extension

↓

Reject

Empty File

↓

Reject

Corrupted Header

↓

Reject

Checksum Error

↓

Reject

---

# Error Handling

Missing File

↓

Abort

Locked File

↓

Retry

Duplicate File

↓

Warning

Archive Failure

↓

Abort

---

# Future Enhancements

Automatic Folder Monitoring

Cloud Archive

File Compression

Automatic OCR

Reserved

---

# Acceptance Criteria

✔ Original file preserved

✔ No machine communication

✔ Duplicate detection

✔ Archive management

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
