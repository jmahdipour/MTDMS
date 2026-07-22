# Audit Trail Database

Document ID : MTDMS-DB-011

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

The Audit Trail Database records every important action performed inside MTDMS.

The Audit Trail guarantees complete traceability.

It records who performed an action, when it occurred, where it occurred and what object was affected.

The Audit Trail never stores engineering calculations.

It never modifies engineering data.

---

# Objectives

The Audit Trail shall

• Record user actions

• Record software actions

• Record report actions

• Record database actions

• Preserve complete traceability

• Support ISO/IEC 17025 audits

---

# Design Philosophy

User Action

↓

Application

↓

Audit Record

↓

SQLite

Audit information is permanent.

Audit records shall never be edited.

---

# Table Name

tblAuditTrail

---

# Primary Key

AuditID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

AuditID

INTEGER

----------------------------

AuditGUID

TEXT

UUID

----------------------------

EventDate

DATE

----------------------------

EventTime

TIME

----------------------------

OperatorID

INTEGER

Foreign Key

tblOperator

----------------------------

UserName

TEXT

----------------------------

ComputerName

TEXT

----------------------------

WindowsUser

TEXT

----------------------------

SoftwareVersion

TEXT

----------------------------

Module

TEXT

Examples

Import

Calculation

Validation

Graph

Reporting

Export

Database

Configuration

Archive

----------------------------

Action

TEXT

Examples

Create

Modify

Delete

Import

Export

Print

Approve

Archive

Login

Logout

----------------------------

ObjectType

TEXT

Examples

TXT

Report

Certificate

Material

Customer

Machine

Template

Database

----------------------------

ObjectID

INTEGER

Nullable

----------------------------

ObjectReference

TEXT

Nullable

----------------------------

PreviousValue

TEXT

Nullable

----------------------------

NewValue

TEXT

Nullable

----------------------------

Result

TEXT

Examples

Success

Failed

Cancelled

Warning

----------------------------

ErrorMessage

TEXT

Nullable

----------------------------

Remarks

TEXT

Nullable

---

# Events to Record

Login

Logout

TXT Import

TXT Import Failure

Material Update

Customer Update

Machine Update

Calculation Completed

Validation Completed

Report Generated

Certificate Generated

Excel Export

PDF Export

Print

Archive

Backup

Restore

Configuration Change

Template Change

Database Upgrade

---

# Engineering Independence

Audit Trail

never changes

Engineering Results

Graphs

Validation

Reports

Certificates

---

# Automatic Logging

Every critical operation

shall automatically

create

one audit record.

Manual logging is not permitted.

---

# Log Retention

Default

Permanent

Administrator configurable.

Records shall never be physically deleted.

Logical archive only.

---

# SQLite Relationships

tblAuditTrail

↓

N : 1

tblOperator

↓

N : 1

tblReport

↓

N : 1

tblCertificate

↓

N : 1

tblImportHistory

---

# Indexes

IX_EventDate

IX_Operator

IX_Module

IX_Action

IX_ObjectType

IX_Result

---

# Constraints

EventDate

Required

EventTime

Required

Module

Required

Action

Required

Result

Required

---

# Search

Supported

Date

Operator

Module

Action

Object

Certificate

Report

TXT

Machine

Result

---

# Permissions

Administrator

Read

Export

Quality Manager

Read

Reviewer

Read

Operator

No Edit

No Delete

---

# Error Handling

Logging Failure

↓

Warning

Continue Application

Audit failure

shall never stop

engineering calculations.

---

# Performance

Audit record insertion

Target

< 20 ms

---

# Acceptance Criteria

✔ Automatic logging

✔ Permanent records

✔ Search supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
