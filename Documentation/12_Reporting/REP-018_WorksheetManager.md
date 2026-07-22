# Worksheet Manager

Document ID : MTDMS-REP-018

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Reporting

Status

Production

---

# Purpose

The Worksheet Manager is responsible for creating, updating, protecting and maintaining all worksheets used by the MTDMS reporting system.

The Worksheet Manager manages worksheet structure only.

It never performs engineering calculations.

It never changes validated engineering results.

---

# Design Principles

Every worksheet shall have

One clear purpose

One owner

One layout

One protection policy

---

# Responsibilities

Create worksheets

Delete temporary worksheets

Update report worksheets

Rename worksheets

Protect worksheets

Restore missing worksheets

Maintain worksheet order

Maintain named ranges

---

# Workbook Structure

```
Workbook

│

├── Report

├── Graph

├── Material Summary

├── Standard Summary

├── Acceptance Summary

├── Report Information

├── _Metadata

├── _Config

└── _Validation
```

---

# Worksheet Types

Visible

Report

Graph

Material Summary

Standard Summary

Acceptance Summary

Report Information

Hidden

_Metadata

_Config

_Validation

---

# Worksheet Naming Rules

Names shall

be unique

contain no illegal characters

remain stable

never change automatically

Maximum length

31 characters

---

# Worksheet Creation

When a report is generated

The Worksheet Manager verifies

Worksheet Exists

↓

No

↓

Create Worksheet

↓

Apply Template

↓

Apply Protection

↓

Continue

---

# Worksheet Update

Existing worksheets

shall be updated

without changing

Engineering Data

Named Ranges

Protection Rules

---

# Worksheet Deletion

Only temporary worksheets

may be deleted automatically.

Permanent report worksheets

shall never be deleted.

---

# Worksheet Protection

Protected

Engineering tables

Engineering graphs

Certificate number

Revision

Acceptance

Validation

Editable

Remarks

Customer Notes

Administrative Notes

---

# Worksheet Visibility

Visible

Report sheets

Hidden

Configuration sheets

Metadata sheets

Validation sheets

VeryHidden

Optional

Administrator configurable.

---

# Worksheet Order

Order is fixed.

Automatic reordering

is not permitted.

---

# Named Ranges

Required

Report_Header

Result_Table

Graph_Object

Material_Table

Acceptance_Table

Footer

Company_Logo

Certificate_Number

Revision

---

# Cell Protection

Locked Cells

Engineering data

Unlocked Cells

Remarks

Review notes

Customer notes

---

# Freeze Panes

Default

Enabled

For report readability.

---

# Print Areas

Each worksheet defines

its own print area.

Print areas are updated automatically.

---

# Graph Sheet

Contains

Validated charts only.

No engineering calculations.

No hidden construction graphics.

---

# Hidden Worksheets

_Metadata

Contains

Import file information

Machine information

Internal identifiers

_Config

Contains

Layout configuration

Fonts

Margins

Paper size

Validation

Contains

Validation status

Acceptance status

Release status

---

# Worksheet Recovery

If a worksheet is missing

↓

Recreate from template

↓

Restore named ranges

↓

Restore protection

---

# SQLite Database

Tables

```
tblWorksheet

tblWorksheetHistory

tblWorksheetConfiguration
```

---

# Audit Trail

Store

Worksheet

Operation

User

Timestamp

Computer Name

Software Version

---

# Permissions

Administrator

Create

Delete

Modify

Quality Manager

Modify Layout

Reviewer

Read

Operator

Use Only

---

# Error Handling

Worksheet Missing

↓

Recreate

Worksheet Protected

↓

Warning

Worksheet Corrupted

↓

Restore Template

Named Range Missing

↓

Rebuild

---

# Performance

Worksheet creation

shall complete

within

2 seconds

for standard reports.

---

# Acceptance Criteria

✔ Fixed worksheet structure

✔ Automatic worksheet recovery

✔ Protection preserved

✔ Named ranges preserved

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering data unchanged

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
