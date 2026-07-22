# Graph Correction Engine

Document ID : MTDMS-CE-008

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Input

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Graph Correction Engine produces a visually corrected engineering stress–strain graph without modifying the original imported data or calculated engineering results.

Its purpose is to improve graphical interpretation while preserving complete engineering traceability.

The corrected graph is intended for display and reporting only.

---

# Objectives

The Graph Correction Engine shall

• Correct the visual alignment of the elastic region

• Preserve all engineering calculations

• Support manual graph adjustment

• Display engineering markers

• Produce publication-quality graphs

---

# Engineering Philosophy

TXT File

↓

Engineering Calculation

↓

Engineering Results

↓

Graph Correction

↓

Display Graph

↓

Report

The graph may be corrected.

The engineering results shall never be altered.

---

# Principle

The Graph Correction Engine

operates only on

graph coordinates.

It never changes

Force

Stress

Extension

Strain

Yield Strength

Ultimate Strength

Young's Modulus

Engineering Results

---

# Inputs

Engineering Stress

Engineering Strain

Young's Modulus

Yield Point

Fracture Point

Manual Secondary Gauge Length

Material Reference (optional)

---

# Graph Corrections

The engine may perform

Elastic Region Alignment

Horizontal Offset Removal

Zero Alignment

Visual Slope Adjustment

Fracture Cut

Marker Optimization

All corrections are visual only.

---

# Elastic Region Alignment

The graph shall be aligned so that

the elastic portion corresponds to the measured Young's Modulus.

The original engineering values remain unchanged.

---

# Horizontal Offset Removal

If the imported curve begins with an offset caused by machine seating or grip clearance,

the graph may be shifted horizontally for visualization.

The imported measurements remain unchanged.

---

# Fracture Handling

After fracture,

the displayed graph shall terminate at the detected fracture point.

Noise or post-fracture data shall not be shown in the final engineering graph.

The original data remain available in the imported dataset.

---

# Construction Lines

The engine may temporarily display

Elastic Regression Line

Offset Line

Yield Construction Line

Reference Modulus Line

These auxiliary lines

shall never appear in

Final Reports

PDF Export

Certificates

unless explicitly enabled by the administrator.

---

# Engineering Markers

The graph may display

Yield Point

Ultimate Strength

Fracture Point

Elastic Region

Manual Yield Marker

Reference Yield Window

Marker visibility is configurable.

---

# Manual Graph Adjustment

The operator may

Move Yield Marker

Adjust Elastic Region

Select Fracture Point

Recalculate Graph Display

Every manual adjustment shall be recorded in the audit trail.

Engineering calculations remain unchanged unless a manual recalculation is explicitly requested.

---

# Output

Corrected Graph Coordinates

Marker Locations

Graph Metadata

Display Parameters

Graph Style Reference

---

# SQLite Interaction

SQLite stores

Graph Parameters

Marker Locations

Operator Adjustments

Graph Style

The corrected graph itself is regenerated whenever needed.

---

# Engineering Independence

The Graph Correction Engine

shall never modify

Imported TXT

Engineering Results

Stress

Strain

Yield Strength

Ultimate Strength

Only graph coordinates are adjusted for visualization.

---

# Error Handling

Missing Young's Modulus

↓

Graph without correction

Missing Yield Point

↓

Graph without yield marker

Fracture Not Found

↓

Display full curve

Invalid Manual Adjustment

↓

Reject

---

# Performance Targets

Graph Preparation

< 300 ms

Graph Correction

< 300 ms

Marker Placement

< 50 ms

---

# Acceptance Criteria

✔ Elastic alignment supported

✔ Horizontal offset correction supported

✔ Fracture trimming supported

✔ Manual adjustment supported

✔ Auxiliary lines hidden in final reports

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO 6892-1 compatible

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
