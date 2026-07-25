# Engineering Yield Point Identification Engine

Document ID : MTDMS-GE-018

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Chart Technology

Microsoft Excel Chart Objects

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Yield Point Identification Engine is responsible for locating, displaying, validating, and allowing manual confirmation of yield-related points on engineering graphs generated from tensile test data.

The engine does **not** calculate the yield strength itself.

Yield calculations are performed by the Calculation Engine.

This module provides graphical identification and operator interaction only.

---

# Objectives

The Yield Point Identification Engine shall

• Display calculated yield locations

• Allow manual confirmation

• Support multiple yield definitions

• Maintain engineering traceability

• Preserve original engineering results

---

# Engineering Philosophy

TXT File

↓

Engineering Calculation

↓

Yield Result

↓

Yield Identification

↓

Operator Verification

↓

Engineering Report

Yield visualization never modifies the engineering calculation.

---

# Supported Yield Definitions

Upper Yield Strength

Lower Yield Strength

Rp0.2

Rp0.1

Rp0.5

Rt0.5

Rt1.0

Administrator configurable.

The available definitions depend on the selected test standard.

---

# Workflow

```
Engineering Dataset

↓

Calculation Engine

↓

Yield Candidate

↓

Graph Display

↓

Operator Verification

↓

Approved Marker
```

---

# Automatic Identification

The graph shall display the yield point determined by the Calculation Engine.

Automatic identification includes

Yield Marker

Reference Label

Engineering Coordinates

Associated Stress

Associated Strain

---

# Manual Verification

The operator may

Accept

Move

Replace

Reject

the displayed yield marker.

The original calculated value remains stored.

The operator-adjusted position is stored separately.

---

# Manual Selection Rules

Manual selection shall snap to the nearest measured point.

Interpolation is optional and disabled by default.

The operator cannot place a yield marker outside the measured dataset.

---

# Multiple Yield Markers

The graph may display

Calculated Yield

Operator Yield

Reference Offset Line

Reference Elastic Line

Each marker uses a different graphical style.

---

# Offset Line Display

For proof stress methods

(Rp0.2, Rp0.1, etc.)

the engine may display

Elastic Regression Line

Offset Line

Intersection Point

These construction lines are hidden from reports unless enabled.

---

# Engineering Information Window

Selecting the yield marker displays

Stress

Strain

Force

Extension

Displacement

Calculation Method

Validation Status

Operator Confirmation

---

# Report Behaviour

Only the approved yield marker is inserted into

Reports

Certificates

PDF

Temporary construction lines remain hidden.

---

# Engineering Independence

The Yield Point Identification Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It manages graphical verification only.

---

# SQLite Interaction

SQLite stores

Calculated Yield Position

Operator Yield Position

Selection Method

Approval Status

Operator

Timestamp

Engineering calculations remain unchanged.

---

# Error Handling

No Yield Found

↓

Warning

Multiple Candidates

↓

Operator Selection

Marker Outside Dataset

↓

Reject

Invalid Offset Method

↓

Abort

---

# Performance Targets

Yield Display

Immediate

Marker Move

< 20 ms

Approval

< 20 ms

---

# Acceptance Criteria

✔ Multiple yield definitions supported

✔ Automatic identification supported

✔ Manual confirmation supported

✔ Operator adjustments logged

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT

---

End of Document
