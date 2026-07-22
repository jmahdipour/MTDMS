# Material Library

Document ID : MTDMS-DB-003

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

The Material Library stores reference engineering properties for materials used by MTDMS.

The library is a reference database only.

Engineering calculations are always performed from the imported TXT file.

Material Library values are never used to overwrite measured values.

---

# Objectives

The Material Library shall

• Store reference material properties

• Assist engineering analysis

• Assist graph correction

• Assist automatic yield search

• Support standards

• Support customer-defined materials

---

# Design Philosophy

Imported TXT

↓

Measured Values

↓

Engineering Calculations

↓

Material Library

↓

Reference Comparison Only

The Material Library never replaces measured values.

---

# Table Name

tblMaterialLibrary

---

# Primary Key

MaterialID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

MaterialID

INTEGER

----------------------------

MaterialCode

TEXT

Unique

----------------------------

MaterialName

TEXT

----------------------------

MaterialGroup

TEXT

Examples

Carbon Steel

Alloy Steel

Stainless Steel

Aluminium

Copper

Cast Iron

Brass

Bronze

Plastic

Composite

----------------------------

Standard

TEXT

----------------------------

StandardRevision

TEXT

----------------------------

Grade

TEXT

----------------------------

YoungModulus

REAL

MPa

----------------------------

YieldStrength_Min

REAL

MPa

----------------------------

YieldStrength_Max

REAL

MPa

----------------------------

UltimateStrength_Min

REAL

MPa

----------------------------

UltimateStrength_Max

REAL

MPa

----------------------------

Elongation_Min

REAL

%

----------------------------

Elongation_Max

REAL

%

----------------------------

ReductionArea_Min

REAL

%

----------------------------

ReductionArea_Max

REAL

%

----------------------------

Density

REAL

g/cm³

----------------------------

PoissonRatio

REAL

----------------------------

ThermalExpansion

REAL

----------------------------

Notes

TEXT

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

---

# Material Groups

Carbon Steel

Structural Steel

Tool Steel

Spring Steel

Stainless Steel

Heat Resistant Steel

Aluminium

Copper

Brass

Bronze

Titanium

Cast Iron

Plastic

Composite

Administrator configurable.

---

# Engineering Usage

Reference only

Used for

Young's Modulus estimation

Yield search window

Expected tensile range

Expected elongation

Automatic warnings

Graph correction support

---

# Automatic Yield Search

Example

Reference Yield

355 MPa

Search Window

±20%

↓

Search Interval

284 MPa

↓

426 MPa

The algorithm searches only inside this interval.

---

# Engineering Protection

Reference values

never overwrite

Measured Values

Measured Values always have priority.

---

# Customer Materials

Supported

Custom Material Code

Customer Grade

Customer Specification

Customer Notes

---

# SQLite Relationships

tblMaterialLibrary

↓

1 : N

tblReport

↓

1 : N

tblImportHistory

---

# Indexes

IX_MaterialCode

IX_Grade

IX_Standard

IX_Group

---

# Constraints

MaterialCode

UNIQUE

YoungModulus

> 0

Yield

>= 0

Ultimate

>= Yield

---

# Audit Trail

Record

Material

Modification

User

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Create

Modify

Delete

Quality Manager

Approve

Reviewer

Read

Operator

Read Only

---

# Error Handling

Duplicate Material

↓

Reject

Missing Grade

↓

Warning

Invalid Modulus

↓

Reject

Missing Standard

↓

Warning

---

# Acceptance Criteria

✔ Reference database only

✔ Never modifies measured values

✔ Supports graph correction

✔ Supports automatic yield search

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
