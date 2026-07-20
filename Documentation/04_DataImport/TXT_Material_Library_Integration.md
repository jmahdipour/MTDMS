# Material Library Integration

Document ID : MTDMS-IMP-021

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines how the TXT Import System communicates with the Material Library.

The Material Library is responsible for supplying engineering reference data.

The TXT Parser never stores material properties.

It only identifies the material.

---

# Architecture

TXT

↓

Material Name

↓

Material Library

↓

Engineering Properties

↓

Calculation Engine

---

# Objectives

Automatically identify material.

Load engineering constants.

Reduce operator errors.

Speed engineering calculations.

Maintain ISO 17025 traceability.

---

# Material Lookup Sequence

```
Read Header

↓

Extract Material Name

↓

Normalize Text

↓

Search SQLite

↓

Material Found

↓

Load Properties

↓

Engineering Ready
```

---

# If Material Not Found

Warning

↓

Operator Notification

↓

Manual Selection

↓

Continue

---

# Material Identification

Matching Priority

1

Material Code

↓

2

Standard Grade

↓

3

Commercial Name

↓

4

Alias

---

# Examples

```
ST37

↓

S235JR
```

```
AISI1045

↓

C45
```

```
1.2344

↓

H13
```

```
SS304

↓

AISI304
```

---

# Loaded Properties

Young's Modulus

Yield Strength

Ultimate Strength

Poisson Ratio

Density

Thermal Expansion

Hardness Range

Standard

Material Family

---

# Young's Modulus

Used for

Elastic Region Correction

Graph Correction

Yield Detection

Machine Verification

---

# Yield Strength

Used for

Expected Yield Search

Automatic Yield Window

Engineering Validation

---

# Ultimate Strength

Used for

Engineering Validation

Report Verification

Automatic Quality Checks

---

# Density

Future

Mass Calculation

Energy Calculation

Reserved

---

# Material Family

Examples

Carbon Steel

Low Alloy Steel

Tool Steel

Stainless Steel

Aluminium

Copper

Brass

Bronze

Cast Iron

Titanium

Plastic

Composite

---

# Material Library Database

SQLite Table

```
tblMaterials
```

---

# Required Fields

Material ID

Material Name

Alias

Standard

Young Modulus

Yield

UTS

Density

Poisson Ratio

Active

---

# Alias Table

SQLite

```
tblMaterialAlias
```

Example

```
ST37

↓

S235JR
```

```
DIN17100 ST37

↓

S235JR
```

---

# Material Confidence

100%

Exact Match

90%

Alias Match

70%

Partial Match

Below 70%

Operator Confirmation

---

# Engineering Lock

Engineering calculations

shall not begin

until

Material Status

=

Resolved

---

# Operator Override

Operator may

Select Material

from Ribbon

↓

Material Library

↓

Continue

Every override

is logged.

---

# Logging

Stores

Original Material Name

Matched Material

Match Type

Operator Override

Timestamp

---

# Future Features

AI Material Recognition

OCR Material Certificates

Automatic Chemical Analysis Matching

Reserved

---

# Acceptance Criteria

✔ Automatic material lookup

✔ Alias support

✔ SQLite compatible

✔ Engineering properties loaded automatically

✔ Ribbon override available

✔ Complete audit trail

---

End of Document
