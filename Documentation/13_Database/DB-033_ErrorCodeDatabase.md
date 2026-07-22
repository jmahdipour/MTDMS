# Error Code Database

Document ID : MTDMS-DB-033

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

The Error Code Database defines all application error messages, warning messages, and information messages used by MTDMS.

It provides a centralized error management system.

It never performs engineering calculations.

It never modifies engineering data.

---

# Objectives

The Error Code Database shall

• Standardize error reporting

• Simplify troubleshooting

• Support multilingual messages

• Support engineering traceability

• Improve maintenance

---

# Design Philosophy

TXT File

↓

Import

↓

Calculation

↓

Validation

↓

Error Detection

↓

Message Database

The database only defines

how errors are presented.

---

# Table Name

tblErrorCode

---

# Primary Key

ErrorID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ErrorID

INTEGER

----------------------------

ErrorCode

TEXT

Unique

Examples

E0001

E0105

W0023

I0010

----------------------------

Category

TEXT

Examples

Import

Calculation

Validation

Database

Graph

Report

Archive

Export

Application

----------------------------

Severity

TEXT

Examples

Information

Warning

Error

Critical

----------------------------

Title

TEXT

----------------------------

Description

TEXT

----------------------------

RecommendedAction

TEXT

----------------------------

CanContinue

BOOLEAN

----------------------------

RequiresAdministrator

BOOLEAN

----------------------------

LogToAudit

BOOLEAN

----------------------------

Active

BOOLEAN

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

# Error Categories

Import

TXT File

Calculation

Validation

Material Library

Customer Library

Machine Library

Graph

Report

Certificate

Archive

Export

SQLite

Application

---

# Severity Levels

Information

↓

Continue

----------------------------

Warning

↓

Operator Decision

----------------------------

Error

↓

Abort Current Operation

----------------------------

Critical

↓

Stop Application

Administrator Intervention Required

---

# Typical Errors

E0001

TXT File Not Found

----------------------------

E0002

Unsupported TXT Format

----------------------------

E0101

Calculation Failed

----------------------------

E0201

Validation Failed

----------------------------

E0301

SQLite Database Locked

----------------------------

E0401

Report Template Missing

----------------------------

W0101

Duplicate TXT File

----------------------------

I0001

Calculation Completed Successfully

---

# Engineering Independence

The Error Code Database

shall never modify

Imported TXT

Engineering Results

Validation Results

Reports

Graphs

It provides

descriptions only.

---

# SQLite Relationships

tblErrorCode

↓

Referenced by

Import Engine

Calculation Engine

Validation Engine

Graph Engine

Report Engine

Backup Engine

Audit Trail

---

# Indexes

IX_ErrorCode

IX_Category

IX_Severity

---

# Constraints

ErrorCode

UNIQUE

Severity

Required

Category

Required

---

# Audit Trail

If

LogToAudit

is TRUE

Store

Error Code

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Modify

Quality Manager

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling Strategy

Information

↓

Continue

Warning

↓

Ask Operator

Error

↓

Abort Current Task

Critical

↓

Stop Application

Create Audit Record

---

# Performance

Error lookup

Target

< 5 ms

---

# Acceptance Criteria

✔ Centralized error management

✔ Standardized messages

✔ Severity levels supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
