# Engineering Stress Calculation

Document ID : MTDMS-ENG-010

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

This document defines the calculation of Engineering Stress.

Engineering Stress is the first engineering quantity calculated after the geometry of the specimen has been validated.

All subsequent tensile calculations depend on Engineering Stress.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

ISO 7500-1

---

# Definition

Engineering Stress is the applied force divided by the original cross-sectional area.

The original area never changes during the calculation.

---

# Formula

Engineering Stress

σ

is calculated as

```
σ = F / A₀
```

Where

F

Applied Force

A₀

Original Cross-sectional Area

---

# Variables

## Input

Force

Original Area

Units

Detected by Import Engine

---

## Output

Engineering Stress

Unit

MPa

---

# Internal Units

Force

Newton

Area

mm²

Stress

MPa

---

# Unit Relationship

Because

```
1 MPa = 1 N/mm²
```

No additional scaling is required.

---

# Calculation Sequence

Geometry Validation

↓

Area Calculation

↓

Force Validation

↓

Engineering Stress

↓

Engineering Strain

---

# Requirements

Area

Must be greater than zero.

Force

Must be numeric.

Negative force values

Allowed

Compression

Only if test type supports compression.

---

# Round Specimen

Original Area

```
A₀ = π d² / 4
```

Where

d

Original Diameter

---

# Flat Specimen

Original Area

```
A₀ = b × t
```

Where

b

Width

t

Thickness

---

# Pipe

Area

Calculated by

Pipe Geometry Module

Engineering Stress always uses

Original Pipe Area

---

# Example

Force

125000 N

Area

250 mm²

Engineering Stress

```
125000 / 250

=

500 MPa
```

---

# Data Type

Double Precision

---

# Array Structure

Input

```
Force(i)
```

Output

```
EngineeringStress(i)
```

Array Length

Equals

Imported Sample Count

---

# Validation

Area

>

0

Force

Numeric

Stress

Finite

No NaN

No Overflow

---

# Error Conditions

Area = 0

↓

Abort Calculation

---

Area < 0

↓

Engineering Error

---

Force Missing

↓

Calculation Stopped

---

Overflow

↓

Abort

Rollback

---

# Storage

Engineering Stress

Stored in

```
tblEngineeringData
```

Field

```
EngineeringStress
```

---

# Graph Usage

Engineering Stress

Used for

Stress-Strain Graph

Elastic Region

Yield Detection

UTS Detection

True Stress

---

# Precision

Internal

Double

Displayed

Configurable

Default

2 Decimal Places

---

# Performance

Calculation Complexity

O(n)

One Division

Per Sample

---

# Acceptance Criteria

✔ Formula complies with ISO 6892-1

✔ Formula complies with ASTM E8/E8M

✔ Uses original area only

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Compatible with Graph Engine

---

End of Document
