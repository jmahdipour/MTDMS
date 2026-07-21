# Offset Proof Strength Calculation (Rp)

Document ID : MTDMS-ENG-017

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

This document defines the calculation of proof strength (Rp) using the offset method.

Rp shall be calculated whenever a distinct upper/lower yield point does not exist or when the applicable standard explicitly requires proof stress.

Supported proof stresses include

• Rp0.05

• Rp0.1

• Rp0.2

• User-defined Rp

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ISO 630

ISO 898

INSO 3132

---

# Principle

A straight line parallel to the elastic portion of the stress–strain curve is shifted horizontally by a specified permanent strain.

The first intersection of this line with the engineering stress–strain curve defines Rp.

---

# Supported Offset Values

| Name | Permanent Strain |
|-------|------------------|
| Rp0.05 | 0.0005 |
| Rp0.10 | 0.0010 |
| Rp0.20 | 0.0020 |
| Custom | User Defined |

---

# Calculation Sequence

```
Engineering Stress

↓

Engineering Strain

↓

Elastic Region

↓

Young's Modulus

↓

Offset Line

↓

Intersection Search

↓

Rp
```

---

# Offset Line Equation

General Equation

```
σ = E ( ε − εoffset )
```

Where

σ

Offset Stress

E

Measured Young's Modulus

ε

Engineering Strain

εoffset

Permanent Offset Strain

---

# Engineering Curve

The engineering curve consists of

```
σ(i)

ε(i)
```

for every imported sample.

---

# Intersection Detection

The intersection shall **not** be determined by selecting the nearest point.

Instead,

the software shall detect

a sign change

between

```
Curve

and

Offset Line
```

and calculate the exact crossing using interpolation.

---

# Linear Interpolation

If

```
Point i

↓

Negative Difference

Point i+1

↓

Positive Difference
```

then

the intersection lies between

```
i

and

i+1
```

---

# Interpolated Yield

The final

Rp

shall be obtained by

linear interpolation

between the two neighbouring samples.

---

# Numerical Stability

Interpolation shall always be performed using

Double Precision

No integer arithmetic permitted.

---

# Multiple Intersections

If multiple intersections exist,

the **first valid intersection after the elastic region** shall be selected.

Subsequent intersections are ignored.

---

# Validation

Rp

must satisfy

```
Elastic Region

↓

Rp

↓

Ultimate Strength

↓

Fracture
```

---

# Error Conditions

No Elastic Region

↓

Abort

Young's Modulus Missing

↓

Abort

No Intersection

↓

Engineering Error

Multiple Invalid Intersections

↓

Operator Warning

---

# User-defined Rp

Administrator may define

```
Rp0.15

Rp0.30

Rp0.50
```

or any offset permitted by the selected standard.

Custom offsets are stored in

```
tblEngineeringSettings
```

---

# SQLite Storage

Table

```
tblEngineeringResult
```

Fields

```
YieldMethod

OffsetValue

YieldStress

YieldStrain

YieldForce

YieldIndex
```

---

# Graph Representation

Displayed

Elastic Line

Offset Line

Intersection Marker

Yield Marker

Construction lines

Visible only

in Engineering Mode.

Hidden

in Final Report.

---

# Performance

Complexity

```
O(n)
```

Suitable for

100,000 samples

---

# Future Improvements

Spline Intersection

Polynomial Approximation

Adaptive Offset

Machine Learning Assisted Detection

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ ASTM E8 compliant

✔ Supports Rp0.05

✔ Supports Rp0.10

✔ Supports Rp0.20

✔ Supports Custom Rp

✔ Uses interpolation

✔ SQLite compatible

✔ Excel 2019 compatible

---

End of Document
