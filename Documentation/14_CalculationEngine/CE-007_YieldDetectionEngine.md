# Yield Detection Engine

Document ID : MTDMS-CE-007

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

The Yield Detection Engine identifies the yield point of a specimen from the engineering stress–strain data generated from the imported TXT file.

This module supports both automatic and manual yield determination according to the selected standard and material type.

The Yield Detection Engine does **not** modify the engineering data. It determines the yield location and stores the result.

---

# Objectives

The Yield Detection Engine shall

• Detect the yield point automatically

• Support manual correction

• Support multiple yield definitions

• Validate the selected yield point

• Supply yield data to reports and graph correction

---

# Engineering Philosophy

TXT File

↓

Engineering Stress–Strain

↓

Elastic Region

↓

Yield Detection

↓

Validation

↓

Engineering Results

Yield determination is always based on the measured data.

Reference material properties are used only for guidance.

---

# Supported Yield Definitions

The engine shall support the following methods.

### Upper Yield Strength

ReH

---

### Lower Yield Strength

ReL

---

### Proof Stress

Rp0.2

---

### Proof Stress

Rp0.1

---

### Total Extension Proof Stress

Rt0.5

---

### User Defined Offset

Administrator configurable.

---

# Automatic Detection

Automatic detection shall use

Stress

Strain

Elastic Region

Young's Modulus

Selected Standard

Material Reference (optional)

to determine the engineering yield point.

---

# Manual Yield Selection

The operator may manually select a yield point directly on the stress–strain graph.

The selected point shall be recorded together with

Operator

Date

Time

Reason

The automatic result shall remain available for comparison.

---

# Reference Material Guidance

If a material reference exists

the engine may define a search window.

Example

Reference Yield Strength

±20%

This guidance does not alter the measured result.

---

# Validation Rules

The detected yield point shall

occur after the elastic region

occur before the ultimate tensile strength

have increasing strain

have positive stress

comply with the selected standard

---

# Output Data

Yield Method

Yield Stress

Yield Strain

Yield Force

Yield Extension

Automatic / Manual Flag

Operator Information (if manual)

Validation Status

---

# Graph Interaction

The Yield Detection Engine provides

Yield Marker

Yield Coordinates

Yield Label

to the Graph Engine.

Construction lines used during automatic detection shall not appear in the final report.

---

# Engineering Independence

The Yield Detection Engine

shall never modify

Imported TXT

Engineering Stress

Engineering Strain

Young's Modulus

Only the yield location is identified.

---

# SQLite Interaction

SQLite stores

Yield Method

Yield Stress

Yield Strain

Selection Method

Validation Status

Operator Information

---

# Error Handling

Yield Not Found

↓

Warning

Multiple Yield Candidates

↓

Select Best Candidate

Manual Selection Outside Valid Region

↓

Reject

Invalid Offset

↓

Reject

---

# Performance Targets

Automatic Detection

< 200 ms

Manual Selection

Immediate

Validation

< 50 ms

---

# Acceptance Criteria

✔ ReH supported

✔ ReL supported

✔ Rp0.2 supported

✔ Rp0.1 supported

✔ Rt0.5 supported

✔ Manual correction supported

✔ Automatic and manual comparison supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 6892-1 compatible

✔ ASTM E8 compatible

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
