# Engineering Graph Generation Engine

Document ID : MTDMS-CE-016

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Chart Engine

Microsoft Excel Chart Object

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

The Engineering Graph Generation Engine creates all engineering charts directly from the reconstructed dataset generated from the imported TXT file.

Graphs are generated dynamically inside Microsoft Excel.

No graph image is permanently stored inside SQLite.

---

# Objectives

The Engineering Graph Generation Engine shall

• Generate engineering charts

• Support interactive analysis

• Support manual engineering markers

• Support graph correction

• Generate report-quality figures

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Graph Engine

↓

Excel Chart

↓

Report

Every graph shall be regenerated from engineering data.

Graphs are never imported as images.

---

# Supported Graphs

Force vs Time

Force vs Displacement

Stress vs Strain

True Stress vs True Strain

Extension vs Time

Displacement vs Time

Spring Force vs Displacement

Ring Stiffness Force vs Displacement

Compression Stress vs Strain

Three-Point Bending Curve

Four-Point Bending Curve

Administrator configurable.

---

# Graph Source

Only

Engineering Dataset

generated from

TXT File

may be used.

Graphs shall never be reconstructed from report values.

---

# Graph Workflow

```
TXT

↓

Engineering Dataset

↓

Engineering Results

↓

Graph Generation

↓

Interactive Analysis

↓

Report
```

---

# Excel Chart Type

Preferred

XY Scatter

Straight Lines

because engineering data are continuous.

Optional

Smooth Line

Administrator configurable.

---

# Interactive Cursor

The graph shall support

Mouse Position

↓

Display

X Coordinate

Y Coordinate

Current Stress

Current Strain

Current Force

Current Displacement

The coordinate display shall update in real time.

---

# Manual Engineering Markers

The operator may manually place

Yield Point

Fracture Point

Maximum Force

Maximum Stress

Reference Points

These markers are stored separately.

Original data remain unchanged.

---

# Auxiliary Construction Lines

Temporary lines may be displayed

Elastic Line

Offset Line

Reference Line

Regression Line

These lines

shall automatically disappear

from

Final Report

PDF

Certificate

unless enabled by the administrator.

---

# Automatic Markers

The engine shall automatically display

Maximum Force

Yield

Fracture

Elastic Region

Reference Strain

Reference Stress

Marker visibility is configurable.

---

# Zoom

Support

Mouse Zoom

Area Zoom

Reset Zoom

Pan

Administrator configurable.

---

# Grid

Configurable

Major Grid

Minor Grid

Log Scale (future)

---

# Graph Styles

Graph appearance

is obtained from

Graph Style Library

No graph colors are hardcoded.

---

# SQLite Interaction

SQLite stores

Graph Metadata

Marker Positions

Operator Adjustments

Graph Style

Graphs themselves are regenerated every time.

---

# Engineering Independence

Graph generation

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only graphical presentation is affected.

---

# Error Handling

No Data

↓

Abort

Invalid Dataset

↓

Abort

Marker Outside Graph

↓

Reject

Chart Creation Failure

↓

Retry

---

# Performance Targets

Typical Tensile Graph

< 500 ms

Interactive Marker Update

< 20 ms

Zoom

Immediate

---

# Acceptance Criteria

✔ Graph generated directly from TXT-derived dataset

✔ Interactive coordinates supported

✔ Manual markers supported

✔ Auxiliary lines hidden from reports

✔ Excel Chart Object used

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility

---

End of Document
