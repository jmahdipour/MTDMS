# Ring Stiffness Calculation Engine

Document ID : MTDMS-CE-013

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

The Ring Stiffness Calculation Engine determines the instantaneous ring stiffness of thermoplastic pipes from force–displacement data imported from the testing machine TXT file.

The engine is intended for corrugated and solid-wall plastic pipes tested according to the selected standard.

The calculation is performed entirely from the imported TXT data.

---

# Objectives

The Ring Stiffness Calculation Engine shall

• Calculate ring stiffness

• Determine the reference deformation

• Validate the measurement

• Generate engineering graphs

• Supply validated engineering results

---

# Engineering Philosophy

TXT File

↓

Pipe Geometry

↓

Force–Displacement Data

↓

Reference Deformation

↓

Ring Stiffness

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

Outside Diameter

Pipe Length

Wall Thickness (optional)

Selected Standard

Material Reference (optional)

---

# Workflow

```
TXT Data

↓

Geometry Verification

↓

Reference Diameter

↓

Reference Deflection

↓

Force Evaluation

↓

Ring Stiffness

↓

Validation

↓

Engineering Results
```

---

# Reference Deformation

The reference deformation shall be determined according to the selected standard.

Typical value

3% of the mean inside or outside diameter

depending on the applicable standard.

The exact percentage is obtained from the selected calculation profile.

---

# Ring Stiffness

The Ring Stiffness Engine shall calculate

Instantaneous Ring Stiffness

using the force corresponding to the reference deformation.

The mathematical formulation shall be determined by the selected standard.

No hardcoded formula shall exist inside the calculation workflow.

---

# Output Data

Reference Diameter

Reference Deflection

Reference Force

Ring Stiffness

Maximum Force

Maximum Deflection

Validation Status

---

# Geometry Verification

The engine shall verify

Outside Diameter

Pipe Length

Wall Thickness (if required)

Specimen Type

---

# Graph Output

The engine supplies

Force–Displacement Curve

Reference Deformation Marker

Reference Force Marker

Ring Stiffness Annotation

for later visualization.

---

# Material Library

Reference properties

may be used

only

for engineering comparison.

Measured values always take priority.

---

# Engineering Independence

The Ring Stiffness Calculation Engine

shall never modify

Imported TXT

Original Force

Original Displacement

Original Measurements

Only calculated engineering values are generated.

---

# SQLite Interaction

SQLite stores

Ring Stiffness

Reference Force

Reference Deformation

Validation Status

Graph Parameters

Metadata

Intermediate calculations are regenerated from the TXT file.

---

# Error Handling

Missing Diameter

↓

Abort

Missing Force

↓

Abort

Reference Deformation Not Found

↓

Reject

Pipe Geometry Invalid

↓

Reject

Maximum Force Not Found

↓

Warning

---

# Performance Targets

Typical Ring Stiffness Dataset

Calculation

< 300 ms

Validation

< 100 ms

Graph Dataset Generation

< 300 ms

---

# Acceptance Criteria

✔ Instantaneous ring stiffness calculated

✔ Reference deformation determined

✔ Reference force determined

✔ Graph dataset generated

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
