# Unit Database

Document ID : MTDMS-DB-028

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

The Unit Database defines all engineering units used by MTDMS.

It provides a single source for unit names, symbols, and conversion factors.

It does not perform engineering calculations.

It only supplies unit definitions.

---

# Objectives

The Unit Database shall

• Store engineering units

• Support unit conversion

• Standardize report units

• Support graph labeling

• Eliminate inconsistent unit usage

---

# Design Philosophy

TXT File

↓

Imported Values

↓

Engineering Calculation

↓

Selected Units

↓

Report

Engineering calculations use the imported values.

Units affect only presentation and conversion where explicitly required.

---

# Table Name

tblUnit

---

# Primary Key

UnitID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

UnitID

INTEGER

----------------------------

QuantityType

TEXT

Examples

Force

Stress

Strain

Length

Time

Energy

Hardness

Angle

Temperature

Mass

----------------------------

UnitName

TEXT

Examples

Newton

MegaPascal

Millimeter

Second

Kilogram-force

----------------------------

Symbol

TEXT

Examples

N

kN

kgf

MPa

GPa

mm

cm

m

%

s

J

°C

----------------------------

SIUnit

BOOLEAN

----------------------------

ConversionFactorToSI

REAL

----------------------------

DecimalPlaces

INTEGER

----------------------------

VisibleInReports

BOOLEAN

----------------------------

VisibleOnGraphs

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

# Supported Quantity Types

Force

Stress

Strain

Length

Displacement

Extension

Time

Energy

Mass

Temperature

Angle

Hardness

Pressure

Administrator configurable.

---

# Typical Units

Force

N

kN

kgf

----------------------------

Stress

MPa

GPa

----------------------------

Length

mm

cm

m

----------------------------

Strain

%

mm/mm

----------------------------

Time

ms

s

min

----------------------------

Energy

J

kJ

----------------------------

Temperature

°C

K

---

# Report Usage

Reports shall display

the unit defined

for each engineering quantity.

---

# Graph Usage

Axis titles

shall automatically include

the corresponding engineering unit.

Example

Stress (MPa)

Strain (%)

Force (kN)

Displacement (mm)

---

# Engineering Independence

Unit definitions

shall never modify

Imported TXT

Engineering Results

Engineering Tables

Validation Results

---

# SQLite Relationships

tblUnit

↓

Referenced by

Calculation Engine

Graph Engine

Report Engine

Export Engine

---

# Indexes

IX_QuantityType

IX_Symbol

IX_UnitName

---

# Constraints

QuantityType

Required

Symbol

Required

ConversionFactorToSI

Required

---

# Audit Trail

Store

Unit

Old Value

New Value

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

Unknown Unit

↓

Reject

Duplicate Symbol

↓

Reject

Invalid Conversion Factor

↓

Reject

Inactive Unit

↓

Hidden from selection

---

# Acceptance Criteria

✔ Central unit management

✔ SI conversion support

✔ Graph labels supported

✔ Report labels supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
