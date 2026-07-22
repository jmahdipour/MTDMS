# Four-Point Bending Calculation Engine

Document ID : MTDMS-CE-011

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

The Four-Point Bending Calculation Engine processes data imported from the machine TXT file and calculates engineering properties for specimens tested under a four-point bending configuration.

The engine performs calculations using validated specimen geometry and loading span information.

---

# Objectives

The Four-Point Bending Calculation Engine shall

• Calculate flexural stress

• Calculate flexural strain

• Determine maximum bending load

• Determine maximum flexural strength

• Generate engineering graphs

• Supply validated engineering results

---

# Engineering Philosophy

TXT File

↓

Geometry

↓

Four-Point Bending Calculation

↓

Validation

↓

Engineering Results

The imported TXT file is always the engineering source.

---

# Input Data

Force

Displacement

Time

Specimen Width

Specimen Thickness

Outer Span

Inner Span

Material Reference (optional)

Selected Standard

---

# Workflow

```
TXT Data

↓

Geometry Verification

↓

Span Verification

↓

Flexural Stress

↓

Flexural Strain

↓

Maximum Load

↓

Validation

↓

Engineering Results
```

---

# Specimen Geometry

Default implementation assumes a rectangular specimen.

Additional geometries may be introduced through future calculation profiles.

---

# Flexural Stress

The calculation shall follow the formula required by the selected standard.

Typical rectangular beam relationship

\[
\sigma_f=f(F,L,a,b,h)
\]

where

F = applied load

L = outer support span

a = loading span

b = specimen width

h = specimen thickness

The exact formulation depends on the selected standard and calculation profile.

---

# Flexural Strain

The calculation shall follow the selected engineering standard.

The engine shall use

Measured Displacement

Specimen Thickness

Support Geometry

to determine engineering flexural strain.

---

# Maximum Load

The engine shall determine

Maximum Force

Maximum Flexural Stress

Maximum Flexural Strain

Maximum Deflection

---

# Elastic Region

If required,

the engine shall identify the elastic portion of the bending curve and supply it to the Young's Modulus Engine.

---

# Graph Output

The engine supplies

Force–Displacement Curve

Flexural Stress–Strain Curve

Four-Point Bending Curve

for later visualization.

---

# Material Library

Reference material properties

may be used

only

for engineering comparison.

Measured values always have priority.

---

# Engineering Independence

The Four-Point Bending Calculation Engine

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

Intermediate calculations are regenerated whenever the TXT file is processed.

---

# Error Handling

Missing Outer Span

↓

Abort

Missing Inner Span

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

Typical Four-Point Bending Dataset

Calculation

< 500 ms

Validation

< 200 ms

Graph Dataset Generation

< 500 ms

---

# Acceptance Criteria

✔ Four-point bending supported

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
