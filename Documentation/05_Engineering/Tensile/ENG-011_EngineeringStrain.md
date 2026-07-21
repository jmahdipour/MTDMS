# Engineering Strain Calculation

Document ID : MTDMS-ENG-011

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

This document defines the calculation of Engineering Strain.

Engineering Strain represents the relative elongation of the specimen during loading.

Engineering Strain is calculated immediately after Engineering Stress.

Both values together generate the complete Engineering Stress–Strain Curve.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

Engineering Strain is the change in gauge length divided by the original gauge length.

The original gauge length remains constant throughout the calculation.

---

# Formula

Engineering Strain

ε

is calculated as

```
ε = ΔL / L₀
```

Where

ΔL

Extension measured by extensometer or crosshead

L₀

Original Gauge Length

---

# Variables

## Input

Original Gauge Length

Extension

Measurement Source

Extensometer

or

Crosshead

---

## Output

Engineering Strain

Dimensionless

---

# Internal Units

Extension

mm

Gauge Length

mm

Engineering Strain

mm/mm

---

# Display Units

Internally

```
mm/mm
```

Optional Display

%

Conversion

```
%

=

Engineering Strain × 100
```

---

# Measurement Priority

1

Extensometer

↓

2

Crosshead

↓

3

Manual Correction

---

# Extensometer Mode

If Extensometer

Available

Connected

Valid

↓

Use

Extension

Only

---

# Crosshead Mode

If Extensometer

Unavailable

↓

Crosshead displacement

Used

---

# Manual Correction

Operator

May enter

Final Gauge Length

After Fracture

Used

Only

For

Elongation After Fracture

Never modifies Engineering Strain curve.

---

# Example

Gauge Length

50 mm

Extension

0.125 mm

Engineering Strain

```
0.125 / 50

=

0.0025
```

Display

```
0.25 %
```

---

# Array Structure

Input

```
Extension(i)
```

Output

```
EngineeringStrain(i)
```

Array Length

Equals

Engineering Stress Array

---

# Validation

Gauge Length

>

0

Extension

Numeric

Engineering Strain

Finite

No NaN

No Overflow

---

# Error Conditions

Gauge Length = 0

↓

Abort Calculation

---

Gauge Length < 0

↓

Engineering Error

---

Extension Missing

↓

Abort Calculation

---

Overflow

↓

Abort

Rollback

---

# Noise Filtering

Optional

Small oscillations

May be filtered

Only

Before

Engineering calculations.

Filtering

Must never change

Original Raw Data.

---

# Storage

Engineering Strain

Stored in

```
tblEngineeringData
```

Field

```
EngineeringStrain
```

---

# Graph Usage

Engineering Strain

Used for

Engineering Stress–Strain Curve

Elastic Region Detection

Young's Modulus

Yield Point Detection

True Strain Calculation

---

# Precision

Internal

Double Precision

Display

Configurable

Default

6 Decimal Places

---

# Performance

Complexity

O(n)

One Division

Per Sample

---

# Acceptance Criteria

✔ Formula complies with ISO 6892-1

✔ Formula complies with ASTM E8/E8M

✔ Original gauge length always used

✔ Extensometer has priority

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Compatible with Graph Engine

---

End of Document
