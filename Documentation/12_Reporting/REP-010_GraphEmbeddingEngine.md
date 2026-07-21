# Graph Embedding Engine

Document ID : MTDMS-REP-010

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Reporting

Status

Production

---

# Purpose

The Graph Embedding Engine inserts validated engineering graphs into laboratory reports while preserving their engineering integrity and visual quality.

The engine only embeds graphs.

It never redraws graphs.

It never modifies engineering data.

It never recalculates graph coordinates.

---

# Objectives

The module shall

• Embed validated graphs

• Preserve graph quality

• Preserve engineering accuracy

• Preserve aspect ratio

• Preserve readability

• Support multiple graph types

---

# Workflow

```
Validated Graph

↓

Graph Embedding Engine

↓

Report Template

↓

Position Verification

↓

Scaling

↓

Report
```

---

# Supported Graph Types

Engineering Stress – Engineering Strain

True Stress – True Strain

Force – Displacement

Force – Extension

Bending Curve

Spring Curve

Ring Stiffness Curve

Hardness Distribution
(Future)

Custom Graph

---

# Graph Source

Graphs originate only from

Validated Engineering Graph Engine

No graph shall be recreated during report generation.

---

# Engineering Integrity

The following shall remain unchanged

X coordinates

Y coordinates

Axis scaling

Engineering markers

Legend

Units

Titles

---

# Image Formats

Preferred

EMF

WMF

Supported

PNG

JPEG

BMP

SVG
(Future)

Vector formats are recommended whenever available.

---

# Embedding Method

Graphs shall be embedded as

Linked Images

or

Embedded Vector Objects

according to template configuration.

---

# Positioning

Supported

Top

Bottom

Center

Left

Right

Custom Position

Administrator configurable.

---

# Scaling Rules

Maintain

Aspect Ratio

Maintain

Axis Proportion

Maintain

Marker Position

Stretching

Not Allowed

Cropping

Not Allowed

---

# Graph Resolution

Minimum

300 DPI

Recommended

600 DPI

Print quality shall remain readable.

---

# Engineering Markers

The report graph may contain

Yield Point

Ultimate Point

Fracture Point

Proof Strength

Maximum Force

Only

validated

markers shall appear.

---

# Hidden Engineering Objects

The following shall never appear in reports

Temporary construction lines

Operator selection guides

Calibration guides

Debug markers

Interactive cursors

Manual correction helpers

Hidden objects remain available only inside the engineering environment.

---

# Axis Validation

Verify

Axis Labels

Units

Scale

Range

Origin

---

# Graph Validation Before Embedding

Verify

Graph Exists

Graph Approved

Graph Complete

Graph Linked

No Corruption

---

# Report Compatibility

Graphs shall automatically fit

A4 Portrait

A4 Landscape

Letter

Legal

Custom layouts

without engineering distortion.

---

# Multi-Graph Reports

Supported

One Graph

Two Graphs

Multiple Graphs

Administrator configurable.

---

# SQLite Database

Tables

```
tblEmbeddedGraph

tblGraphLayout

tblGraphHistory
```

---

# Audit Trail

Record

Certificate Number

Graph Type

Template

Operator

Timestamp

Embedding Result

Revision

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Reviewer

View

Operator

Generate

---

# Error Handling

Missing Graph

↓

Abort

Corrupted Image

↓

Abort

Invalid Resolution

↓

Warning

Unsupported Format

↓

Convert if possible

Otherwise

Abort

---

# Future Enhancements

Vector PDF Embedding

Interactive Electronic Reports

High-DPI Scaling

Automatic Graph Layout Optimization

Reserved

---

# Acceptance Criteria

✔ Engineering graph unchanged

✔ Aspect ratio preserved

✔ Hidden engineering objects removed

✔ Multiple graph layouts supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
