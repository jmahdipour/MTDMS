# True Strain Calculation

Document ID : MTDMS-ENG-013

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

This document defines the calculation of True Strain according to ISO 6892-1.

True Strain represents the actual incremental deformation of the specimen during loading.

Unlike Engineering Strain, True Strain considers the continuously changing gauge length during deformation.

True Strain is required for:

• Plastic deformation analysis

• Flow stress curves

• Material modelling

• Finite Element Analysis

• Hardening law determination

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

Engineering Strain

assumes

Original Gauge Length

True Strain

uses

Instantaneous Gauge Length

Therefore

True Strain represents the accumulated logarithmic deformation.

---

# Mathematical Definition

General Definition

```
εtrue = ln(L / L0)
```

Where

L

Current Gauge Length

L0

Original Gauge Length

---

# Practical Formula

Using Engineering Strain

```
εtrue = ln(1 + εengineering)
```

Where

εengineering

Engineering Strain

---

# Calculation Sequence

Engineering Strain

↓

True Strain

↓

True Stress

↓

Plastic Analysis

---

# Variables

Input

Engineering Strain

Output

True Strain

---

# Units

Engineering Strain

mm/mm

True Strain

Dimensionless

---

# Example

Engineering Strain

0.200

```
εtrue

=

ln(1.20)

=

0.18232156
```

---

# Data Range

Elastic Region

Engineering

≈

True

Plastic Region

Difference increases

Large Deformation

Difference becomes significant

---

# Validation Rules

Engineering Strain

≥ 0

True Strain

≥ 0

True Strain

≤ Engineering Strain

(for positive tensile strain)

---

# Necking

Before Necking

Formula

Fully Valid

After Necking

Requires

Local Measurement

Current Version

Stops at Fracture

No post-fracture values calculated.

---

# Array Structure

Input

```
EngineeringStrain(i)
```

Output

```
TrueStrain(i)
```

Array Length

Equals

Engineering Stress Array

---

# Data Type

Double Precision

IEEE-754 Double

---

# Numerical Stability

When

Engineering Strain

≈ 0

Calculation uses

```
Log(1+x)
```

to improve numerical stability.

Very small values

(<1E-12)

treated as

Zero.

---

# Error Conditions

Engineering Strain Missing

↓

Abort

Engineering Strain < -1

↓

Impossible

↓

Engineering Error

NaN

↓

Abort

Overflow

↓

Abort

Rollback

---

# Database Storage

SQLite

Table

```
tblEngineeringData
```

Field

```
TrueStrain
```

---

# Graph Usage

True Strain is used for

True Stress–True Strain Curve

Plastic Region

Hardening Analysis

Flow Curve

Material Modelling

---

# Precision

Internal

Double Precision

Display

Default

6 Decimal Places

---

# Future Enhancements

True Local Strain

Digital Image Correlation

Laser Extensometer

Necking Compensation

Large Plastic Deformation

Reserved

---

# Acceptance Criteria

✔ Formula complies with ISO 6892-1

✔ Uses logarithmic definition

✔ Double precision

✔ Numerically stable near zero

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Compatible with Graph Engine

---

End of Document
