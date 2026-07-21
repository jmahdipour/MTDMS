# True Fracture Strain Calculation

Document ID : MTDMS-ENG-025

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

This document defines the calculation of True Fracture Strain.

True Fracture Strain represents the logarithmic plastic deformation of the specimen at the moment of fracture.

Unlike Engineering Elongation, it is calculated from the reduction in cross-sectional area and therefore represents the local strain in the necked region.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

True Fracture Strain is calculated from the ratio of the original cross-sectional area to the final cross-sectional area.

It assumes plastic deformation occurs under approximately constant volume.

---

# Mathematical Formula

```
εTF = ln(A₀ / Af)
```

Where

εTF

True Fracture Strain

A₀

Original Area

Af

Final Minimum Area

---

# Assumption

The calculation assumes

```
Volume Before Necking

≈

Volume After Necking
```

This assumption is valid for most metallic materials undergoing plastic deformation.

---

# Variables

Input

Original Area

Final Area

Output

True Fracture Strain

---

# Round Specimen

Original Area

```
A₀ = π d₀² / 4
```

Final Area

```
Af = π df² / 4
```

---

# Flat Specimen

Original Area

```
A₀ = b₀ × t₀
```

Final Area

```
Af = bf × tf
```

---

# Pipe Specimen

Area determined by

Pipe Geometry Module

---

# Calculation Sequence

Geometry

↓

Original Area

↓

Fracture Measurement

↓

Final Area

↓

True Fracture Strain

↓

Report

---

# Example

Original Area

250 mm²

Final Area

100 mm²

```
εTF

=

ln(250 / 100)

=

ln(2.5)

=

0.916291
```

---

# Validation

```
A₀ > 0
```

```
Af > 0
```

```
Af < A₀
```

---

# Engineering Relationship

Normally

```
True Fracture Strain

>

Engineering Fracture Strain
```

because logarithmic strain accounts for continuous deformation.

---

# Error Conditions

Final Area Missing

↓

Abort

Original Area Missing

↓

Abort

Area ≤ 0

↓

Engineering Error

Final Area > Original Area

↓

Invalid Measurement

Overflow

↓

Abort

Rollback

---

# Database Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

```
OriginalArea

FinalArea

TrueFractureStrain
```

---

# Graph Usage

True Fracture Strain

shall not extend the engineering curve.

It is reported as

a terminal material property

only.

---

# Report

Certificate Displays

Original Area

Final Area

True Fracture Strain

Calculation Formula

Measurement Method

---

# Numerical Precision

Internal

Double Precision

Display

6 Decimal Places

Configurable

---

# Future Enhancements

Digital Image Correlation

Laser Area Measurement

3D Neck Geometry

Finite Element Local Strain

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ Uses logarithmic definition

✔ Uses measured fracture area

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full audit traceability

---

End of Document
