# Ultimate Tensile Strength (UTS) Calculation

Document ID : MTDMS-ENG-019

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

This document defines the calculation of Ultimate Tensile Strength (UTS).

UTS is the maximum engineering stress reached during the tensile test before necking causes the engineering stress to decrease.

The value shall be calculated automatically for every tensile specimen.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ISO 630

ISO 898

INSO 3132

---

# Definition

Ultimate Tensile Strength is

the highest engineering stress recorded during the tensile test.

```
UTS = max(σengineering)
```

---

# Mathematical Formula

Engineering Stress

```
σ = F / A₀
```

Ultimate Tensile Strength

```
UTS

=

max(σ)
```

---

# Calculation Sequence

Geometry

↓

Engineering Stress

↓

Maximum Stress Search

↓

Validation

↓

Store UTS

↓

Locate Necking

---

# Input

Engineering Stress Array

Engineering Force Array

Sample Index

---

# Output

Ultimate Tensile Strength

Maximum Force

Maximum Stress Index

Maximum Extension

Maximum Time

---

# Search Algorithm

```
σ₁

↓

σ₂

↓

σ₃

↓

...

↓

σmax

↓

Continue

↓

End
```

The entire engineering stress array shall be scanned.

---

# Multiple Equal Peaks

If two or more identical maximum values exist

↓

The first occurrence

shall be used.

Reason

Beginning of necking is defined at the first maximum.

---

# Validation

UTS

Must satisfy

```
UTS

>

Yield Strength
```

---

```
UTS

>

0
```

---

```
UTS

Before

Fracture
```

---

# Necking

The point immediately following

UTS

is the beginning of engineering necking.

Future modules

shall use

```
UTS Index
```

to locate

Necking Region.

---

# Data Type

Double Precision

---

# Example

Maximum Force

125000 N

Original Area

250 mm²

```
UTS

=

125000 / 250

=

500 MPa
```

---

# Error Conditions

Stress Array Empty

↓

Abort

Negative UTS

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

# Graph Representation

Display

Maximum Marker

Label

UTS

Displayed

Stress

Force

Extension

Time

---

# SQLite Storage

Table

```
tblEngineeringResult
```

Fields

```
UltimateStress

UltimateForce

UltimateIndex

UltimateExtension

UltimateTime
```

---

# Report

Certificate

Displays

Ultimate Tensile Strength

Maximum Force

Standard

Material

Units

---

# Performance

Algorithm

Maximum Search

Complexity

```
O(n)
```

Suitable for

100000 Samples

---

# Future Improvements

Noise Resistant Peak Detection

Plateau Detection

Multiple Peak Analysis

Adaptive Smoothing

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ ASTM E8 compliant

✔ Uses Engineering Stress

✔ First maximum selected

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Compatible with Graph Engine

---

End of Document
