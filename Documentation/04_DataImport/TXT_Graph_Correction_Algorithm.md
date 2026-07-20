# TXT Graph Correction Algorithm

Document ID : MTDMS-IMP-032

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

This document defines the mathematical algorithm used to correct the displayed tensile stress-strain graph.

The algorithm shall compensate for machine compliance, grip seating, backlash and extensometer synchronization errors while preserving all original measured values.

This algorithm is compatible with

ISO 6892-1

ASTM E8

ASTM A370

INSO 3132

---

# Design Philosophy

Measured Data

↓

Engineering Data

↓

Correction Layer

↓

Displayed Graph

↓

Report Graph

Raw measurements shall never change.

Engineering calculations shall never change.

Only visualization is corrected.

---

# Inputs

Engineering Stress

Engineering Strain

Young's Modulus

Yield Point

Material

Gauge Length

Area

Fracture Position

---

# Output

Corrected X Coordinates

Reference Elastic Line

Yield Marker

Elastic Region

Corrected Graph

---

# Algorithm Overview

Step 1

Locate Elastic Region

↓

Step 2

Fit Straight Line

↓

Step 3

Compare With Reference Modulus

↓

Step 4

Compute Horizontal Offset

↓

Step 5

Correct Elastic Region

↓

Step 6

Blend Transition

↓

Step 7

Freeze Plastic Region

---

# Step 1

Locate Elastic Region

Candidate Region

0%

↓

Yield

Initial estimate

Material Library

↓

Expected Yield

Window

±20%

---

# Step 2

Linear Regression

Elastic Region

↓

Least Squares

Compute

Slope

Intercept

Coefficient of Determination

R²

---

# Acceptance

R²

≥0.998

Otherwise

Expand

Shrink

Retry

Maximum

10 iterations

---

# Step 3

Reference Comparison

Measured Slope

↓

Reference Young's Modulus

Difference

Computed

---

# Error

Elastic Error

```
ΔE = Emeasured − Ereference
```

---

# Step 4

Horizontal Offset

For each point

Compute

```
Δx = σ / Ereference
```

Instead of

```
σ / Emeasured
```

Difference

Applied

Horizontally

---

# Step 5

Elastic Correction

For every point

Before Yield

```
Xcorrected = Xmeasured + Δx
```

Y

Unchanged

---

# Step 6

Transition Zone

Abrupt correction

Not allowed

Transition

5%

↓

10%

Around Yield

Smooth interpolation

Required

---

# Step 7

Plastic Region

After Yield

No correction

Unless

Operator selects

Full Curve Correction

---

# Fracture

Graph ends

Exactly

At fracture point

Data after fracture

Hidden

Never deleted

---

# Necking

Future

Automatic Necking Detection

Reserved

---

# Manual Yield

Operator clicks

Yield Point

↓

Elastic Region recalculated

↓

Correction repeated

---

# Reset

Reset removes

Entire correction layer

Original Engineering Graph restored.

---

# Numerical Stability

Regression

Double Precision

Tolerance

1×10⁻¹²

No cumulative error

---

# Performance

100000 points

↓

Correction

<1 second

---

# Error Handling

Regression Failure

↓

Display Warning

↓

Use Original Graph

No correction applied

---

# Logging

Store

Original Slope

Reference Slope

R²

Correction Applied

Operator Override

Timestamp

---

# Acceptance Criteria

✔ Engineering values unchanged

✔ Raw values unchanged

✔ Horizontal correction only

✔ Smooth transition at yield

✔ Automatic reset available

✔ Manual yield supported

✔ Compatible with Excel 2019

✔ ISO 6892-1 compliant

---

End of Document
