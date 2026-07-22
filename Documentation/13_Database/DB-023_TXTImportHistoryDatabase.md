# TXT Import History Database

Document ID : MTDMS-DB-023

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

The TXT Import History Database records every TXT file imported into MTDMS.

The imported TXT file is the only engineering source used by the system.

Engineering calculations are always performed from the imported TXT file.

The TXT file is never modified.

---

# Objectives

The Import History Database shall

• Register imported TXT files

• Prevent duplicate imports

• Verify file integrity

• Preserve engineering traceability

• Support regeneration of reports

---

# Design Philosophy

TXT File

↓

Import

↓

SQLite Registration

↓

Engineering Calculation

↓

Graph

↓

Report

The original TXT file remains unchanged.

---

# Table Name

tblImportHistory

---

# Primary Key

ImportID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ImportID

INTEGER

----------------------------

ImportGUID

TEXT

UUID

----------------------------

ImportDate

DATE

----------------------------

ImportTime

TIME

----------------------------

TXTFileName

TEXT

----------------------------

TXTFilePath

TEXT

----------------------------

TXTFileSize

INTEGER

Bytes

----------------------------

SHA256

TEXT

----------------------------

MachineID

INTEGER

Foreign Key

tblMachine

----------------------------

OperatorID

INTEGER

Foreign Key

tblOperator

----------------------------

CustomerID

INTEGER

Nullable

----------------------------

MaterialID

INTEGER

Nullable

----------------------------

StandardID

INTEGER

Nullable

----------------------------

TXTVersion

TEXT

----------------------------

ImportStatus

TEXT

Examples

Success

Duplicate

Cancelled

Corrupted

Failed

----------------------------

ImportRemarks

TEXT

Nullable

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

---

# TXT Integrity

During import

the application shall calculate

SHA256

for every TXT file.

The checksum shall be stored

for duplicate detection

and integrity verification.

---

# Duplicate Detection

Duplicate detection shall compare

SHA256

TXT size

TXT filename

If SHA256 is identical

↓

Warn operator

↓

Operator decides

Continue

or

Cancel

---

# Engineering Independence

The Import History Database

does not contain

engineering calculations.

It contains only

references

to imported TXT files.

---

# TXT File Rules

The application

shall never

modify

Rename

Rewrite

Delete

the imported TXT file.

The TXT file is read only.

---

# SQLite Relationships

tblImportHistory

↓

1 : N

tblReport

↓

1 : N

tblValidation

↓

1 : N

tblArchive

↓

1 : N

tblAuditTrail

---

# Indexes

IX_SHA256

IX_ImportDate

IX_TXTFileName

IX_MachineID

IX_OperatorID

---

# Constraints

SHA256

Required

TXTFilePath

Required

ImportDate

Required

---

# Audit Trail

Record

TXT filename

Import date

Operator

Machine

SHA256

Computer

Software Version

---

# Permissions

Administrator

Full Access

Quality Manager

Read

Reviewer

Read

Operator

Import

Read

---

# Error Handling

TXT Missing

↓

Abort

TXT Corrupted

↓

Abort

Unsupported TXT Version

↓

Warning

Duplicate TXT

↓

Warning

File Access Denied

↓

Abort

---

# Performance

TXT registration

Target

< 100 ms

Checksum calculation

Depends on file size

---

# Acceptance Criteria

✔ Every TXT import recorded

✔ SHA256 stored

✔ Duplicate detection supported

✔ Original TXT unchanged

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
