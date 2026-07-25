# Excel Chart Engine

Document ID : MTDMS-GE-002

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

The Excel Chart Engine is responsible for creating, updating, and managing all engineering charts inside Microsoft Excel.

The engine converts validated engineering datasets into dynamic Excel charts suitable for engineering analysis, reporting, and printing.

---

# Objectives

The Excel Chart Engine shall

• Create engineering charts

• Update charts automatically

• Support multiple datasets

• Maintain engineering precision

• Support publication-quality output

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Excel Chart Engine

↓

Excel Chart

↓

Report

Charts are generated directly from engineering data.

No bitmap or screenshot is used.

---

# Supported Chart Technology

Microsoft Excel

XY Scatter

Straight Lines

Dynamic Series

Named Ranges

Chart Objects

Embedded Charts

---

# Supported Chart Types

Stress vs Strain

True Stress vs True Strain

Force vs Displacement

Force vs Time

Extension vs Time

Compression Curve

Spring Curve

Ring Stiffness Curve

Three-Point Bending

Four-Point Bending

Administrator configurable.

---

# Chart Creation Workflow

```
Engineering Dataset

↓

Create Chart Object

↓

Assign Series

↓

Assign Axes

↓

Apply Style

↓

Apply Markers

↓

Display
```

---

# Data Source

Charts shall use

validated engineering datasets

generated from the TXT file.

Charts shall never use

report values

or manually copied values.

---

# X Axis

Possible values

Strain

Displacement

Time

Extension

Administrator configurable.

---

# Y Axis

Possible values

Stress

Force

True Stress

Spring Force

Ring Load

Administrator configurable.

---

# Dynamic Update

Charts shall automatically update

After TXT Import

After Recalculation

After Validation

After Manual Marker Change

After Graph Style Change

---

# Multiple Series

The engine shall support

Engineering Curve

True Curve

Elastic Line

Reference Line

Comparison Curve

Administrator configurable.

---

# Axis Scaling

Automatic

Manual

Locked

Scientific

Administrator configurable.

---

# Legend

Configurable

Visible

Hidden

Custom Position

Custom Text

---

# Titles

Graph Title

X Axis Title

Y Axis Title

Subtitle

Material

Report Number

Optional.

---

# Grid

Major Grid

Minor Grid

Visible

Hidden

Administrator configurable.

---

# Printing

Charts shall be optimized for

A4 Portrait

A4 Landscape

Report Templates

PDF Export

---

# Engineering Independence

The Excel Chart Engine

shall never modify

Engineering Dataset

Engineering Results

Validation Results

Charts visualize existing data only.

---

# SQLite Interaction

SQLite stores

Chart Metadata

Style Selection

Display Configuration

Charts themselves are regenerated.

---

# Error Handling

No Dataset

↓

Abort

Invalid Axis

↓

Reject

Chart Creation Failure

↓

Retry

Series Missing

↓

Warning

---

# Performance Targets

Create Chart

< 300 ms

Refresh Chart

< 200 ms

Update Series

Immediate

---

# Acceptance Criteria

✔ Dynamic Excel charts

✔ Multiple engineering graphs

✔ Automatic refresh

✔ Dynamic axes

✔ Publication-quality output

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
