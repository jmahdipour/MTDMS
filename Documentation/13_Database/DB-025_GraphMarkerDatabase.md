# Graph Marker Database

Document ID : MTDMS-DB-025

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

The Graph Marker Database stores the positions of engineering markers selected on graphs generated from the imported TXT file.

Markers are references only.

They never modify the imported engineering data.

They are used to reproduce graphs and reports consistently.

---

# Objectives

The Graph Marker Database shall

• Store automatic marker positions

• Store manually corrected marker positions

• Preserve graph reproducibility

• Support report regeneration

• Preserve engineering traceability

---

# Design Philosophy

TXT File

↓

Engineering Calculation

↓

Engineering Graph

↓

Marker Selection

↓

SQLite

Markers describe locations on the graph.

Engineering values are recalculated from the TXT file.

---

# Table Name

tblGraphMarker

---

# Primary Key

MarkerID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

MarkerID

INTEGER

----------------------------

ImportID

INTEGER

Foreign Key

tblImportHistory

----------------------------

ReportID

INTEGER

Nullable

----------------------------

GraphType

TEXT

Examples

Stress-Strain

Force-Displacement

Force-Time

Spring

Ring Stiffness

----------------------------

MarkerType

TEXT

Examples

Yield

Maximum

Fracture

Offset

Manual Reference

Elastic Region

Intersection

----------------------------

SelectionMethod

TEXT

Examples

Automatic

Manual

Semi Automatic

----------------------------

XValue

REAL

----------------------------

YValue

REAL

----------------------------

PointIndex

INTEGER

Nullable

Reference to imported TXT row.

----------------------------

VisibleInReport

BOOLEAN

----------------------------

Locked

BOOLEAN

----------------------------

OperatorID

INTEGER

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

----------------------------

Remarks

TEXT

Nullable

---

# Supported Markers

Yield Point

Ultimate Point

Fracture Point

Elastic End

Offset Line

Maximum Force

Maximum Extension

Reference Point

Future markers

Administrator configurable.

---

# Manual Marker Rules

Manual marker

shall replace

automatic marker

for report generation.

The original automatic marker

shall remain stored

for traceability.

---

# Engineering Independence

Marker positions

shall never

modify

Imported TXT

Engineering calculations

Stress

Strain

Force

Displacement

Markers are graphical references only.

---

# Hidden Markers

Construction markers

Guide lines

Temporary intersections

Operator helper points

shall never appear

in the final report.

---

# SQLite Relationships

tblGraphMarker

↓

N : 1

tblImportHistory

↓

N : 1

tblReport

↓

N : 1

tblOperator

↓

N : 1

tblAuditTrail

---

# Indexes

IX_ImportID

IX_ReportID

IX_GraphType

IX_MarkerType

---

# Constraints

ImportID

Required

GraphType

Required

MarkerType

Required

---

# Audit Trail

Store

Marker

Operator

Automatic / Manual

Coordinates

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Modify

Quality Manager

Modify

Reviewer

Read

Operator

Create

Modify

---

# Error Handling

Marker Outside Graph

↓

Reject

Missing Graph

↓

Abort

Missing TXT Reference

↓

Abort

Duplicate Marker

↓

Replace after confirmation

---

# Performance

Marker save

Target

< 10 ms

---

# Acceptance Criteria

✔ Automatic markers stored

✔ Manual markers stored

✔ Graph reproducibility preserved

✔ Hidden construction markers excluded from reports

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
