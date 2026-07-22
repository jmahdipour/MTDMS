# Standard Library

Document ID : MTDMS-DB-007

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

The Standard Library stores the standards supported by MTDMS and the engineering properties required for each standard.

The library is a reference database only.

It does not perform engineering calculations.

It does not determine PASS or FAIL.

It defines what shall be reported.

---

# Objectives

The Standard Library shall

• Store standards

• Store revisions

• Define required engineering properties

• Define optional engineering properties

• Support laboratory-specific standards

• Support customer-specific standards

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Validation

↓

Standard Library

↓

Reference Only

The Standard Library never changes measured values.

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

Unique

Examples

ISO 6892-1

ISO 630

ISO 898

INSO 3132

ASTM E8/E8M

ISO 6508

ISO 6507

ISO 148

----------------------------

Title

TEXT

----------------------------

Revision

TEXT

----------------------------

PublicationYear

INTEGER

----------------------------

Category

TEXT

Examples

Tensile

Compression

Hardness

Impact

Chemical Analysis

Spring

Ring Stiffness

Custom

----------------------------

MaterialFamily

TEXT

Examples

Steel

Aluminium

Copper

Plastic

Composite

General

----------------------------

Description

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

# Table Name

tblStandardProperty

Purpose

Defines which engineering properties belong to each standard.

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

StandardID

INTEGER

Foreign Key

----------------------------

PropertyName

TEXT

Examples

Yield Strength

Ultimate Strength

Young's Modulus

Elongation

Reduction of Area

Maximum Force

Impact Energy

Hardness

Chemical Composition

----------------------------

EngineeringSymbol

TEXT

Examples

ReH

Rp0.2

Rm

E

A

Z

----------------------------

Unit

TEXT

MPa

GPa

%

J

HRC

HBW

HV

ppm

----------------------------

Mandatory

BOOLEAN

----------------------------

DisplayOrder

INTEGER

----------------------------

VisibleInReport

BOOLEAN

---

# Engineering Independence

The Standard Library

defines

report structure only.

It never

changes

engineering calculations.

---

# Custom Standards

Supported

Each custom standard may define

Required properties

Display order

Units

Report notes

Acceptance profile reference

---

# Standard Categories

Mechanical

Chemical

Physical

Dimensional

Customer

Internal Laboratory

---

# SQLite Relationships

tblStandard

↓

1 : N

tblStandardProperty

↓

1 : N

tblReport

↓

1 : N

tblMaterialLibrary

---

# Indexes

IX_StandardCode

IX_Category

IX_MaterialFamily

IX_Revision

---

# Constraints

StandardCode

UNIQUE

Revision

Required

Category

Required

---

# Audit Trail

Store

Standard

Revision

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

Duplicate Standard

↓

Reject

Missing Revision

↓

Reject

Missing Property

↓

Warning

Inactive Standard

↓

Hidden

---

# Acceptance Criteria

✔ Standard definitions stored

✔ Property definitions stored

✔ Supports custom standards

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
