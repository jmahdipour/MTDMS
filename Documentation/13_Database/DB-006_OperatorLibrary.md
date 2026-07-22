# Operator Library

Document ID : MTDMS-DB-006

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

The Operator Library stores information about users who interact with MTDMS.

The library is used for traceability, authorization and audit logging.

It does not store engineering results.

It does not participate in engineering calculations.

---

# Objectives

The Operator Library shall

• Identify operators

• Identify reviewers

• Identify quality managers

• Support authorization

• Support audit trail

• Support report traceability

---

# Design Philosophy

Operator

↓

TXT Import

↓

Engineering Calculation

↓

Validation

↓

Report

↓

Audit Trail

Operator identity never affects engineering calculations.

---

# Table Name

tblOperator

---

# Primary Key

OperatorID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

OperatorID

INTEGER

----------------------------

OperatorCode

TEXT

Unique

----------------------------

FullName

TEXT

----------------------------

ShortName

TEXT

Nullable

----------------------------

EmployeeNumber

TEXT

Nullable

----------------------------

Department

TEXT

----------------------------

Position

TEXT

Examples

Operator

Reviewer

Quality Manager

Laboratory Manager

Administrator

----------------------------

Username

TEXT

----------------------------

WindowsAccount

TEXT

Nullable

----------------------------

Phone

TEXT

Nullable

----------------------------

Email

TEXT

Nullable

----------------------------

SignatureImage

TEXT

File Path

Nullable

----------------------------

Active

BOOLEAN

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

----------------------------

Remarks

TEXT

Nullable

---

# User Roles

Administrator

Laboratory Manager

Quality Manager

Reviewer

Operator

Read Only

Future Roles

Administrator configurable.

---

# Permissions

Administrator

Full Access

Laboratory Manager

Configuration

Quality Manager

Validation

Reviewer

Review

Operator

Import

Calculation

Report Generation

Read Only

View Only

---

# Engineering Independence

Operator information

shall never influence

Engineering Results

Material Properties

Graphs

Acceptance

Validation

---

# Signature Support

Optional

Stores

Image path only.

Electronic signature validation

is outside the scope of this module.

---

# Authentication

Current Version

Windows User

or

Application User

Administrator configurable.

---

# SQLite Relationships

tblOperator

↓

1 : N

tblImportHistory

↓

1 : N

tblReport

↓

1 : N

tblAuditTrail

↓

1 : N

tblExportHistory

---

# Indexes

IX_OperatorCode

IX_FullName

IX_Username

IX_Department

---

# Constraints

OperatorCode

UNIQUE

FullName

Required

Role

Required

---

# Audit Trail

Store

Operator

Action

Timestamp

Computer Name

Software Version

Result

---

# Security

Passwords

shall never be stored

in plain text.

If application authentication is used

passwords shall be stored

as cryptographic hashes.

---

# Error Handling

Duplicate OperatorCode

↓

Reject

Missing Name

↓

Reject

Unknown Role

↓

Reject

Inactive User

↓

Login Denied

---

# Acceptance Criteria

✔ Operator identification

✔ Role management

✔ Audit compatibility

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
