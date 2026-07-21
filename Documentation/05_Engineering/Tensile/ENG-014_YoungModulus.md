# Young's Modulus Calculation

Document ID : MTDMS-ENG-014

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

This document defines the calculation of Young's Modulus (Elastic Modulus).

Young's Modulus is calculated from the elastic portion of the engineering stress-strain curve.

The calculated modulus is subsequently used by

• Graph correction

• Yield determination

• Material verification

• ISO 6892 compliance

• ASTM E111 compliance

---

# Reference Standards

ISO 6892-1

ASTM E111

ISO 7500-1

---

# Definition

Young's Modulus is the slope of the linear elastic portion of the engineering stress-strain curve.

---

# Formula

```
E = Δσ / Δε
```

Where

E

Young's Modulus

σ

Engineering Stress

ε

Engineering Strain

---

# General Method

The modulus shall **never** be calculated from only two points.

The calculation shall use

Linear Least Squares Regression

over the selected elastic region.

---

# Calculation Pipeline

Engineering Stress

↓

Engineering Strain

↓

Elastic Region Detection

↓

Linear Regression

↓

Young's Modulus

↓

Validation

---

# Input Data

Engineering Stress Array

Engineering Strain Array

Elastic Region Start

Elastic Region End

---

# Output

YoungMeasured

RegressionSlope

RegressionIntercept

RegressionR²

ElasticStartIndex

ElasticEndIndex

---

# Regression Method

Current Version

Ordinary Least Squares (OLS)

Future

Robust Regression

RANSAC

Theil–Sen

Reserved

---

# Mathematical Model

```
σ = E ε + b
```

Where

E

Regression Slope

b

Regression Intercept

---

# Elastic Region Requirements

Minimum Points

50

Recommended

100

Maximum

Automatic

---

# R² Requirement

Minimum

```
0.9990
```

Preferred

```
0.9995
```

If

```
R² < 0.9990
```

↓

Warning

Operator Review

---

# Material Verification

If Material Library contains

Reference Young's Modulus

↓

Compare

Measured

Reference

---

# Acceptance Range

Recommended

±1 %

Maximum

±3 %

Outside tolerance

↓

Warning

Not automatic failure

---

# Units

Internal

MPa

Display

GPa

Conversion

```
GPa = MPa / 1000
```

---

# Example

Engineering Stress

200 MPa

Engineering Strain

0.001

```
E

=

200 / 0.001

=

200000 MPa

=

200 GPa
```

---

# Numerical Stability

Very small strain values

(<1×10⁻⁶)

Ignored

to prevent unstable slope calculation.

---

# Error Conditions

Elastic Region Not Found

↓

Abort

Insufficient Points

↓

Abort

Regression Failure

↓

Abort

NaN

↓

Abort

Overflow

↓

Abort

Rollback

---

# Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

YoungMeasured

YoungCorrected

RegressionR2

ElasticStartIndex

ElasticEndIndex

---

# Graph Usage

Young's Modulus is used for

Elastic Line

Graph Correction

Offset Yield Line

Operator Verification

---

# Relationship with Graph Correction

Measured Young

↓

Compared with Material Library

↓

Horizontal Axis Correction

↓

Display Only

Original engineering data

Never modified.

---

# Performance

Complexity

O(n)

One regression

Per specimen

---

# Future Enhancements

Adaptive Elastic Window

Automatic Noise Rejection

Multi-pass Regression

Machine Learning Elastic Detection

Reserved

---

# Acceptance Criteria

✔ Complies with ASTM E111

✔ Compatible with ISO 6892-1

✔ Uses regression

✔ Uses validated elastic region

✔ Stores R²

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

---

End of Document
