# Reduction of Area Calculation

Document ID : MTDMS-ENG-022

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

This document defines the calculation of Reduction of Area (RA).

Reduction of Area is an important ductility parameter used to evaluate the plastic deformation capability of metallic materials.

Unlike elongation, Reduction of Area is determined from the fractured cross-section.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ISO 630

ISO 898

INSO 3132

---

# Definition

Reduction of Area represents the percentage decrease in the minimum cross-sectional area after fracture.

The value shall be determined using physical measurements of the fractured specimen.

---

# Formula

```
Z = ((A₀ − Af) / A₀) × 100
```

Where

Z

Reduction of Area

%

A₀

Original Cross-sectional Area

Af

Minimum Cross-sectional Area After Fracture

---

# Variables

Input

Original Area

Final Area

Output

Reduction of Area

---

# Measurement Priority

1

Measured Final Dimensions

↓

2

Digital Measuring Device

↓

3

Manual Entry

Never calculated from engineering stress.

---

# Round Specimen

Original Area

```
A₀ = π d₀² / 4
```

Final Area

```
Af = π df² / 4
```

Where

d₀

Original Diameter

df

Minimum Diameter After Fracture

---

# Flat Specimen

Original Area

```
A₀ = b₀ × t₀
```

Final Area

```
Af = bf × tf
```

Where

b

Width

t

Thickness

Measured at the smallest fractured section.

---

# Pipe Specimen

Area shall be calculated using

Pipe Geometry Module

after fracture measurements.

---

# Example

Original Area

250 mm²

Final Area

150 mm²

```
Z

=

((250−150)/250)

×

100

=

40 %
```

---

# Validation Rules

```
Af

>

0
```

---

```
Af

<

A₀
```

---

```
Reduction of Area

0 %

↓

100 %
```

---

# Error Conditions

Af = 0

↓

Engineering Error

Af > A₀

↓

Invalid Measurement

Missing Measurements

↓

Operator Prompt

Negative Result

↓

Abort

---

# Manual Editing

Operator may modify

Final Diameter

Final Width

Final Thickness

↓

Software recalculates

Final Area

↓

Reduction of Area

↓

Audit Logged

---

# Database Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

OriginalArea

FinalArea

ReductionOfAreaPercent

FinalDiameter

FinalWidth

FinalThickness

---

# Report

Certificate displays

Original Area

Final Area

Reduction of Area

Measurement Method

Operator

Measurement Date

---

# Relationship to Elongation

Elongation

Measures

Axial Plastic Deformation

Reduction of Area

Measures

Local Plastic Deformation

Both shall be reported independently.

---

# Statistical Analysis

When multiple specimens exist

Average

Minimum

Maximum

Standard Deviation

Coefficient of Variation

shall be calculated.

---

# Future Enhancements

Automatic Diameter Measurement

Image Recognition

Laser Micrometer

3D Fracture Surface Analysis

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ ASTM E8 compliant

✔ Uses measured final dimensions

✔ Never derived from stress curve

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full audit traceability

---

End of Document
