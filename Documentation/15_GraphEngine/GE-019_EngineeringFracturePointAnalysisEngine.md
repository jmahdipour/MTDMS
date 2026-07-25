# Engineering Fracture Point Analysis Engine

Document ID : MTDMS-GE-019

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

The Engineering Fracture Point Analysis Engine identifies, displays, validates, and allows operator verification of the fracture point on engineering graphs reconstructed from the imported TXT file.

This module is responsible only for graphical interpretation.

Engineering fracture calculations remain the responsibility of the Calculation Engine.

---

# Objectives

The Fracture Point Analysis Engine shall

• Display calculated fracture location

• Support operator verification

• Detect abnormal fracture behaviour

• Preserve engineering traceability

• Support report generation

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Calculation Engine

↓

Fracture Result

↓

Graphical Verification

↓

Engineering Report

Fracture visualization shall never modify engineering calculations.

---

# Fracture Definition

The fracture point represents

the final valid engineering measurement

immediately before specimen separation

or

the last accepted engineering data point

according to the selected calculation profile.

---

# Workflow

```
Engineering Dataset

↓

Fracture Detection

↓

Graph Marker

↓

Operator Verification

↓

Approved Fracture Marker
```

---

# Automatic Detection

The graph shall automatically display

Fracture Point

Final Force

Final Stress

Final Strain

Final Extension

Final Displacement

---

# Manual Verification

The operator may

Accept

Move

Reject

Replace

the fracture marker.

The original calculated fracture location remains preserved.

---

# Manual Selection Rules

The fracture marker

shall always snap

to the nearest measured engineering point.

Interpolation is disabled by default.

---

# Fracture Indicators

The graph may display

Fracture Marker

Reference Label

Final Segment

Fracture Line

End of Valid Dataset

Administrator configurable.

---

# Abnormal Fracture Detection

The engine may warn about

Sudden Force Drop

Unexpected Data Gap

Missing Final Measurement

Multiple Candidate Fracture Points

Extensometer Loss Before Fracture

Crosshead Continues After Fracture

These warnings assist the operator only.

---

# Fracture Information Window

Selecting the fracture marker displays

Force

Stress

Strain

Extension

Displacement

Elapsed Time

Validation Status

Operator Confirmation

---

# Graph Behaviour

Optional display modes

Original Curve

Trimmed Curve

Overlay

Comparison

Administrator configurable.

The trimmed curve affects only visualization.

---

# Report Behaviour

Approved fracture information may appear in

Reports

Certificates

PDF

Temporary engineering construction objects remain hidden.

---

# Engineering Independence

The Fracture Point Analysis Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only graphical verification is managed.

---

# SQLite Interaction

SQLite stores

Calculated Fracture Position

Operator Position

Approval Status

Operator

Timestamp

Audit Trail

Engineering calculations remain unchanged.

---

# Error Handling

No Fracture Found

↓

Warning

Multiple Candidates

↓

Operator Review

Marker Outside Dataset

↓

Reject

Missing Final Measurement

↓

Warning

---

# Performance Targets

Fracture Display

Immediate

Marker Update

< 20 ms

Operator Approval

< 20 ms

---

# Acceptance Criteria

✔ Automatic fracture detection displayed

✔ Manual verification supported

✔ Abnormal fracture warnings supported

✔ Operator approval recorded

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT

---

End of Document
