# True Stress Calculation

Document ID : MTDMS-ENG-012

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Engineering → Tensile

Status

Production

---

# Purpose

This document defines the calculation of True Stress according to ISO 6892-1.

True Stress represents the actual stress acting on the continuously reducing cross-sectional area of the specimen.

Unlike Engineering Stress, True Stress considers the instantaneous geometry of the specimen.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

Engineering Stress assumes

Original Area

True Stress assumes

Instantaneous Area

Therefore

True Stress is always greater than or equal to Engineering Stress until necking behavior dominates.

---

# Mathematical Definition

General Definition

```
σ_true = F / A_i
```

Where

F

Applied Force

Ai

Instantaneous Area

---

# Practical Formula

Before necking

Assuming constant volume

```
σ_true = σ_engineering (1 + ε_engineering)
```

Where

σ_engineering

Engineering Stress

ε_engineering

Engineering Strain

---

# Necking Region

After necking begins

The previous equation is no longer sufficiently accurate.

Possible methods

Method A

Bridgman Correction

Method B

Instantaneous Measured Diameter

Method C

Digital Image Correlation

Current Version

Method A

Until Necking

Only

---

# Calculation Sequence

Engineering Stress

↓

Engineering Strain

↓

True Stress

↓

True Strain

---

# Variables

Input

Engineering Stress

Engineering Strain

Output

True Stress

---

# Internal Units

Engineering Stress

MPa

Engineering Strain

mm/mm

True Stress

MPa

---

# Example

Engineering Stress

500 MPa

Engineering Strain

0.20

```
σ_true

=

500 × (1 + 0.20)

=

600 MPa
```

---

# Validation Rules

Engineering Stress

≥ 0

Engineering Strain

≥ 0

True Stress

≥ Engineering Stress

---

# Data Type

Double Precision

---

# Array Structure

Input

```
EngineeringStress(i)

EngineeringStrain(i)
```

Output

```
TrueStress(i)
```

Array Length

Equals

Imported Sample Count

---

# Fracture Handling

True Stress

Calculated

Only

Until

Fracture Index

No values shall exist

After fracture.

---

# Error Conditions

Engineering Stress Missing

↓

Abort

Engineering Strain Missing

↓

Abort

Overflow

↓

Abort

Rollback Engineering

---

# Graph Usage

True Stress Curve

Used for

Plastic Region Analysis

True Stress–True Strain Graph

Material Modeling

Work Hardening Analysis

---

# Database Storage

SQLite

Table

```
tblEngineeringData
```

Field

```
TrueStress
```

---

# Precision

Internal

Double

Display

Default

2 Decimal Places

---

# Future Enhancements

Bridgman Correction

Instantaneous Area Measurement

Laser Diameter Measurement

Digital Image Correlation

Finite Element Correction

Reserved

---

# Acceptance Criteria

✔ Formula complies with ISO 6892-1

✔ Uses Engineering Stress and Engineering Strain

✔ Stops at fracture

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Compatible with Graph Engine

---

End of Document
