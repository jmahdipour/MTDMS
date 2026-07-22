# Material Property Database

Document ID : MTDMS-DB-026

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

The Material Property Database stores reference engineering properties used only as comparison values during evaluation and graph correction.

These values are **reference data only**.

They never replace measured values extracted from the TXT file.

They never modify engineering calculations.

---

# Objectives

The Material Property Database shall

• Store reference material properties

• Support automatic material identification

• Support graph correction

• Support engineering comparison

• Support report generation

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Measured Results

↓

Material Property Library

↓

Comparison Only

Measured engineering values always have priority.

---

# Table Name

tblMaterialProperty

---

# Primary Key

PropertyID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

PropertyID

INTEGER

----------------------------

MaterialID

INTEGER

Foreign Key

tblMaterialLibrary

----------------------------

StandardID

INTEGER

Nullable

----------------------------

Grade

TEXT

Examples

ST37

ST52

CK45

A36

304

316

4140

1.2344

----------------------------

YoungModulus

REAL

GPa

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

ReductionArea_Min

REAL

%

Nullable

----------------------------

Density

REAL

kg/m³

Nullable

----------------------------

PoissonRatio

REAL

Nullable

----------------------------

ReferenceSource

TEXT

Examples

ISO

ASTM

INSO

Manufacturer

Laboratory

----------------------------

Revision

TEXT

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

# Usage

Reference values are used for

Material identification

Engineering comparison

Graph correction

Automatic validation

Report reference

---

# Graph Correction

The reference Young's modulus

may be used

to correct

the graphical elastic region.

It shall never modify

the engineering calculations

derived from the TXT file.

---

# Material Identification

Automatic identification

may compare

Measured Yield

Measured Ultimate Strength

Measured Young's Modulus

with

Reference Ranges

and suggest

possible material grades.

Operator confirmation is always required.

---

# Engineering Independence

Reference properties

shall never overwrite

Measured Results

Engineering Tables

Imported TXT

Validation Results

---

# SQLite Relationships

tblMaterialProperty

↓

N : 1

tblMaterialLibrary

↓

N : 1

tblStandard

↓

Referenced by

Calculation Engine

Validation Engine

Graph Engine

---

# Indexes

IX_MaterialID

IX_Grade

IX_StandardID

IX_YoungModulus

---

# Constraints

MaterialID

Required

Grade

Required

YoungModulus

Required

---

# Audit Trail

Store

Material

Property

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

Missing Property

↓

Ignore

Missing Young's Modulus

↓

Graph correction unavailable

Invalid Range

↓

Reject

Duplicate Grade

↓

Reject

---

# Acceptance Criteria

✔ Reference material properties stored

✔ Material comparison supported

✔ Graph correction supported

✔ Measured data always preserved

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
