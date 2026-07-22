# Compression Calculation Engine

Document ID : MTDMS-CE-009

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

The Compression Calculation Engine processes compression test data imported from the TXT file and calculates the engineering properties required for compression testing.

The engine supports metallic and non-metallic compression tests.

All calculations are regenerated from the imported TXT file.

---

# Objectives

The Compression Calculation Engine shall

• Calculate compressive stress

• Calculate compressive strain

• Determine compressive strength

• Determine elastic region

• Generate engineering graphs

• Supply validated results

---

# Engineering Philosophy

TXT File

↓

Geometry

↓

Compression Calculation

↓

Validation

↓

Engineering Results

The TXT file is always the engineering source.

---

# Input Data

Force

Displacement

Extension

Time

Specimen Geometry

Material Reference (optional)

Selected Standard

---

# Workflow

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

Maximum Compression

↓

Validation

↓

Engineering Results
```

---

# Engineering Stress

Compressive stress

\[
\sigma_c=\frac{F}{A_0}
\]

where

F = compressive force

A₀ = original cross-sectional area

---

# Engineering Strain

Compressive strain

\[
\varepsilon_c=\frac{\Delta L}{L_0}
\]

Compression is recorded using the convention defined by the selected standard.

Sign convention (positive or negative strain) is configurable according to the calculation profile.

---

# Elastic Region

The elastic region shall be identified using the same methodology as tensile testing where applicable.

The elastic region may be supplied to the Young's Modulus Engine if required by the selected standard.

---

# Maximum Compression

The engine shall determine

Maximum Force

Maximum Compressive Stress

Maximum Compressive Strain

Displacement at Maximum Load

---

# Failure Detection

Where applicable,

the engine shall identify

Specimen Failure

Maximum Load

Test Termination

Machine Limit

Failure criteria depend on the selected calculation profile.

---

# Graph Output

The engine supplies

Stress–Strain Curve

Force–Displacement Curve

Compression Curve

for later visualization.

---

# Material Library

Reference properties

may be used

for comparison only.

Measured values always take precedence.

---

# Engineering Independence

The Compression Calculation Engine

shall never modify

Imported TXT

Original Force

Original Displacement

Original Measurements

Only calculated engineering values are generated.

---

# SQLite Interaction

SQLite stores

Compression Results

Validation Status

Graph Parameters

Metadata

Intermediate calculations are regenerated from the TXT file.

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

Invalid Displacement

↓

Reject

Compression Not Detected

↓

Warning

---

# Performance Targets

Typical Compression Dataset

Calculation

< 500 ms

Validation

< 200 ms

Graph Dataset Generation

< 500 ms

---

# Acceptance Criteria

✔ Compressive stress calculated

✔ Compressive strain calculated

✔ Maximum compression determined

✔ Graph dataset generated

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Supports configurable sign convention

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
