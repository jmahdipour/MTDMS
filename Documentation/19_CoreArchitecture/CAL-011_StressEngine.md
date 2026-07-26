# Stress Calculation Engine

Document ID

MTDMS-CAL-011

Version

1.0

Status

Core Engine

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Dependencies

EngineeringDataset

---

# Purpose

Stress Engine calculates engineering stress for every sampled point.

It is the first engineering calculation performed after preprocessing.

The engine uses only raw force values and specimen cross-sectional area.

---

# Formula

Engineering Stress

σ = F / A

where

σ = Engineering Stress

F = Force

A = Initial Cross Section Area

---

# Units

## Force

Input

kgf

(Current TXT format)

---

## Area

Input

mm²

---

## Output

Engineering Stress

kgf/mm²

---

# Internal Rule

Stress Engine shall NOT convert units.

Force remains

kgf

Area remains

mm²

Conversion to MPa is performed only if requested by report settings.

---

# Inputs

EngineeringDataset.Raw.Force()

EngineeringDataset.Metadata.Area

---

# Outputs

EngineeringDataset.Calc.Stress()

---

# Preconditions

Dataset Imported

Dataset Validated

Area > 0

Force Array Exists

---

# Processing Algorithm

For every point

Stress(i)=Force(i)/Area

No smoothing

No filtering

No interpolation

---

# Pseudocode

For i = 1 To PointCount

    Stress(i)=Force(i)/Area

Next

---

# Output Array

Index

↓

Stress(i)

Array length shall always equal Force array length.

---

# Invalid Area

Area <=0

↓

Fatal Error

Calculation aborted.

---

# Invalid Force

If Force(i) is invalid

↓

Stress(i)=NaN

↓

Flag Invalid Point

Continue calculation.

---

# Memory Policy

Input arrays remain unchanged.

Only

Calc.Stress()

is written.

---

# Performance

Complexity

O(n)

Memory

One Double Array

---

# Error Codes

1101

Area Missing

1102

Area Zero

1103

Force Array Missing

1104

Array Length Mismatch

---

# Validation

Check

Stress Array Length

Maximum Stress

Minimum Stress

NaN Count

Negative Values

---

# Engineering Rule

Stress Engine shall never

detect yield

calculate modulus

correct graph

detect fracture

Those belong to other engines.

---

# Unit Tests

Case 1

Area=100

Force=500

Stress=5

PASS

-----------------------

Case 2

Area=0

Abort

PASS

-----------------------

Case 3

Negative Force

Stress Negative

PASS

---

# Acceptance Criteria

✔ Array Based

✔ O(n)

✔ Double Precision

✔ No Worksheet Access

✔ No TXT Access

✔ No SQLite Access

✔ No Unit Conversion

✔ ISO 17025 Compatible

---

# Related Documents

CAL-012_StrainEngine

CAL-013_YoungModulusEngine

CAL-014_YieldEngine

---

End Of Document
