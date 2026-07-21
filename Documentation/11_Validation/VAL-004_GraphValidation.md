# Graph Validation

Document ID : MTDMS-VAL-004

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Validation

Status

Production

---

# Purpose

The Graph Validation module verifies that every graph generated from imported test data accurately represents the engineering dataset.

This module validates graphical consistency only.

It never changes engineering calculations.

It never modifies imported data.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ASTM E8/E8M

Applicable product standards

---

# Objectives

The module shall

• Verify graph completeness

• Verify graph consistency

• Verify axis configuration

• Verify engineering markers

• Detect graphical anomalies

• Prevent invalid reports

---

# Scope

Validation applies to

Stress–Strain Graph

Force–Displacement Graph

Force–Extension Graph

Engineering Stress–Engineering Strain

True Stress–True Strain

Bending Curves

Spring Curves

Ring Stiffness Curves

Future Graph Types

---

# Validation Workflow

Engineering Dataset

↓

Graph Engine

↓

Generated Graph

↓

Graph Validation

↓

PASS

WARNING

FAIL

↓

Report Engine

---

# General Validation

Verify

Graph Exists

Graph Generated Successfully

No Missing Data

No Empty Plot

Data Count Matches Dataset

---

# Axis Validation

Verify

Horizontal Axis Defined

Vertical Axis Defined

Axis Labels

Axis Units

Axis Scale

Axis Direction

---

# Unit Validation

Examples

Stress

MPa

Force

N

kN

kgf

Length

mm

Time

s

Unknown unit

↓

WARNING

---

# Dataset Consistency

Verify

Graph Point Count

=

Imported Dataset Count

No Missing Points

No Duplicate Points

Ordered Sequence

---

# Engineering Marker Validation

Verify

Yield Point

Ultimate Point

Fracture Point

Maximum Force

Offset Yield

Manual Marker (if used)

---

# Manual Marker Validation

If operator manually selects

Yield Point

Fracture Point

Elastic Region

the graph shall record

Marker Position

User

Date

Time

Reason

The original imported dataset shall remain unchanged.

---

# Graph Range Validation

Verify

Minimum Value

Maximum Value

Visible Data Range

No Truncated Graph

No Hidden Data

---

# Scale Validation

Verify

Automatic Scale

Manual Scale

Log Scale (if supported)

Zero Position

---

# Annotation Validation

Verify

Legends

Titles

Axis Names

Material Name

Certificate Number

Revision

---

# Image Quality Validation

Verify

Resolution

Minimum Size

Visible Text

Readable Grid

No Clipping

---

# Report Compatibility

Verify

Graph fits report template

Margins

Orientation

Scaling

Print Area

PDF Area

---

# Validation Results

PASS

PASS WITH WARNING

FAIL

MANUAL REVIEW REQUIRED

---

# Warning Examples

Manual Yield Selection

Auto Scale Changed

Missing Legend

Large Dataset Simplification

---

# Failure Examples

Missing Graph

Missing Fracture Point

Invalid Axis

Zero-Length Graph

Corrupted Rendering

Dataset Mismatch

---

# SQLite Database

Tables

```
tblGraphValidation

tblGraphValidationHistory

tblGraphMarker
```

---

# Audit Trail

Every validation records

Validation ID

Graph Type

Certificate Number

Revision

Operator

Timestamp

Validation Result

Reviewer

---

# Permissions

Administrator

Full Access

Reviewer

Approve Warning

Operator

View Results

---

# Error Handling

Graph Generation Failed

↓

FAIL

Missing Dataset

↓

FAIL

Marker Outside Range

↓

WARNING

Axis Undefined

↓

FAIL

---

# Future Enhancements

Automatic Graph Quality Analysis

AI Curve Inspection

Automatic Marker Verification

Interactive Validation Dashboard

Reserved

---

# Acceptance Criteria

✔ Graph consistency verified

✔ Engineering markers verified

✔ Dataset consistency verified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations never modified

✔ No communication with testing machine

✔ ISO/IEC 17025 compliant

---

End of Document
