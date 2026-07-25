# Graph Coordinate Inspection Engine

Document ID : MTDMS-GE-006

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

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Graph Coordinate Inspection Engine provides precise engineering coordinate inspection on all graphs generated from the imported TXT file.

It allows the operator to examine any point on a graph without modifying engineering data.

The inspection process is read-only.

---

# Objectives

The Coordinate Inspection Engine shall

• Display engineering coordinates

• Display engineering values

• Support cursor tracking

• Support engineering inspection

• Preserve engineering integrity

---

# Engineering Philosophy

Engineering Dataset

↓

Graph

↓

Coordinate Inspection

↓

Engineering Review

Inspection never changes engineering results.

---

# Supported Graphs

Stress–Strain

True Stress–Strain

Force–Displacement

Force–Time

Extension–Time

Compression Curve

Spring Curve

Ring Stiffness Curve

Bending Curves

Administrator configurable.

---

# Cursor Tracking

Moving the mouse over a graph shall continuously display

Graph X

Graph Y

Nearest Data Point

Distance to Cursor

Engineering Coordinates

---

# Displayed Values

Depending on graph type

the inspection window may display

Time

Force

Stress

True Stress

Strain

True Strain

Extension

Displacement

Calculated Engineering Values

Validation Status

---

# Nearest Point Search

The engine shall locate

the nearest measured point

rather than using interpolated values

unless interpolation is explicitly enabled.

Administrator configurable.

---

# Interpolation

Supported

Disabled (default)

Linear

Spline (future)

Engineering reports always use measured data.

---

# Precision

Displayed values shall preserve

full engineering precision.

Graph labels may display fewer decimals,

but the inspection window shall always use the original calculated values.

---

# Inspection Window

The inspection panel may include

Coordinate

Engineering Values

Material

Test ID

Point Number

Validation Flag

Reference Value

---

# Snap Mode

Supported

Free Cursor

Nearest Point

Nearest Marker

Administrator configurable.

---

# Crosshair

Optional

Horizontal Guide

Vertical Guide

Both

Administrator configurable.

---

# Keyboard Navigation

Optional

Previous Point

Next Point

Previous Marker

Next Marker

Zoom Center

Administrator configurable.

---

# Engineering Independence

The Coordinate Inspection Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Markers

Validation Results

Inspection is completely read-only.

---

# SQLite Interaction

SQLite stores

Inspection History (optional)

Operator

Timestamp

Graph

Point Number

Engineering data remain unchanged.

---

# Error Handling

No Dataset

↓

Abort

Graph Missing

↓

Abort

Point Not Found

↓

Ignore

Invalid Coordinate

↓

Ignore

---

# Performance Targets

Cursor Update

Immediate

Nearest Point Search

< 10 ms

Inspection Window Refresh

< 20 ms

---

# Acceptance Criteria

✔ Real-time coordinate inspection

✔ Nearest-point search supported

✔ Full engineering precision displayed

✔ Crosshair supported

✔ Snap mode supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Read-only operation

✔ ISO/IEC 17025 compliant

✔ Complete engineering traceability

---

End of Document
