# Export History Database

Document ID : MTDMS-DB-016

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

The Export History Database records every export operation performed by MTDMS.

It records export activity only.

It never stores engineering calculations.

It never modifies engineering results.

---

# Objectives

The Export History Database shall

• Record Excel exports

• Record PDF exports

• Record print operations

• Record archive exports

• Preserve export traceability

• Support ISO/IEC 17025 audits

---

# Design Philosophy

TXT

↓

Engineering Report

↓

Approved Report

↓

Export

↓

Export History

Export records describe document distribution.

They do not contain engineering calculations.

---

# Table Name

tblExportHistory

---

# Primary Key

ExportID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ExportID

INTEGER

----------------------------

ExportGUID

TEXT

UUID

----------------------------

ReportID

INTEGER

Foreign Key

tblReport

----------------------------

CertificateID

INTEGER

Nullable

Foreign Key

tblCertificate

----------------------------

OperatorID

INTEGER

Foreign Key

tblOperator

----------------------------

ExportDate

DATE

----------------------------

ExportTime

TIME

----------------------------

ExportType

TEXT

Examples

Excel

PDF

Print

Archive

Image

Clipboard

----------------------------

DestinationFolder

TEXT

----------------------------

FileName

TEXT

----------------------------

FullPath

TEXT

----------------------------

FileExtension

TEXT

----------------------------

FileSize

INTEGER

Bytes

----------------------------

SHA256

TEXT

Nullable

----------------------------

ExportStatus

TEXT

Examples

Success

Failed

Cancelled

Warning

----------------------------

FailureReason

TEXT

Nullable

----------------------------

PrinterName

TEXT

Nullable

----------------------------

ExportProfile

TEXT

Nullable

----------------------------

Remarks

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

# Supported Export Types

Excel Workbook

PDF

Print

Archive Copy

PNG

JPEG

Clipboard

Future

CSV Summary

---

# Engineering Independence

Export history

shall never

modify

Engineering Results

Reports

Certificates

Imported TXT

---

# File Verification

Optional

Store

SHA256

of exported file

for future integrity verification.

---

# Print Logging

Print operations record

Printer

Copies

Timestamp

Operator

Result

---

# Archive Export

Archive export records

Archive Folder

Archive Name

Archive Status

---

# SQLite Relationships

tblExportHistory

↓

N : 1

tblReport

↓

N : 1

tblCertificate

↓

N : 1

tblOperator

↓

N : 1

tblAuditTrail

---

# Indexes

IX_ReportID

IX_ExportDate

IX_ExportType

IX_Operator

IX_Status

---

# Constraints

ReportID

Required

ExportType

Required

ExportStatus

Required

---

# Audit Trail

Store

Export

Operator

Destination

File

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Full Access

Quality Manager

Export

Reviewer

Read

Operator

Export

Read Only

View History

---

# Error Handling

Destination Missing

↓

Create Folder

Access Denied

↓

Abort

Disk Full

↓

Abort

Printer Missing

↓

Abort Print

Log Failure

---

# Performance

Export logging

Target

< 20 ms

---

# Acceptance Criteria

✔ Every export recorded

✔ Print operations recorded

✔ Archive operations recorded

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
