# Curve Correction Engine

Document ID : MTDMS-GRH-005

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Graph Engine

Status

Production

---

# Purpose

This document defines the Curve Correction Engine used for graphical correction of engineering curves.

The correction engine improves the visual representation of tensile curves without modifying the original imported data or engineering calculations.

This module is intended for

• Young's Modulus correction

• Compliance correction

• Zero correction

• Graph alignment

• Engineering visualization

Only the displayed graph is modified.

---

# Scope

The Curve Correction Engine shall

Correct

Display Data

Only.

It shall never modify

Raw TXT Data

Imported Database

Engineering Results

Stress Values

Force Values

Original Arrays

---

# Supported Corrections

Elastic Region Correction

Young's Modulus Correction

Machine Compliance Compensation

Grip Compliance Compensation

Zero Shift Correction

Axis Offset

Horizontal Scaling

Vertical Offset

Future

Polynomial Correction

Spline Correction

Reserved

---

# Architecture

Engineering Data

↓

Correction Engine

↓

Corrected Dataset

↓

Graph Renderer

↓

Display

Original Dataset

remains untouched.

---

# Correction Pipeline

Load Dataset

↓

Read Material Library

↓

Read Engineering Results

↓

Select Correction Method

↓

Generate Corrected Dataset

↓

Render Graph

---

# Data Model

Original Dataset

Read Only

Corrected Dataset

Temporary

Memory Only

---

# Original Dataset

Contains

Engineering Stress

Engineering Strain

Engineering Force

Engineering Extension

Engineering Time

---

# Corrected Dataset

Contains

Corrected X Coordinates

Original Y Coordinates

Only X values may change.

---

# Young's Modulus Correction

Reference

Document

```
ENG-028
```

Correction uses

Measured Young

Reference Young

Correction Factor

---

# Compliance Compensation

Machine deformation may be estimated by

```
ΔLmachine

=

F / Kmachine
```

Where

Kmachine

Machine stiffness

The compensated displacement becomes

```
ΔLcorrected

=

ΔLmeasured

−

ΔLmachine
```

---

# Zero Correction

If initial force

or displacement

is not zero

↓

Apply Offset

↓

Shift Entire Dataset

Original data remain unchanged.

---

# Horizontal Scaling

Applies only to

Display Coordinates.

Stress values

remain identical.

---

# Vertical Offset

Allowed only

for visualization.

Engineering stress

shall never change.

---

# Correction Methods

Method 1

Young's Modulus

Method 2

Machine Compliance

Method 3

Grip Compliance

Method 4

Manual Shift

Method 5

Combined

---

# Multiple Corrections

Corrections are applied in sequence

Zero Correction

↓

Compliance

↓

Young Correction

↓

Manual Adjustment

---

# Operator Controls

Enable Correction

Disable Correction

Preview Correction

Compare

Original

Corrected

Overlay

Reset

---

# Graph Modes

Original

Corrected

Overlay

Split View

---

# Preview Mode

Operator may compare

Original

and

Corrected

simultaneously.

---

# Undo

Every correction

supports

Undo

Redo

without affecting engineering calculations.

---

# SQLite Storage

Table

```
tblGraphCorrection
```

Fields

CorrectionID

CorrectionMethod

CorrectionFactor

MachineCompliance

GripCompliance

Operator

Timestamp

Enabled

---

# Performance

Correction

shall complete

before rendering.

Target

100000 Samples

Processing Time

<500 ms

---

# Error Handling

Missing Young

↓

Skip Correction

Invalid Compliance

↓

Ignore

Overflow

↓

Abort

Rollback

Negative Scale

↓

Reject

---

# Future Enhancements

Adaptive Compliance Learning

Automatic Machine Calibration

Artificial Intelligence Correction

Polynomial Warp

Digital Image Correlation Alignment

Reserved

---

# Acceptance Criteria

✔ Original data preserved

✔ Engineering calculations unchanged

✔ Multiple correction methods supported

✔ Overlay comparison supported

✔ Undo / Redo supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 17025 traceable

---

End of Document
