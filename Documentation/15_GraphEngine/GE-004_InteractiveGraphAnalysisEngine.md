# Interactive Graph Analysis Engine

Document ID : MTDMS-GE-004

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

The Interactive Graph Analysis Engine provides engineering interaction with charts generated from the validated dataset reconstructed from the imported TXT file.

This module enables engineers to inspect curves, read coordinates, place engineering markers, and review calculated results.

The engine performs **no engineering calculations**.

---

# Objectives

The Interactive Graph Analysis Engine shall

• Display engineering coordinates

• Support engineering inspection

• Support manual engineering markers

• Support engineering review

• Preserve engineering integrity

---

# Engineering Philosophy

Engineering Dataset

↓

Interactive Analysis

↓

Operator Review

↓

Engineering Decision

↓

Report

The operator analyzes engineering data.

The graph never changes the engineering calculations automatically.

---

# Interactive Functions

Coordinate Inspection

Zoom

Pan

Engineering Markers

Reference Cursor

Manual Yield Selection

Manual Fracture Selection

Engineering Notes

---

# Coordinate Display

While moving over the curve

display

X Coordinate

Y Coordinate

Force

Stress

Strain

Displacement

Extension

Time

depending on graph type.

---

# Cursor

Supported cursor modes

Standard

Crosshair

Engineering Cursor

Administrator configurable.

---

# Zoom

Supported

Mouse Wheel

Selection Zoom

Reset Zoom

Fit to Window

---

# Pan

Supported

Horizontal

Vertical

Both

Administrator configurable.

---

# Engineering Markers

The operator may place

Yield

Fracture

Maximum Load

Reference Point

Inspection Point

Every marker is stored independently from engineering calculations.

---

# Manual Selection

The operator may manually select

Yield Point

Fracture Point

Linear Region

Reference Position

The selection shall be validated before acceptance.

---

# Inspection Window

Selecting any point shall display

Force

Stress

Strain

Displacement

Extension

Time

Calculated Coordinates

Reference Values

Validation Status

---

# Engineering Notes

The operator may attach notes

to

Markers

Graph

Inspection Points

These notes become part of the report audit trail.

---

# Undo

Supported

Undo Marker

Undo Last Action

Clear Temporary Marker

Permanent engineering results are unaffected.

---

# Engineering Independence

The Interactive Graph Analysis Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Operator interaction affects only review data.

---

# SQLite Interaction

SQLite stores

Marker Positions

Operator Notes

Review History

Inspection History

Audit Trail

Engineering values remain unchanged.

---

# Error Handling

Marker Outside Dataset

↓

Reject

Invalid Coordinate

↓

Ignore

Missing Dataset

↓

Abort

Invalid Graph

↓

Abort

---

# Performance Targets

Coordinate Update

Immediate

Zoom

Immediate

Marker Placement

< 20 ms

Inspection Window

< 50 ms

---

# Acceptance Criteria

✔ Coordinate inspection supported

✔ Interactive zoom supported

✔ Interactive pan supported

✔ Manual engineering markers supported

✔ Engineering notes supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
