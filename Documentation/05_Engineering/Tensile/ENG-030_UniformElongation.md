# Uniform Elongation Calculation

Document ID : MTDMS-ENG-030

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

This document defines the calculation of Uniform Elongation.

Uniform Elongation is the permanent elongation of the specimen before localized necking begins.

Unlike Total Elongation, it excludes deformation occurring after neck formation.

Uniform Elongation is an important parameter for

• Material Ductility

• Sheet Formability

• Metal Forming

• Finite Element Material Models

• Material Comparison

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

---

# Definition

Uniform Elongation is the engineering strain measured at the Ultimate Tensile Strength.

Therefore

```
Uniform Elongation

=

Engineering Strain

at

UTS
```

---

# Mathematical Definition

```
Ag = εUTS × 100
```

Where

Ag

Uniform Elongation

%

εUTS

Engineering Strain at Ultimate Tensile Strength

---

# Calculation Sequence

Engineering Stress

↓

Ultimate Tensile Strength

↓

UTS Index

↓

Engineering Strain

↓

Uniform Elongation

---

# Input

Engineering Stress Array

Engineering Strain Array

UTS Index

---

# Output

Uniform Elongation

Uniform Extension

Uniform Strain

---

# Units

Internal

mm/mm

Display

%

---

# Engineering Meaning

Uniform Elongation

Represents

Maximum strain

before

Localized Necking

After this point

Deformation becomes localized

and is no longer uniformly distributed.

---

# Relationship

```
Yield

↓

Plastic Region

↓

Uniform Elongation

↓

Necking

↓

Fracture

↓

Total Elongation
```

---

# Example

Engineering Strain

at UTS

```
0.185
```

Uniform Elongation

```
Ag

=

18.5 %
```

---

# Validation

```
Yield

<

Uniform Elongation

<

Total Elongation
```

---

Uniform Elongation

shall always occur

before fracture.

---

# Error Conditions

UTS Missing

↓

Abort

Engineering Strain Missing

↓

Abort

UTS After Fracture

↓

Engineering Error

Overflow

↓

Abort

Rollback

---

# Graph Representation

Display

Yield

↓

Uniform Elongation

↓

Necking

↓

Fracture

Each point shall be marked independently.

---

# Database Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

```
UniformElongation

UniformStrain

UTSIndex
```

---

# Report

Certificate

Displays

Uniform Elongation

Total Elongation

Reduction of Area

Comparison

may be shown

between

Uniform

and

Total

Elongation.

---

# Material Behaviour

Higher Uniform Elongation

↓

Better Formability

Lower Uniform Elongation

↓

Earlier Necking

↓

Lower Plastic Stability

---

# Future Enhancements

Automatic Forming Limit Estimation

Formability Index

FLD Integration

Digital Image Correlation

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ Calculated at UTS

✔ Independent of fracture measurement

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Compatible with Graph Engine

---

End of Document
