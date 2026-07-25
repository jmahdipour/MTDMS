# Engineering Zoom & Pan Engine

Document ID : MTDMS-GE-007

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

The Engineering Zoom & Pan Engine provides controlled navigation within engineering charts generated from validated datasets.

The engine enables detailed inspection of engineering curves without altering the underlying engineering data.

---

# Objectives

The Zoom & Pan Engine shall

• Zoom into engineering graphs

• Pan graph views

• Reset graph view

• Preserve engineering scale

• Improve engineering inspection

---

# Engineering Philosophy

Engineering Dataset

↓

Graph

↓

Zoom / Pan

↓

Inspection

↓

Engineering Decision

Navigation affects only visualization.

Engineering data remain unchanged.

---

# Supported Operations

Mouse Wheel Zoom

Selection Zoom

Zoom In

Zoom Out

Pan

Reset View

Fit Entire Dataset

Administrator configurable.

---

# Zoom Modes

### Automatic Zoom

Entire dataset visible.

---

### Region Zoom

Operator selects a rectangular area.

The chart scales to the selected region.

---

### Axis Zoom

Horizontal only

Vertical only

Both

Administrator configurable.

---

# Pan Modes

Supported

Horizontal

Vertical

Both

Mouse Drag

Keyboard

Administrator configurable.

---

# View Reset

The operator may restore

Original Axis Limits

Original Scale

Original Grid

Original Marker Positions

without affecting engineering data.

---

# Axis Scaling

Supported

Automatic

Manual

Locked

Scientific

Logarithmic (future)

Administrator configurable.

---

# Marker Behaviour

During zoom and pan

all engineering markers shall remain attached to their engineering coordinates.

Marker positions shall update automatically as the chart view changes.

---

# Inspection Compatibility

Zoom and Pan shall remain fully compatible with

Coordinate Inspection

Engineering Markers

Graph Correction

Manual Yield Selection

---

# Engineering Independence

The Zoom & Pan Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only the chart viewport changes.

---

# SQLite Interaction

SQLite stores

Optional View Preferences

Zoom Level

Last View

User Preference

Charts are always regenerated from engineering data.

---

# Error Handling

Invalid Zoom Region

↓

Ignore

Axis Limit Error

↓

Reset

No Dataset

↓

Abort

Chart Missing

↓

Abort

---

# Performance Targets

Zoom

Immediate

Pan

Immediate

Reset

< 20 ms

Axis Refresh

< 50 ms

---

# Acceptance Criteria

✔ Region zoom supported

✔ Mouse wheel zoom supported

✔ Pan supported

✔ Reset supported

✔ Marker positions preserved

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete engineering traceability

---

End of Document
