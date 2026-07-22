# Standard Database

Document ID : MTDMS-DB-027

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

The Standard Database stores all engineering standards supported by MTDMS.

The database defines

test methods

acceptance criteria

calculation methods

report references

It never performs calculations.

It only provides reference information.

---

# Objectives

The Standard Database shall

• Store engineering standards

• Classify test methods

• Support automatic report generation

• Support material comparison

• Support validation

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Selected Standard

↓

Validation

↓

Report

The engineering calculations originate from the TXT file.

The standard only defines the engineering rules.

---

# Table Name

tblStandard

---

# Primary Key

StandardID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

StandardID

INTEGER

----------------------------

StandardCode

TEXT

Examples

ISO 6892-1

ISO 6508

ISO 6507

ISO 148-1

ASTM E8

ASTM A370

INSO 3132

----------------------------

Title

TEXT

----------------------------

Category

TEXT

Examples

Tensile

Compression

Bending

Hardness

Impact

Spring

Ring Stiffness

Custom

----------------------------

Version

TEXT

----------------------------

RevisionDate

DATE

----------------------------

Organization

TEXT

Examples

ISO

ASTM

INSO

DIN

EN

----------------------------

CalculationProfile

TEXT

Reference only

----------------------------

ReportTemplateID

INTEGER

Nullable

----------------------------

MaterialGroup

TEXT

Nullable

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

# Categories

Mechanical Testing

Hardness

Impact

Spring

Pipe Testing

Plastic Testing

Custom Tests

Administrator configurable.

---

# Supported Standards

Examples

ISO 6892-1

ISO 7500-1

ISO 6508

ISO 6507

ISO 6506

ISO 148-1

ASTM E8

ASTM A370

ASTM E111

ASTM D732

ASTM D1894

INSO 3132

Additional standards

may be added

without changing database structure.

---

# Usage

The selected standard determines

Calculation profile

Validation profile

Report format

Acceptance limits

Reference material properties

---

# Engineering Independence

The Standard Database

never modifies

Engineering Results

Imported TXT

Engineering Tables

Graph Data

It only supplies reference information.

---

# SQLite Relationships

tblStandard

↓

N : 1

tblMaterialProperty

↓

N : 1

tblMaterialLibrary

↓

N : 1

tblReport

↓

N : 1

tblValidation

↓

N : 1

tblTemplate

---

# Indexes

IX_StandardCode

IX_Category

IX_Organization

---

# Constraints

StandardCode

UNIQUE

Category

Required

Organization

Required

---

# Audit Trail

Store

Standard

Version

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

Missing Standard

↓

Abort Validation

Inactive Standard

↓

Warning

Duplicate Code

↓

Reject

Unknown Category

↓

Reject

---

# Acceptance Criteria

✔ Standards centrally managed

✔ Multiple organizations supported

✔ Report linkage supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
