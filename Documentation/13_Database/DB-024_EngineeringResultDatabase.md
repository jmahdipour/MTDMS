# Engineering Result Database

Document ID : MTDMS-DB-024

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

The Engineering Result Database stores the final calculated engineering values extracted from the imported TXT file.

Only final engineering results are stored.

Raw measurement points remain inside the imported TXT file.

Engineering calculations are always regenerated from the TXT file whenever required.

---

# Objectives

The Engineering Result Database shall

• Store final calculated values

• Preserve calculation traceability

• Support report generation

• Support report searching

• Preserve engineering history

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Final Engineering Results

↓

SQLite

↓

Report

SQLite stores the calculated summary only.

The TXT file remains the engineering source.

---

# Table Name

tblEngineeringResult

---

# Primary Key

ResultID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ResultID

INTEGER

----------------------------

ImportID

INTEGER

Foreign Key

tblImportHistory

----------------------------

ReportID

INTEGER

Nullable

Foreign Key

tblReport

----------------------------

MaterialID

INTEGER

Nullable

----------------------------

StandardID

INTEGER

Nullable

----------------------------

ResultType

TEXT

Examples

Tensile

Compression

Bending

Spring

Ring Stiffness

Custom

----------------------------

YieldStrength

REAL

Nullable

----------------------------

UltimateStrength

REAL

Nullable

----------------------------

YoungModulus

REAL

Nullable

----------------------------

Elongation

REAL

Nullable

----------------------------

ReductionOfArea

REAL

Nullable

----------------------------

MaximumForce

REAL

Nullable

----------------------------

MaximumDisplacement

REAL

Nullable

----------------------------

MaximumStrain

REAL

Nullable

----------------------------

FractureForce

REAL

Nullable

----------------------------

FractureDisplacement

REAL

Nullable

----------------------------

EngineeringStatus

TEXT

Examples

Calculated

Validated

Approved

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

# Stored Results

Only calculated engineering values.

Examples

Yield Strength

Ultimate Strength

Young's Modulus

Elongation

Maximum Force

Maximum Displacement

Maximum Strain

Fracture Values

Additional results may be added for future test types.

---

# Raw Data

Raw engineering data

is never stored

inside this table.

All raw data

remains

inside the imported TXT file.

---

# Engineering Independence

Engineering Result Database

stores

results only.

Recalculation

always starts

from

the imported TXT file.

---

# SQLite Relationships

tblEngineeringResult

↓

N : 1

tblImportHistory

↓

1 : N

tblReport

↓

1 : N

tblValidation

---

# Indexes

IX_ImportID

IX_ReportID

IX_ResultType

IX_EngineeringStatus

---

# Constraints

ImportID

Required

ResultType

Required

---

# Audit Trail

Store

Calculation

Operator

Timestamp

Software Version

Computer Name

Result Status

---

# Permissions

Administrator

Modify

Quality Manager

Approve

Reviewer

Read

Operator

Read

Calculation Only

---

# Error Handling

Missing TXT

↓

Abort

Missing Import Record

↓

Abort

Calculation Failure

↓

Reject

Validation Failure

↓

Warning

---

# Acceptance Criteria

✔ Final engineering results stored

✔ Linked to imported TXT

✔ No raw data duplication

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Recalculation always uses TXT

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
