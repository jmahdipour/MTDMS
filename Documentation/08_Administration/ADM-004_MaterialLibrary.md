# Material Library

Document ID : MTDMS-ADM-004

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

The Material Library is the engineering knowledge base of MTDMS.

It stores all material properties required for automatic calculations, report generation, acceptance evaluation and graph correction.

All engineering modules shall retrieve material information exclusively from this library.

The Material Library shall never directly modify test results.

---

# Reference Standards

ISO 17025

ISO 6892-1

ISO 630

ISO 898

ASTM E8

ASTM E111

ASTM A370

INSO 3132

---

# Objectives

The Material Library shall

• Store engineering properties

• Support multiple standards

• Maintain revision history

• Support customer-specific materials

• Supply engineering calculations

• Supply acceptance limits

• Support multilingual names

---

# Architecture

```
Material Library

↓

Material Grade

↓

Mechanical Properties

↓

Chemical Properties

↓

Acceptance Rules

↓

Engineering Modules
```

---

# Material Categories

Carbon Steel

Low Alloy Steel

Tool Steel

Spring Steel

Stainless Steel

Cast Iron

Aluminium

Copper

Brass

Bronze

Titanium

Nickel Alloy

Plastic

Composite

Custom

---

# Material Identification

Each material contains

Material ID

Material Name

Material Grade

Material Standard

Revision

Status

Manufacturer

Customer

Optional

---

# Mechanical Properties

Young's Modulus

Poisson Ratio

Density

Yield Strength

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Rt0.5

Ultimate Tensile Strength

Elongation

Reduction of Area

Hardness

Fatigue Limit

Fracture Toughness

Thermal Expansion

Optional

---

# Physical Properties

Density

Melting Point

Thermal Conductivity

Electrical Conductivity

Specific Heat

Magnetic Property

Optional

---

# Chemical Composition

Supported Elements

C

Si

Mn

P

S

Cr

Ni

Mo

Cu

Al

Ti

Nb

V

Co

W

Pb

Sn

Zn

Fe

Balance

Administrator configurable.

---

# Acceptance Limits

Each material may contain

Minimum

Maximum

Target

Tolerance

Engineering Notes

Acceptance Method

---

# Engineering Usage

The Material Library supplies

Young's Modulus

↓

Graph Correction

Yield Range

↓

Yield Detection

Acceptance Limits

↓

PASS / FAIL

Density

↓

Mass Calculations

Poisson Ratio

↓

Future FEA Export

---

# Multiple Standards

One material may belong to

ISO

ASTM

DIN

JIS

BS

INSO

Customer Standard

Custom

---

# Revision Control

Each material maintains

Version

Revision

Created By

Modified By

Approval Status

Effective Date

Old revisions remain archived.

---

# Material Status

Draft

Approved

Obsolete

Archived

Under Review

---

# Search Methods

Material Name

Material Grade

Standard

Keyword

Customer Code

Material ID

---

# Import

Supported

Excel

CSV

SQLite

Future

XML

JSON

ERP

---

# Export

Excel

CSV

SQLite

PDF Summary

Future

XML

JSON

---

# Database

SQLite

Tables

```
tblMaterial

tblMaterialProperty

tblMaterialChemical

tblMaterialRevision

tblMaterialStandard
```

---

# Permissions

Administrator

Full Access

Engineering Manager

Approve

Operator

Read Only

Reviewer

Read Only

---

# Audit Trail

Every modification records

User

Date

Time

Old Value

New Value

Reason

Computer Name

---

# Validation Rules

Material Name

Required

Grade

Required

Standard

Required

Young's Modulus

Required

Duplicate Grades

Not Allowed

unless

different standard.

---

# Error Handling

Duplicate Material

↓

Reject

Missing Standard

↓

Reject

Missing Young's Modulus

↓

Warning

Corrupted Record

↓

Restore Previous Revision

---

# Future Enhancements

Automatic Grade Identification

AI Material Recommendation

Customer Material Packages

ERP Synchronization

Cloud Library

Reserved

---

# Acceptance Criteria

✔ Supports multiple standards

✔ Revision controlled

✔ Engineering calculations supported

✔ Chemical composition supported

✔ Acceptance limits supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 17025 traceability

---

End of Document
