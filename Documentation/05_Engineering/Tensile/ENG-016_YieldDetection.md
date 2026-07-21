# Yield Point Detection

Document ID : MTDMS-ENG-016

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

This document defines the algorithms used for automatic determination of yield strength according to the selected material standard.

Yield detection is one of the most critical calculations because it directly affects:

• Material Acceptance

• Certificate Generation

• Mechanical Property Verification

• Structural Design Compliance

• ISO / ASTM Reporting

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

ISO 630

ISO 898

INSO 3132

---

# Supported Yield Methods

Upper Yield Strength (ReH)

Lower Yield Strength (ReL)

Rp0.2

Rp0.1

Rp0.05

Rt

Manual Yield

Future

Proof Stress

Custom Offset

---

# Calculation Pipeline

Engineering Stress

↓

Engineering Strain

↓

Elastic Region

↓

Young's Modulus

↓

Yield Algorithm

↓

Validation

↓

Engineering Results

---

# Automatic Method Selection

Material Library

↓

Selected Standard

↓

Yield Method

↓

Calculation

Example

Low Carbon Steel

↓

Upper / Lower Yield

High Strength Steel

↓

Rp0.2

Pipe Standard

↓

Rt

---

# Method 1

Upper Yield Strength (ReH)

Definition

Maximum stress immediately before the first discontinuous drop.

Detection

```
Maximum Local Peak

↓

Stress Drop

↓

Upper Yield
```

Requirements

Distinct Load Drop

Stable Signal

---

# Method 2

Lower Yield Strength (ReL)

Definition

Minimum stress after Upper Yield and before strain hardening begins.

Detection

```
Upper Yield

↓

Stress Drop

↓

Minimum Plateau Stress

↓

Lower Yield
```

---

# Method 3

Rp0.2 Offset

Definition

Stress corresponding to a permanent plastic strain of

```
0.2 %
```

Procedure

1

Determine Young's Modulus

↓

2

Create Parallel Offset Line

↓

3

Find First Intersection

↓

4

Yield Point

---

# Offset Equation

Offset

```
εoffset = 0.002
```

Parallel Line

```
σ = E(ε − 0.002)
```

Intersection

↓

Rp0.2

---

# Method 4

Rp0.1

Same procedure

Offset

```
0.001
```

---

# Method 5

Rp0.05

Offset

```
0.0005
```

---

# Method 6

Rt

True extension method

Used mainly for

Pipe

Tube

Special Materials

Calculated according to

Selected Standard

---

# Manual Yield

Operator

Clicks

Stress-Strain Graph

↓

Yield Marker

↓

Engineering Recalculated

Audit Logged

---

# Numerical Algorithm

Intersection search

Uses

Linear interpolation

Between neighboring samples.

No nearest-point approximation permitted.

---

# Validation Rules

Yield

Must satisfy

```
Yield Stress

<

Ultimate Tensile Strength
```

Yield

Must occur

After Elastic Region

Before Necking

---

# Warning Conditions

Multiple Possible Intersections

↓

Operator Warning

Weak Elastic Regression

↓

Yield Warning

Large Noise

↓

Operator Confirmation

---

# Failure Conditions

No Intersection

↓

Engineering Error

Invalid Elastic Region

↓

Abort

Young Not Calculated

↓

Abort

---

# Stored Results

Yield Method

Yield Index

Yield Force

Yield Stress

Yield Strain

Yield Extension

Yield Time

Operator Override

Automatic / Manual

---

# SQLite

Table

```
tblEngineeringResult
```

Fields

YieldMethod

YieldStress

YieldStrain

YieldForce

YieldIndex

---

# Graph

Displayed

Yield Marker

Offset Line

Elastic Line

Construction Lines

Visible

Operator Mode

Hidden

Report Mode

---

# Performance

Complexity

O(n)

Suitable for

100,000 Samples

---

# Future Improvements

Spline Intersection

Adaptive Offset

Machine Learning Yield Detection

Digital Image Correlation

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ ASTM E8 compliant

✔ Multiple yield methods supported

✔ Automatic and manual modes

✔ Linear interpolation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full audit traceability

---

End of Document
