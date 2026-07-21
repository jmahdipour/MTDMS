# True Fracture Stress Calculation

Document ID : MTDMS-ENG-024

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

This document defines the calculation of True Fracture Stress.

True Fracture Stress represents the actual stress acting on the minimum cross-sectional area immediately before fracture.

Unlike Ultimate Tensile Strength, True Fracture Stress uses the measured fracture area.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

True Fracture Stress is calculated from

Maximum Force Immediately Before Fracture

divided by

Minimum Measured Area at Fracture.

---

# Mathematical Formula

```
σTF = Ff / Af
```

Where

σTF

True Fracture Stress

Ff

Force immediately before fracture

Af

Measured minimum area after fracture

---

# Variables

Input

Fracture Force

Final Area

Output

True Fracture Stress

---

# Area Determination

Round Specimen

```
Af = π df² / 4
```

---

Flat Specimen

```
Af = bf × tf
```

---

Pipe

Calculated using

Pipe Geometry Module

---

# Calculation Pipeline

Fracture Detection

↓

Final Area Measurement

↓

True Fracture Stress

↓

Report

---

# Example

Force Before Fracture

110000 N

Final Area

120 mm²

```
σTF

=

110000 / 120

=

916.67 MPa
```

---

# Validation

```
Af > 0
```

```
Ff > 0
```

```
σTF ≥ UTS
```

Normally

True Fracture Stress

is greater than

Engineering Ultimate Tensile Strength.

---

# Error Conditions

Final Area Missing

↓

Abort

Fracture Force Missing

↓

Abort

Area ≤ 0

↓

Engineering Error

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
TrueFractureStress

FractureForce

FinalArea
```

---

# Graph Usage

True Fracture Stress

is not plotted

on the Engineering Stress-Strain Curve.

It is displayed only

as a calculated property.

---

# Report

Certificate Displays

True Fracture Stress

Final Area

Fracture Force

Calculation Method

---

# Future Enhancements

Local Neck Diameter Tracking

Laser Area Measurement

Digital Image Correlation

3D Fracture Surface Analysis

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ Uses measured fracture area

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full audit traceability

---

End of Document
