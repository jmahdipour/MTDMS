# Report Field Mapping Database

Document ID : MTDMS-DB-031

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

The Report Field Mapping Database defines how engineering results are transferred to Excel report templates.

It provides a configurable mapping between calculated results and Excel cells.

No engineering calculation is performed in this database.

---

# Objectives

The Report Field Mapping Database shall

• Map engineering values to Excel cells

• Support multiple report templates

• Support multiple standards

• Allow template changes without changing VBA code

• Simplify report maintenance

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Engineering Results

↓

Field Mapping

↓

Excel Report

Mapping defines

where

a value is written.

It never changes

the value itself.

---

# Table Name

tblReportFieldMapping

---

# Primary Key

MappingID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

MappingID

INTEGER

----------------------------

TemplateID

INTEGER

Foreign Key

tblTemplate

----------------------------

StandardID

INTEGER

Nullable

Foreign Key

tblStandard

----------------------------

WorksheetName

TEXT

----------------------------

CellAddress

TEXT

Examples

B5

F12

H28

AA10

----------------------------

FieldCode

TEXT

Examples

YieldStrength

UltimateStrength

YoungModulus

MaximumForce

MaximumDisplacement

CustomerName

MaterialGrade

MachineName

OperatorName

ReportNumber

CertificateNumber

TestDate

TestTime

----------------------------

DataSource

TEXT

Examples

EngineeringResult

MaterialLibrary

Customer

Machine

Operator

Configuration

Application

----------------------------

NumberFormat

TEXT

Examples

0.00

0.000

0%

0.0 MPa

----------------------------

Visible

BOOLEAN

----------------------------

Locked

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

# Supported Data Sources

Engineering Results

Material Library

Customer Library

Machine Library

Operator Library

Configuration

System Information

Report Information

Certificate Information

---

# Mapping Rules

One field

↓

One destination cell

Multiple fields

shall never

write to the same cell.

---

# Empty Values

If a field is unavailable

↓

Leave cell blank

unless

a default value

has been defined.

---

# Engineering Independence

Mapping

shall never

modify

Engineering Results

Imported TXT

Validation Results

Graphs

Only the destination

inside Excel

is defined.

---

# SQLite Relationships

tblReportFieldMapping

↓

N : 1

tblTemplate

↓

N : 1

tblStandard

↓

Referenced by

Report Engine

---

# Indexes

IX_TemplateID

IX_FieldCode

IX_Worksheet

IX_CellAddress

---

# Constraints

TemplateID

Required

WorksheetName

Required

CellAddress

Required

FieldCode

Required

Unique

TemplateID + WorksheetName + CellAddress

---

# Audit Trail

Store

Template

Field

Old Cell

New Cell

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

# Error Handling

Missing Template

↓

Abort Report

Missing Cell

↓

Abort

Duplicate Mapping

↓

Reject

Invalid Address

↓

Reject

---

# Performance

Mapping loading

Target

< 30 ms

---

# Acceptance Criteria

✔ Excel field mapping configurable

✔ No hardcoded report locations

✔ Multiple templates supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
