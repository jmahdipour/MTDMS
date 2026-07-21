# True Proof Strength (Rt) Calculation

Document ID : MTDMS-ENG-018

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

This document defines the calculation of Rt (True Proof Strength).

Rt is required by several ISO standards for materials where conventional yield points cannot be determined reliably.

Unlike Rp, Rt is based on total extension under load rather than permanent plastic offset only.

---

# Reference Standards

ISO 6892-1

ISO 630

ISO 898

INSO 3132

---

# Definition

Rt is the stress corresponding to a specified total extension.

The extension includes

Elastic Extension

+

Plastic Extension

Therefore

```
Rt

≠

Rp
```

---

# Supported Rt Values

Rt0.5

Rt0.6

Rt1.0

Custom

Administrator Defined

---

# General Equation

```
εtotal

=

εelastic

+

εplastic
```

Where

εplastic

Specified by Standard

---

# Calculation Sequence

Engineering Stress

↓

Engineering Strain

↓

Young's Modulus

↓

Elastic Extension

↓

Specified Total Extension

↓

Offset Construction

↓

Intersection

↓

Rt

---

# Elastic Component

Elastic Extension

Calculated from

```
εelastic

=

σ / E
```

---

# Total Extension

Example

Rt0.5

```
εtotal

=

0.005
```

---

# Offset Construction

The Rt line

is constructed using

Measured Young's Modulus

and

Specified Total Extension.

---

# Intersection Algorithm

Engineering Curve

↓

Offset Line

↓

Sign Change

↓

Linear Interpolation

↓

Rt

---

# Numerical Method

Interpolation

Required

Nearest Point

Not Allowed

---

# Validation

Rt

Must satisfy

```
Elastic Region

↓

Rt

↓

Ultimate Strength

↓

Fracture
```

---

# Data Required

Engineering Stress

Engineering Strain

Young's Modulus

Specified Rt Offset

---

# Input

```
EngineeringStress()

EngineeringStrain()

YoungMeasured
```

---

# Output

Rt Stress

Rt Strain

Rt Force

Rt Extension

Rt Index

---

# Example

Young

210000 MPa

Specified Rt

0.5 %

↓

Construct Offset

↓

Find Intersection

↓

Rt

---

# Error Conditions

Young Missing

↓

Abort

No Intersection

↓

Engineering Error

Invalid Offset

↓

Abort

Overflow

↓

Rollback

---

# Graph Representation

Display

Elastic Line

Rt Offset Line

Intersection Marker

Construction Lines

Engineering Mode Only

Report

Marker Only

---

# SQLite Storage

Table

```
tblEngineeringResult
```

Fields

RtMethod

RtValue

RtStress

RtStrain

RtForce

RtIndex

---

# Material Library

Material Library

may define

Preferred Rt Method

Example

Pipe

↓

Rt0.5

Structural Steel

↓

Rp0.2

---

# Future Improvements

Spline Intersection

Adaptive Offset

Automatic Standard Selection

Machine Learning Prediction

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ Supports configurable Rt values

✔ Uses measured Young's Modulus

✔ Uses interpolation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full traceability

---

End of Document
