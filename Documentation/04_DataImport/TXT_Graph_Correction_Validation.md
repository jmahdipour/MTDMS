# TXT Graph Correction Validation

Document ID : MTDMS-IMP-033

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Graph Correction Engine

---

# Purpose

This document defines all validation procedures required before, during and after graphical correction.

The objective is to ensure that graph correction improves visualization while preserving engineering correctness.

Graph correction shall never introduce false engineering results.

---

# Validation Philosophy

Raw Data

↓

Engineering Data

↓

Graph Correction

↓

Validation

↓

Approved Display

---

# Validation Stages

Stage 1

Input Validation

↓

Stage 2

Elastic Region Validation

↓

Stage 3

Regression Validation

↓

Stage 4

Correction Validation

↓

Stage 5

Engineering Verification

↓

Stage 6

Operator Approval

---

# Stage 1

Input Validation

Required

Material

Young's Modulus

Area

Gauge Length

Engineering Stress

Engineering Strain

Yield Estimate

Missing information

↓

Correction not permitted

---

# Stage 2

Elastic Region Validation

Checks

Continuous Data

No Missing Samples

Monotonic Increase

No Outliers

Minimum Samples

20

Recommended

100+

---

# Stage 3

Regression Validation

Linear Regression

↓

Slope

↓

Intercept

↓

R²

Acceptance

```
R² ≥ 0.998
```

Preferred

```
R² ≥ 0.9995
```

---

# Stage 4

Correction Validation

After correction

Verify

Elastic slope

≈

Material Library

Tolerance

±1%

---

# Stage 5

Engineering Verification

Verify

Yield Stress

UNCHANGED

Ultimate Strength

UNCHANGED

Maximum Force

UNCHANGED

Fracture Position

UNCHANGED

True Stress

UNCHANGED

True Strain

UNCHANGED

Only X display coordinates may change.

---

# Stage 6

Operator Approval

Operator verifies

Elastic Region

Reference Line

Yield Marker

Transition Zone

Fracture

↓

Approve

or

Reject

---

# Validation Parameters

## Young's Modulus Error

```
|Emeasured − Ereference|
```

Target

<1%

Maximum

3%

---

## Yield Shift

Horizontal

Allowed

Vertical

Not Allowed

---

## Stress Difference

Allowed

```
0 MPa
```

Engineering stress values

shall never change.

---

## Strain Difference

Engineering strain

Database

UNCHANGED

Display strain

May change

---

# Transition Validation

Transition Region

Must be

Continuous

Differentiable

No sudden jumps

No broken curve

---

# Fracture Validation

Fracture Marker

Must remain

Original Position

Graph shall terminate

Exactly at fracture.

---

# Plastic Region Validation

Plastic Region

Must remain

Visually continuous

No distortion

No scaling

Unless Full Correction enabled.

---

# Manual Yield Validation

If operator changes yield

↓

Regression repeated

↓

Correction repeated

↓

Validation repeated

---

# Automatic Rejection

Correction rejected if

Regression fails

R² below threshold

Missing data

Invalid modulus

Negative correction

Broken curve

---

# Logging

Store

Original Slope

Corrected Slope

Reference Modulus

R²

Correction Accepted

Operator

Timestamp

---

# Validation Report

Generated automatically

Contains

Pass

Warning

Fail

Values

Recommendations

---

# Future Validation

AI Elastic Detection

Machine Learning Fit

Automatic Outlier Removal

Reserved

---

# Acceptance Criteria

✔ Raw Data unchanged

✔ Engineering values unchanged

✔ Corrected slope within tolerance

✔ Continuous graph

✔ Original fracture preserved

✔ Operator approval required

✔ Complete validation log

✔ ISO 6892-1 compliant

---

End of Document
