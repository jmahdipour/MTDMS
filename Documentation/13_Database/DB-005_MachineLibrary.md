# Machine Library

Document ID : MTDMS-DB-005

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

The Machine Library stores configuration information for every testing machine supported by MTDMS.

This library contains machine metadata only.

Engineering data is always obtained from the imported TXT file.

Machine Library values shall never replace values contained in the imported TXT file.

---

# Objectives

The Machine Library shall

• Identify testing machines

• Store machine configuration

• Store supported test types

• Store machine capabilities

• Support calibration traceability

---

# Design Philosophy

Testing Machine

↓

TXT Export

↓

Excel Import

↓

Engineering Calculation

↓

Machine Library

↓

Reference Only

Machine Library never modifies imported engineering data.

---

# Table Name

tblMachine

---

# Primary Key

MachineID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

MachineID

INTEGER

----------------------------

MachineCode

TEXT

Unique

----------------------------

MachineName

TEXT

----------------------------

Manufacturer

TEXT

----------------------------

Model

TEXT

----------------------------

SerialNumber

TEXT

----------------------------

LaboratoryCode

TEXT

Nullable

----------------------------

Department

TEXT

Nullable

----------------------------

MachineType

TEXT

Examples

Universal Testing Machine

Compression Machine

Hardness Tester

Impact Tester

Spring Tester

Ring Stiffness Tester

Custom

----------------------------

SupportedTest

TEXT

Examples

Tensile

Compression

Bending

Spring

Ring Stiffness

Impact

Administrator configurable.

----------------------------

TXTFormatVersion

TEXT

----------------------------

MaximumForce

REAL

----------------------------

ForceUnit

TEXT

----------------------------

DisplacementUnit

TEXT

----------------------------

StrainUnit

TEXT

----------------------------

SoftwareVersion

TEXT

Nullable

----------------------------

CommunicationType

TEXT

Examples

TXT Export Only

----------------------------

CalibrationCertificate

TEXT

Nullable

----------------------------

CalibrationDate

DATE

----------------------------

NextCalibration

DATE

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

# Supported Machine Types

Universal Testing Machine

Hardness Tester

Impact Tester

Spring Tester

Ring Stiffness Tester

Future Machines

Administrator configurable.

---

# Engineering Independence

Machine Library

shall never

modify

Imported TXT

Engineering Results

Calculated Results

Graphs

Validation

---

# TXT Compatibility

Each machine

may define

TXT format version

Delimiter

Decimal separator

Encoding

Header structure

Only for parsing support.

Never for engineering correction.

---

# Calibration Information

Reference only.

Displays

Calibration Date

Calibration Certificate

Next Calibration

Calibration Laboratory

---

# SQLite Relationships

tblMachine

↓

1 : N

tblImportHistory

↓

1 : N

tblCalibrationHistory

↓

1 : N

tblReport

---

# Indexes

IX_MachineCode

IX_Model

IX_SerialNumber

IX_MachineType

---

# Constraints

MachineCode

UNIQUE

MachineName

Required

Model

Required

---

# Audit Trail

Store

Machine

Modification

Operator

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

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Duplicate MachineCode

↓

Reject

Missing MachineName

↓

Reject

Missing Calibration Date

↓

Warning

Unknown TXT Version

↓

Warning

---

# Acceptance Criteria

✔ Machine information stored

✔ TXT format reference stored

✔ Calibration reference stored

✔ Engineering calculations unaffected

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
