# Standard Library

Document ID : MTDMS-ADM-007

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Administration

Status

Production

---

# Purpose

The Standard Library is the central repository for all engineering, testing, calibration and reporting standards used by MTDMS.

It ensures that calculations, acceptance criteria, reports and procedures always reference controlled and approved standard revisions.

The Standard Library does **not** perform engineering calculations.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 6892-1

ISO 7500-1

ISO 9513

ISO 376

ISO 148-1

ISO 6506

ISO 6507

ISO 6508

ASTM E8/E8M

ASTM E4

ASTM E74

ASTM E23

ASTM E10

ASTM E18

ASTM E92

ASTM E384

INSO 3132

ISO 630

ISO 898

---

# Objectives

The Standard Library shall

• Maintain approved standards

• Track revisions

• Associate standards with test methods

• Store acceptance rules

• Support multilingual titles

• Maintain historical versions

---

# Architecture

```
Standard Library

↓

Standard Family

↓

Revision

↓

Acceptance Rules

↓

Engineering Modules

↓

Reports
```

---

# Supported Standard Families

ISO

ASTM

DIN

EN

JIS

BS

INSO

API

ASME

Customer Standards

Internal Procedures

---

# Standard Information

Standard ID

Standard Number

Title

Organization

Revision

Edition

Publication Date

Status

Language

Category

---

# Categories

Mechanical Testing

Chemical Analysis

Calibration

Hardness

Impact

Dimensional Inspection

Coating

Welding

Metallography

General Laboratory

Quality Management

---

# Status

Draft

Approved

Superseded

Archived

Withdrawn

---

# Engineering Associations

Each standard may define

Test Method

Required Parameters

Calculation Rules

Acceptance Rules

Required Graph

Required Report

Measurement Units

---

# Acceptance Rules

Each standard may contain

Minimum Value

Maximum Value

Tolerance

Decision Rule

Pass/Fail Logic

Notes

These values are referenced by

Material Library

Engineering Engine

Report Engine

---

# Required Parameters

Example

ISO 6892-1

requires

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Gauge Length

Test Speed

---

# Revision Control

Every standard maintains

Revision Number

Issue Date

Effective Date

Approval Status

Approved By

Previous Revision

Old revisions remain available for historical reports.

---

# Cross References

A standard may reference

Another Standard

Laboratory Procedure

Customer Specification

Material Library

Calibration Procedure

---

# Search

By

Standard Number

Title

Organization

Category

Revision

Keyword

Status

---

# Import

Supported

Excel

CSV

SQLite

Future

XML

JSON

Official Standard Database

---

# Export

Excel

CSV

PDF Summary

SQLite

---

# Database

SQLite

Tables

```
tblStandard

tblStandardRevision

tblStandardCategory

tblStandardRequirement

tblStandardAcceptance
```

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Engineering Manager

Modify Draft

Operator

Read Only

Reviewer

Read Only

---

# Audit Trail

Every modification records

User

Timestamp

Old Revision

New Revision

Reason

Computer Name

---

# Validation Rules

Standard Number

Required

Revision

Required

Duplicate Revision

Not Allowed

Approved Standard

Cannot Be Edited

---

# Error Handling

Duplicate Standard

↓

Reject

Missing Revision

↓

Reject

Corrupted Record

↓

Restore Previous Revision

Missing Category

↓

Warning

---

# Future Enhancements

Automatic Standards Update

Online Standards Repository

Customer Standard Packages

AI Standard Recommendation

Reserved

---

# Acceptance Criteria

✔ Supports multiple standard organizations

✔ Revision controlled

✔ Acceptance rules stored

✔ Historical revisions preserved

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Engineering independent

---

End of Document
