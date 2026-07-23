# Graph & Visualization Engine Architecture

Document ID : MTDMS-GE-001

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Chart Engine

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

The Graph & Visualization Engine is responsible for presenting engineering data generated from the Calculation Engine.

It creates interactive engineering charts inside Microsoft Excel.

The engine performs **no engineering calculations**.

Its sole responsibility is graphical visualization.

---

# Objectives

The Graph Engine shall

• Display engineering graphs

• Support interactive engineering analysis

• Support engineering markers

• Support graph correction

• Produce publication-quality figures

• Support report generation

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Calculation Engine

↓

Validated Engineering Results

↓

Graph Engine

↓

Excel Charts

The graph is always regenerated from engineering data.

Graphs are never imported as images.

---

# Engine Position

```
TXT

↓

Calculation Engine

↓

Validation

↓

Graph Engine

↓

Report Engine

↓

PDF
```

---

# Responsibilities

Generate graphs

Manage engineering markers

Manage graph styles

Manage zoom

Manage coordinate display

Manage graph correction display

Generate report graphics

Generate printable graphics

---

# Engineering Independence

The Graph Engine

shall never

modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It visualizes only.

---

# Data Sources

Engineering Dataset

Validation Results

Material Library

Graph Style Library

Graph Marker Library

Operator Adjustments

---

# Supported Engineering Graphs

Stress vs Strain

True Stress vs True Strain

Force vs Displacement

Force vs Time

Extension vs Time

Compression Curve

Three-Point Bending

Four-Point Bending

Spring Curve

Ring Stiffness Curve

Administrator configurable.

---

# Graph Components

Each graph consists of

Axes

Data Series

Markers

Construction Lines

Legend

Title

Annotations

Grid

Metadata

---

# Excel Technology

The engine uses

Microsoft Excel

XY Scatter Charts

Dynamic Named Ranges

Chart Objects

No external chart library is required.

---

# Coordinate System

Internal coordinates

are generated from

validated engineering data.

Displayed coordinates

may be transformed

for graph correction

without affecting engineering values.

---

# Refresh Strategy

Graphs shall automatically refresh

After TXT Import

After Recalculation

After Validation

After Manual Marker Change

After Graph Style Change

Administrator configurable.

---

# Performance Targets

Typical Tensile Graph

Creation

< 500 ms

Refresh

< 300 ms

Marker Update

Immediate

---

# SQLite Interaction

SQLite stores

Graph Metadata

Marker Locations

Style Configuration

Operator Adjustments

Charts themselves are regenerated.

---

# Acceptance Criteria

✔ Architecture defined

✔ Engineering independence maintained

✔ Excel Chart Objects used

✔ Automatic refresh supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
