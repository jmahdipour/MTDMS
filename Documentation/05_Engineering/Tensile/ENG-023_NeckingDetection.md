# Necking Detection Algorithm

Document ID : MTDMS-ENG-023

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

This document defines the automatic detection of necking.

Necking represents the transition from uniform plastic deformation to localized plastic deformation.

Correct detection is essential because several calculations become invalid after necking begins.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

Necking begins when plastic deformation is no longer uniformly distributed along the gauge length.

After necking,

the Engineering Stress starts decreasing,

while the True Stress usually continues increasing.

---

# Engineering Behaviour

Uniform Deformation

↓

Engineering Stress Increases

↓

Ultimate Tensile Strength

↓

Necking Begins

↓

Engineering Stress Decreases

↓

Fracture

---

# Detection Principle

The beginning of necking is defined as

the first occurrence

of

Maximum Engineering Stress.

Therefore

```
Necking Index

=

Ultimate Tensile Strength Index
```

---

# Mathematical Basis

Before Necking

```
dσ/dε > 0
```

At Necking

```
dσ/dε = 0
```

After Necking

```
dσ/dε < 0
```

---

# Calculation Sequence

Engineering Stress

↓

Maximum Stress

↓

Necking Index

↓

True Stress

↓

Plastic Analysis

---

# Input

Engineering Stress Array

Engineering Strain Array

UTS Index

---

# Output

Necking Index

Necking Stress

Necking Strain

Necking Force

Necking Time

---

# Validation

Necking

Must occur

After Yield

```
Yield Index

<

Necking Index
```

---

Necking

Must occur

Before Fracture

```
Necking Index

<

Fracture Index
```

---

# Multiple Peaks

If several equal maximum stresses exist

↓

First Maximum

defines

Necking

because localized deformation begins there.

---

# Noise Handling

Small oscillations around the maximum

shall not create false necking points.

Optional

Peak smoothing

may be applied.

Raw data

shall remain unchanged.

---

# Engineering Consequences

After Necking

Engineering Stress

No longer represents

actual material stress.

True Stress

becomes

preferred.

---

# Graph Representation

Display

UTS Marker

↓

Necking Marker

Both refer to the same physical point.

Label

```
UTS / Necking
```

---

# SQLite Storage

Table

```
tblEngineeringResult
```

Fields

```
NeckingIndex

NeckingStress

NeckingStrain

NeckingForce

NeckingTime
```

---

# Relationship with Other Modules

Necking Detection

↓

True Stress

↓

True Strain

↓

Fracture Analysis

↓

Hardening Analysis

---

# Error Conditions

UTS Missing

↓

Abort

Fracture Before UTS

↓

Engineering Error

Multiple Invalid Peaks

↓

Warning

Operator Review

---

# Future Improvements

Considère Criterion

Digital Image Correlation

Local Diameter Monitoring

Machine Learning Necking Detection

Reserved

---

# Acceptance Criteria

✔ Necking begins at first UTS

✔ Compatible with ISO 6892-1

✔ Compatible with ASTM E8/E8M

✔ Supports noisy signals

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Integrated with True Stress calculations

---

End of Document
