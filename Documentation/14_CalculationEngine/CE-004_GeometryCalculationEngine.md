# Geometry Calculation Engine

Document ID : MTDMS-CE-004

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

The Geometry Calculation Engine determines all specimen geometric properties required before engineering calculations begin.

These values are derived from the imported TXT file and, where required, operator-entered dimensions.

The calculated geometry is then supplied to the Engineering Calculation Engine.

---

# Objectives

The Geometry Calculation Engine shall

• Determine specimen geometry

• Calculate cross-sectional area

• Validate dimensions

• Support multiple specimen shapes

• Supply geometry to all calculation modules

---

# Engineering Philosophy

TXT File

↓

Imported Dimensions

↓

Geometry Engine

↓

Validated Geometry

↓

Engineering Calculation

Engineering calculations shall never estimate specimen geometry.

Geometry shall be explicitly calculated before any stress or strain calculation.

---

# Supported Specimen Types

Round specimen

Flat specimen

Pipe specimen

Wire

Spring wire

Rectangular section

Custom section

Administrator configurable.

---

# Geometry Sources

The engine may obtain dimensions from

TXT metadata

Operator input

Material Library (reference only)

Configuration defaults

Operator-entered values always take precedence over defaults.

---

# Required Dimensions

## Round Specimen

Diameter

Gauge Length

---

## Flat Specimen

Width

Thickness

Gauge Length

---

## Pipe Specimen

Outside Diameter

Wall Thickness

Gauge Length

---

## Spring

Wire Diameter

Mean Coil Diameter

Number of Active Coils (optional)

---

## Ring Stiffness

Outside Diameter

Wall Thickness

Specimen Length

---

# Cross-Section Calculation

Round specimen

\[
A=\frac{\pi d^2}{4}
\]

Flat specimen

\[
A=b\times t
\]

Pipe specimen

\[
A=\frac{\pi}{4}(D^2-d^2)
\]

where

D = outside diameter

d = inside diameter

---

# Secondary Dimensions

The engine may also calculate

Radius

Inside Diameter

Hydraulic Area

Perimeter

Moment of Inertia (future)

Section Modulus (future)

---

# Gauge Length

The engine stores

Initial Gauge Length

Final Gauge Length

Operator Secondary Gauge Length

Secondary Gauge Length is used only where required by the selected calculation profile.

---

# Validation Rules

Dimensions

must be

Positive

Non-zero

Within machine capability

Consistent with specimen type

---

# Manual Editing

The operator may edit

Diameter

Width

Thickness

Gauge Length

only before engineering calculations begin.

Any modification shall be recorded in the audit trail.

---

# Engineering Independence

Geometry calculations

shall never modify

Imported TXT

Original dimensions

Only the internal geometry model is updated.

---

# SQLite Interaction

SQLite stores

Calculated geometry

for traceability only.

Geometry is recalculated whenever the TXT file is processed again.

---

# Error Handling

Missing Diameter

↓

Abort

Missing Thickness

↓

Abort

Negative Dimension

↓

Reject

Zero Area

↓

Reject

Invalid Specimen Type

↓

Reject

---

# Performance Targets

Geometry Calculation

< 20 ms

Validation

< 20 ms

Typical Geometry Processing

< 50 ms

---

# Acceptance Criteria

✔ Round specimen supported

✔ Flat specimen supported

✔ Pipe specimen supported

✔ Cross-sectional area calculated correctly

✔ Manual dimensions supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
