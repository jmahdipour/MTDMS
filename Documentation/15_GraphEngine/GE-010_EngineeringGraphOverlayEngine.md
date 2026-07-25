# Engineering Graph Overlay Engine

Document ID : MTDMS-GE-010

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

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Graph Overlay Engine compares multiple datasets on a single engineering graph without modifying any underlying data.

Its primary function is to assist engineers in comparing

- Raw machine data
- Corrected engineering data
- Previous tests
- Material references
- Standard reference curves

The engine performs no engineering calculations.

---

# Objectives

The Graph Overlay Engine shall

• Overlay multiple engineering datasets

• Compare raw and corrected curves

• Compare multiple specimens

• Compare different materials

• Support engineering analysis

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Overlay Engine

↓

Comparison Graph

Every displayed curve retains its original engineering identity.

---

# Supported Overlay Types

Raw vs Engineering

Test vs Test

Material vs Material

Batch vs Batch

Customer vs Customer

Machine vs Machine

Reference vs Measurement

Administrator configurable.

---

# Overlay Workflow

```
Dataset A

↓

Dataset B

↓

Alignment

↓

Overlay

↓

Comparison

↓

Engineering Review
```

---

# Data Alignment

The engine shall support

Time Alignment

Origin Alignment

Force Alignment

Stress Alignment

Strain Alignment

Displacement Alignment

No alignment shall modify the original datasets.

---

# Raw vs Engineering

The engine shall display

Original TXT Curve

Engineering Stress–Strain Curve

Graph Corrected Curve

simultaneously.

This assists in validating engineering transformations.

---

# Multiple Specimens

The operator may overlay

2

5

10

or more specimens

depending on available system resources.

---

# Curve Identification

Each curve shall display

Name

Report Number

Material

Date

Operator

Standard

Color

Line Style

---

# Automatic Scaling

Supported

Independent Scaling

Shared Scaling

Normalized Scaling

Administrator configurable.

---

# Legend

The legend shall automatically identify every displayed dataset.

Hidden datasets shall not appear in the legend.

---

# Difference Analysis

Optional

The engine may calculate

Maximum Difference

Average Difference

Area Difference

Deviation Curve

Comparison values are informational only.

---

# Visibility Control

Each dataset may be

Visible

Hidden

Locked

Highlighted

Administrator configurable.

---

# Printing

Overlay graphs shall support

Excel Reports

PDF

PNG

EMF

without loss of engineering information.

---

# Engineering Independence

The Overlay Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It displays multiple existing datasets only.

---

# SQLite Interaction

SQLite stores

Overlay Configuration

Visible Datasets

Color Assignment

Operator Preferences

Graphs are regenerated dynamically.

---

# Error Handling

Missing Dataset

↓

Ignore

Different Units

↓

Reject Overlay

Invalid Alignment

↓

Warning

Too Many Curves

↓

Performance Warning

---

# Performance Targets

Overlay Two Curves

< 200 ms

Overlay Ten Curves

< 1 s

Visibility Update

Immediate

---

# Acceptance Criteria

✔ Raw vs engineering overlay supported

✔ Multiple specimen comparison supported

✔ Independent dataset preservation

✔ Dynamic legend supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
