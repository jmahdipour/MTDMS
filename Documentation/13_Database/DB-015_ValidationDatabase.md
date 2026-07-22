# Validation Database

Document ID : MTDMS-DB-015

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

The Validation Database stores the results of all engineering validation processes performed by MTDMS.

It records the outcome of validation only.

It never performs engineering calculations.

It never modifies imported TXT data.

---

# Objectives

The Validation Database shall

• Record validation results

• Record validation history

• Preserve engineering traceability

• Support report approval

• Support ISO/IEC 17025 audits

---

# Design Philosophy

TXT

↓

Engineering Calculation

↓

Validation Engine

↓

Validation Record

↓

Report Approval

Validation records document engineering verification.

They never replace engineering calculations.

---

# Table Name

tblValidation

---

# Primary Key

ValidationID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ValidationID

INTEGER

----------------------------

ValidationGUID

TEXT

UUID

----------------------------

ImportID

INTEGER

Foreign Key

tblImportHistory

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

ValidationDate

DATE

----------------------------

ValidationTime

TIME

----------------------------

OperatorID

INTEGER

Foreign Key

tblOperator

----------------------------

ReviewerID

INTEGER

Nullable

Foreign Key

tblOperator

----------------------------

ValidationProfile

TEXT

Examples

ISO 6892-1

ISO 6508

ISO 6507

ISO 148

Customer

Internal

----------------------------

ValidationStage

TEXT

Examples

Automatic

Manual

Final Review

----------------------------

ValidationStatus

TEXT

Examples

Passed

Failed

Warning

Cancelled

----------------------------

FailureCount

INTEGER

----------------------------

WarningCount

INTEGER

----------------------------

ValidationSummary

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

# Validation Stages

Automatic Validation

↓

Manual Review

↓

Quality Review

↓

Final Approval

---

# Validation Scope

The Validation Database records

Engineering consistency

Required fields

Graph generation status

Report completeness

TXT integrity verification

Reference standard verification

---

# Engineering Independence

Validation records

shall never

modify

Engineering Results

Engineering Tables

Graphs

Imported TXT

---

# TXT Verification

Validation shall verify

TXT checksum

TXT completeness

TXT readability

TXT format

Results are recorded

but the TXT file is never modified.

---

# SQLite Relationships

tblValidation

↓

N : 1

tblReport

↓

N : 1

tblCertificate

↓

N : 1

tblImportHistory

↓

N : 1

tblAuditTrail

---

# Indexes

IX_ReportID

IX_ValidationDate

IX_Status

IX_Profile

IX_Operator

---

# Constraints

ValidationStatus

Required

ValidationProfile

Required

ImportID

Required

---

# Audit Trail

Store

Validation

Operator

Reviewer

Profile

Result

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Reviewer

Review

Operator

Automatic Validation Only

Read Only

View Results

---

# Error Handling

Missing Report

↓

Abort

Missing Import

↓

Abort

Invalid Profile

↓

Reject

Validation Failure

↓

Store Failure

Continue Review

---

# Performance

Validation record insertion

Target

< 50 ms

---

# Acceptance Criteria

✔ Validation history stored

✔ TXT verification recorded

✔ Engineering calculations unaffected

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
