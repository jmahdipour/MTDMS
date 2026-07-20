# Engineering Calculation Pipeline

Document ID : MTDMS-ENG-002

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Engineering Core

---

# Purpose

This document defines the complete engineering calculation sequence.

Every calculation inside MTDMS shall follow this pipeline.

Changing the order is prohibited because later calculations depend on previous validated results.

---

# Design Philosophy

Validated Raw Data

↓

Engineering Data

↓

Material Properties

↓

Mechanical Calculations

↓

Verification

↓

Results

---

# Pipeline Overview

```
Import

↓

Raw Data

↓

Geometry

↓

Engineering Stress

↓

Engineering Strain

↓

Elastic Region

↓

Young's Modulus

↓

Yield Detection

↓

Rp / Rt

↓

Ultimate Strength

↓

True Stress

↓

True Strain

↓

Fracture

↓

Elongation

↓

Reduction of Area

↓

Statistics

↓

Validation

↓

Database

↓

Graphs

↓

Reports
```

---

# Stage 1

Geometry

Input

Diameter

Width

Thickness

Gauge Length

Area

Output

Validated Geometry

---

# Stage 2

Engineering Stress

Formula

σ = F / A₀

Input

Force

Original Area

Output

Engineering Stress

---

# Stage 3

Engineering Strain

Formula

ε = ΔL / L₀

Input

Extension

Original Gauge Length

Output

Engineering Strain

---

# Stage 4

Elastic Region Detection

Determine

Best Linear Region

↓

Regression

↓

Candidate Elastic Zone

Output

Elastic Region

---

# Stage 5

Young's Modulus

Linear Regression

↓

Slope

↓

Young's Modulus

Output

E

---

# Stage 6

Graph Correction

Use

Reference Young's Modulus

↓

Horizontal Axis Correction

↓

Display Only

Raw engineering values

Never modified.

---

# Stage 7

Yield Detection

Methods

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Rp0.05

Rt

Manual Yield

Output

Yield Point

Yield Stress

Yield Strain

---

# Stage 8

Ultimate Tensile Strength

Maximum Engineering Stress

↓

UTS

---

# Stage 9

True Stress

Engineering Stress

↓

True Stress

---

# Stage 10

True Strain

Engineering Strain

↓

True Strain

---

# Stage 11

Fracture Detection

Locate

Maximum Extension

↓

Fracture Point

↓

Stop Calculations

---

# Stage 12

Elongation

Original Length

↓

Final Length

↓

Percent Elongation

---

# Stage 13

Reduction of Area

Original Area

↓

Final Area

↓

Reduction %

---

# Stage 14

Statistics

Average

Minimum

Maximum

Standard Deviation

Coefficient of Variation

---

# Stage 15

Engineering Validation

Check

Yield

Ultimate

Fracture

Modulus

Consistency

↓

PASS

WARNING

FAIL

---

# Stage 16

Storage

Engineering Results

↓

SQLite

↓

Audit

---

# Stage 17

Graph Generation

Engineering Dataset

↓

Graph Engine

↓

Interactive Graph

---

# Stage 18

Report Generation

Engineering Results

↓

Certificate

↓

PDF

↓

Excel

---

# Dependency Rules

Geometry

↓

Stress

↓

Elastic Region

↓

Young

↓

Yield

↓

True Stress

↓

Fracture

Later stages may never execute before prerequisite stages.

---

# Failure Handling

Failure

↓

Stop Current Stage

↓

Log Error

↓

Rollback Engineering

↓

Keep Raw Data

---

# Acceptance Criteria

✔ Deterministic calculation order

✔ No skipped stages

✔ No circular dependency

✔ Raw Data preserved

✔ Engineering Results reproducible

✔ SQLite compatible

✔ Excel 2019 compatible

---

End of Document
