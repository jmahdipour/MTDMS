# Tensile Calculation Engine

Document ID : MTDMS-CE-005

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

The Tensile Calculation Engine converts validated tensile-test data imported from the TXT file into engineering tensile properties.

This module performs the complete engineering calculation workflow for metallic and non-metallic tensile tests.

The calculations are reproducible solely from the imported TXT file and validated specimen geometry.

---

# Objectives

The Tensile Calculation Engine shall

• Calculate engineering stress

• Calculate engineering strain

• Calculate true stress

• Calculate true strain

• Determine tensile properties

• Supply data to graphs

• Supply validated results to reports

---

# Engineering Philosophy

TXT File

↓

Geometry

↓

Engineering Calculation

↓

Validation

↓

Engineering Results

Every calculation starts from the imported TXT file.

No engineering value is reused from previous reports.

---

# Input Data

Force

Displacement

Extension

Time

Gauge Length

Cross-sectional Area

Material Reference (optional)

Selected Standard

---

# Internal Workflow

```
TXT Data

↓

Geometry Verification

↓

Stress Calculation

↓

Strain Calculation

↓

Elastic Region

↓

Yield Detection

↓

Ultimate Strength

↓

Fracture Analysis

↓

True Stress / Strain

↓

Validation

↓

Engineering Results
```

---

# Engineering Stress

Engineering stress is calculated as

\[
\sigma=\frac{F}{A_0}
\]

Where

F = applied force

A₀ = original cross-sectional area

---

# Engineering Strain

Engineering strain is calculated as

\[
\varepsilon=\frac{\Delta L}{L_0}
\]

Where

ΔL = extension

L₀ = original gauge length

---

# True Stress

Before necking

\[
\sigma_t=\sigma(1+\varepsilon)
\]

After necking

the engine shall use the calculation profile defined by the selected standard.

---

# True Strain

\[
\varepsilon_t=\ln(1+\varepsilon)
\]

---

# Elastic Region

The elastic region shall be identified before yield determination.

This region is later used by

Young's Modulus Engine

Graph Correction Engine

Yield Detection Engine

---

# Yield Determination

The Tensile Calculation Engine

does not determine

yield strength directly.

It transfers

validated stress-strain data

to

Yield Detection Engine.

---

# Ultimate Tensile Strength

The engine shall determine

Maximum Force

Maximum Engineering Stress

Maximum True Stress

and their corresponding strain values.

---

# Fracture

The engine shall detect

Fracture Point

Last Valid Data Point

Maximum Extension

Final Gauge Length

where available.

---

# Output Data

Engineering Stress

Engineering Strain

True Stress

True Strain

Maximum Force

Ultimate Tensile Strength

Maximum Extension

Fracture Point

Complete Stress-Strain Dataset

---

# Graph Output

The engine supplies

Stress-Strain Curve

True Stress-Strain Curve

Force-Displacement Curve

for later visualization.

---

# Material Library

Reference values may be used

only

for comparison

or graph correction.

Measured values always take precedence.

---

# Engineering Independence

The engine

never modifies

Imported TXT

Original Measurements

Original Force

Original Extension

Only calculated engineering values are produced.

---

# SQLite Interaction

SQLite stores

Final engineering results

Graphs

Validation status

Metadata

No intermediate calculation states are permanently stored.

---

# Error Handling

Missing Force

↓

Abort

Missing Geometry

↓

Abort

Zero Area

↓

Reject

Invalid Extension

↓

Reject

Fracture Not Found

↓

Warning

---

# Performance Targets

Typical Tensile Dataset

Calculation

< 500 ms

Validation

< 200 ms

Graph Dataset Generation

< 500 ms

---

# Acceptance Criteria

✔ Engineering stress calculated

✔ Engineering strain calculated

✔ True stress calculated

✔ True strain calculated

✔ Ultimate strength determined

✔ Complete graph dataset generated

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 6892-1 compatible

✔ ASTM E8 compatible

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
