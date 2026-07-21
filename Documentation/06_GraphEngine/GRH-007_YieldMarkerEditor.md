# Yield Marker Editor

Document ID : MTDMS-GRH-007

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

This document defines the Yield Marker Editor.

The editor allows the operator to inspect, verify, adjust and approve automatically detected yield points without modifying the raw test data.

This editor is one of the most important quality assurance tools in MTDMS.

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ASTM E111

ISO 17025

---

# Scope

Supported Yield Types

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Rp1.0

Rt0.5

Rt1.0

Custom Offset Yield

---

# Design Philosophy

Automatic Detection

↓

Operator Verification

↓

Approval

↓

Engineering Result

Operator decisions shall always have priority over automatic detection.

---

# Workflow

Import Data

↓

Automatic Yield Detection

↓

Display Marker

↓

Operator Review

↓

Move Marker (Optional)

↓

Approve

↓

Store

---

# Editing Modes

Read Only

Operator

Engineering

Administrator

---

# Marker Selection

Operator clicks

Yield Marker

↓

Marker becomes active

↓

Properties panel displayed

---

# Marker Movement

Marker may only move

along the engineering curve.

Free movement outside the curve

is prohibited.

---

# Snap Algorithm

Marker snaps to

Nearest Sample

or

Interpolated Position

depending on settings.

---

# Interpolation

If interpolation is enabled

marker position is calculated using

Linear Interpolation

between adjacent samples.

Nearest sample mode

may also be selected.

---

# Live Update

During marker movement

software continuously updates

Engineering Stress

Engineering Strain

Force

Extension

Time

Sample Number

---

# Validation Rules

Yield Point

Must occur

After Elastic Region

Before UTS

```
Elastic

↓

Yield

↓

UTS

↓

Fracture
```

---

# Approval

Operator must explicitly approve

the edited marker.

Approval records

Operator Name

Timestamp

Previous Position

New Position

Reason

---

# Reject Operation

Operator may reject

automatic yield detection.

Software shall

recalculate using another method

or

allow complete manual selection.

---

# Undo / Redo

Every movement

supports

Undo

Redo

without recalculation of the raw dataset.

---

# Display

Marker

Large Green Circle

Leader Line

Yield Label

Current Coordinates

---

# Context Menu

Approve

Reject

Reset Automatic

Delete Manual

Copy Coordinates

Properties

---

# Keyboard Shortcuts

Arrow Keys

Fine Adjustment

Ctrl + Arrow

Very Fine Adjustment

Enter

Approve

Esc

Cancel

---

# Database Storage

SQLite

Table

```
tblYieldMarker
```

Fields

MarkerID

Method

OriginalIndex

EditedIndex

OriginalStress

EditedStress

OriginalStrain

EditedStrain

Operator

Timestamp

Approved

Reason

---

# Report Behaviour

Final Report

Displays

Approved Yield Marker

Construction lines

Temporary markers

Editing helpers

shall NOT appear.

---

# Error Handling

Marker Outside Curve

↓

Reject

Marker After UTS

↓

Engineering Error

Marker Before Elastic Region

↓

Engineering Error

Interpolation Failure

↓

Nearest Sample

---

# Future Enhancements

AI Yield Verification

Automatic Confidence Score

Multiple Candidate Detection

Voice Approval

Digital Signature

Reserved

---

# Acceptance Criteria

✔ Supports all yield methods

✔ Marker constrained to curve

✔ Live engineering values

✔ Undo / Redo

✔ Operator approval required

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO 17025 traceability

---

End of Document
