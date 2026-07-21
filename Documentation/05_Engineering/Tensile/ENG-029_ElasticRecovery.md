# Elastic Recovery Analysis

Document ID : MTDMS-ENG-029

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

This document defines the calculation and analysis of Elastic Recovery.

Elastic Recovery represents the elastic portion of deformation that disappears after the applied load is removed.

The parameter is used for

• Springback estimation

• Elastic-Plastic separation

• Material modelling

• Forming simulations

• Verification of Young's Modulus

---

# Reference Standards

ISO 6892-1

ASTM E111

ASTM E8 / ASTM E8M

---

# Definition

Total deformation consists of

```
Total Strain

=

Elastic Strain

+

Plastic Strain
```

When the load is removed,

Elastic Strain disappears,

while

Plastic Strain remains.

---

# Mathematical Definition

Elastic Strain

```
εelastic

=

σ / E
```

Plastic Strain

```
εplastic

=

εtotal

−

εelastic
```

Elastic Recovery

```
Elastic Recovery

=

εelastic
```

---

# Calculation Sequence

Engineering Stress

↓

Engineering Strain

↓

Young's Modulus

↓

Elastic Strain

↓

Plastic Strain

↓

Elastic Recovery

---

# Inputs

Engineering Stress

Engineering Strain

Young's Modulus

---

# Outputs

Elastic Strain

Plastic Strain

Elastic Recovery %

Plastic Recovery %

---

# Units

Stress

MPa

Strain

mm/mm

Display

%

---

# Example

Engineering Stress

300 MPa

Young's Modulus

210000 MPa

```
Elastic Strain

=

300 / 210000

=

0.0014286
```

Engineering Strain

```
0.015
```

Plastic Strain

```
0.015

−

0.0014286

=

0.0135714
```

---

# Validation

Elastic Strain

≥ 0

Plastic Strain

≥ 0

Elastic Strain

≤

Total Strain

---

# Material Behaviour

High Strength Steel

↓

Small Elastic Recovery

Spring Steel

↓

Large Elastic Recovery

Aluminium

↓

Moderate Elastic Recovery

---

# Graph Representation

Optional Graph

Total Strain

↓

Elastic Portion

↓

Plastic Portion

Displayed using

Different Colors

---

# Database Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

ElasticStrain

PlasticStrain

ElasticRecovery

---

# Engineering Applications

Springback Prediction

Forming Analysis

Bending Compensation

Finite Element Calibration

---

# Error Conditions

Young Missing

↓

Abort

Stress Missing

↓

Abort

Plastic Strain Negative

↓

Engineering Error

Overflow

↓

Abort

Rollback

---

# Future Enhancements

Unload Curve Analysis

Cyclic Loading

Hysteresis Analysis

Springback Prediction Module

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compatible

✔ Uses measured Young's Modulus

✔ Separates elastic and plastic strain

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Ready for springback analysis

---

End of Document
