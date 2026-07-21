# Plastic Region Analysis

Document ID : MTDMS-ENG-026

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

This document defines the analysis of the plastic deformation region of the tensile test.

The plastic region begins immediately after yielding and ends at fracture.

The analysis is used for:

• Material characterization

• Work hardening analysis

• Flow curve generation

• Finite Element material models

• Engineering reports

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

ISO 630

ISO 898

---

# Plastic Region Definition

```
Elastic Region

↓

Yield Point

↓

Plastic Region

↓

Uniform Plastic Deformation

↓

Necking

↓

Fracture
```

---

# Plastic Region Limits

Start

Yield Point

End

Fracture Point

---

# Input Data

Engineering Stress

Engineering Strain

True Stress

True Strain

Yield Index

Necking Index

Fracture Index

---

# Output

Plastic Region Start

Plastic Region End

Uniform Plastic Region

Necking Region

Plastic Strain Array

Plastic Stress Array

---

# Plastic Strain

Plastic Strain is calculated as

```
εplastic

=

εtotal

−

εelastic
```

Where

```
εelastic

=

σ / E
```

---

# Plastic Region Segmentation

The software divides the plastic region into

Section 1

Uniform Plastic Deformation

↓

Section 2

Necking

---

# Uniform Plastic Region

Start

Yield Point

End

Ultimate Tensile Strength

This region is used for

Flow Curve

Hardening

Material Modelling

---

# Necking Region

Start

Ultimate Tensile Strength

End

Fracture

Engineering stress is no longer representative.

True stress analysis becomes dominant.

---

# Data Validation

Plastic Region

Must satisfy

```
Yield Index

<

UTS Index

<

Fracture Index
```

---

# Calculated Properties

Plastic Work

Maximum Plastic Strain

Uniform Plastic Strain

Necking Length

Plastic Energy

Hardening Input

---

# Graph Representation

Display

Elastic Region

Blue

Plastic Region

Orange

Necking

Red

Fracture

Black

Colors configurable.

---

# Database Storage

SQLite

Table

```
tblEngineeringPlastic
```

Fields

PlasticStartIndex

PlasticEndIndex

UniformPlasticIndex

NeckingIndex

MaximumPlasticStrain

PlasticWork

---

# Error Conditions

Yield Missing

↓

Abort

UTS Missing

↓

Abort

Fracture Missing

↓

Abort

Index Order Invalid

↓

Engineering Error

---

# Performance

Complexity

```
O(n)
```

One pass

through the plastic region.

---

# Future Enhancements

Automatic Flow Curve

Plastic Energy Integration

AI Material Classification

FE Material Export

Digital Image Correlation

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ Plastic region correctly segmented

✔ Uniform deformation identified

✔ Necking identified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Ready for work hardening analysis

---

End of Document
