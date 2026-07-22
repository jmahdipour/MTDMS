# Three-Point Bending Calculation Engine

Document ID : MTDMS-CE-010

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Input

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Three-Point Bending Calculation Engine processes bending test data imported from the TXT file and calculates engineering bending properties for specimens tested under a three-point loading configuration.

The engine performs all calculations directly from the imported machine data and validated specimen geometry.

---

# Objectives

The Three-Point Bending Calculation Engine shall

• Calculate bending stress

• Calculate bending strain

• Determine maximum bending load

• Determine flexural strength

• Generate engineering graphs

• Supply validated engineering results

---

# Engineering Philosophy

TXT File

↓

Geometry

↓

Three-Point Bending Calculation

↓

Validation

↓

Engineering Results

The TXT file is always the engineering source.

---

# Input Data

Force

Displacement

Time

Specimen Width

Specimen Thickness

Support Span

Material Reference (optional)

Selected Standard

---

# Workflow

```
TXT Data

↓

Geometry Verification

↓

Support Span Verification

↓

Bending Stress

↓

Bending Strain

↓

Maximum Load

↓

Validation

↓

Engineering Results
```

---

# Rectangular Specimen

The standard implementation assumes a rectangular cross-section unless another specimen profile is selected.

---

# Flexural Stress

For a rectangular specimen

\[
\sigma_f=\frac{3FL}{2bh^2}
\]

where

F = applied load

L = support span

b = specimen width

h = specimen thickness

---

# Flexural Strain

For a rectangular specimen

\[
\varepsilon_f=\frac{6Dh}{L^2}
\]

where

D = midpoint displacement

---

# Maximum Load

The engine shall determine

Maximum Force

Maximum Flexural Stress

Maximum Flexural Strain

Maximum Deflection

---

# Elastic Region

If required by the selected standard,

the elastic portion of the bending curve shall be identified and supplied to the Young's Modulus Engine.

---

# Graph Output

The engine supplies

Force–Displacement Curve

Flexural Stress–Strain Curve

for later visualization.

---

# Material Library

Reference values

may be used

for comparison only.

Measured values always take precedence.

---

# Engineering Independence

The Three-Point Bending Calculation Engine

shall never modify

Imported TXT

Original Force

Original Displacement

Original Measurements

Only calculated engineering values are generated.

---

# SQLite Interaction

SQLite stores

Flexural Results

Validation Status

Graph Parameters

Metadata

Intermediate calculations are regenerated from the TXT file.

---

# Error Handling

Missing Span

↓

Abort

Missing Width

↓

Abort

Missing Thickness

↓

Abort

Invalid Geometry

↓

Reject

Maximum Load Not Found

↓

Warning

---

# Performance Targets

Typical Three-Point Bending Dataset

Calculation

< 500 ms

Validation

< 200 ms

Graph Dataset Generation

< 500 ms

---

# Acceptance Criteria

✔ Flexural stress calculated

✔ Flexural strain calculated

✔ Maximum load determined

✔ Graph dataset generated

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
