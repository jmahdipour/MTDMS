# Engineering Multi-Graph Workspace Engine

Document ID : MTDMS-GE-014

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

The Engineering Multi-Graph Workspace Engine manages the simultaneous display of multiple engineering graphs within Microsoft Excel.

It provides engineers with a workspace for comparing different graph types, specimens, or engineering datasets while maintaining complete traceability to the original TXT file.

The engine performs no engineering calculations.

---

# Objectives

The Multi-Graph Workspace Engine shall

• Display multiple engineering graphs simultaneously

• Synchronize graph navigation

• Support engineering comparison

• Improve engineering workflow

• Preserve engineering independence

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Graph Engine

↓

Workspace Engine

↓

Engineering Review

Every displayed graph originates from validated engineering data.

---

# Supported Workspace Layouts

Single Graph

Two Graphs

Four Graphs

Six Graphs

Custom Layout

Administrator configurable.

---

# Supported Graph Combinations

Stress–Strain

+

Force–Displacement

----------------------------

Raw Curve

+

Engineering Curve

----------------------------

Compression

+

Tensile

----------------------------

Spring

+

Ring Stiffness

----------------------------

Bending

+

Stress–Strain

Administrator configurable.

---

# Workspace Workflow

```
Engineering Dataset

↓

Generate Graphs

↓

Arrange Workspace

↓

Synchronize View

↓

Engineering Inspection
```

---

# Workspace Synchronization

Optional synchronization

Zoom

Pan

Cursor

Markers

Selection

Administrator configurable.

---

# Independent Navigation

Each graph may also be inspected independently.

Synchronization may be disabled at any time.

---

# Linked Cursor

Optional

Moving the cursor on one graph highlights the corresponding engineering position on all synchronized graphs.

Example

Force–Displacement

↓

Equivalent point

↓

Stress–Strain

---

# Workspace Presets

Supported presets

Tensile Analysis

Compression Analysis

Spring Analysis

Ring Stiffness

Failure Analysis

Administrator configurable.

---

# Workspace Saving

The engine may save

Visible Graphs

Layout

Zoom

Synchronization State

Marker Visibility

Operator Preferences

---

# Workspace Restoration

Saved workspaces may be restored automatically when reopening a project.

---

# Engineering Independence

The Workspace Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only the visual arrangement is affected.

---

# SQLite Interaction

SQLite stores

Workspace Layout

Visible Graphs

Synchronization State

Operator Preferences

Engineering data remain unchanged.

---

# Error Handling

Missing Graph

↓

Ignore

Layout Invalid

↓

Use Default

Synchronization Failure

↓

Disable Sync

Workspace Missing

↓

Create Default Workspace

---

# Performance Targets

Open Workspace

< 500 ms

Switch Layout

< 300 ms

Synchronize Cursor

Immediate

Refresh All Graphs

< 1 s

---

# Acceptance Criteria

✔ Multiple graphs displayed simultaneously

✔ Synchronized navigation supported

✔ Independent navigation supported

✔ Workspace presets supported

✔ Workspace restoration supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT

---

End of Document
