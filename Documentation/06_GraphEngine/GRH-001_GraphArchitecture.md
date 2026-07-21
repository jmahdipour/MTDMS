# Graph Engine Architecture

Document ID : MTDMS-GRH-001

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Graph Engine

Status

Production

---

# Purpose

This document defines the overall architecture of the Graph Engine used throughout MTDMS.

The Graph Engine is responsible for

• Displaying engineering graphs

• Interactive graph editing

• Graph correction

• Marker management

• Zoom and navigation

• Report-quality plotting

• Export

It shall be independent from engineering calculations.

---

# Design Principles

The Graph Engine shall

• Never modify raw data

• Never perform engineering calculations

• Receive calculated data only

• Be reusable for all test types

• Be modular

• Be independent of report generation

---

# Supported Graph Types

Tensile

Stress–Strain

Force–Extension

Force–Time

Displacement–Time

True Stress–True Strain

---

Bending

Force–Deflection

Moment–Curvature

---

Spring

Force–Displacement

K Curve

---

Ring Stiffness

Load–Deflection

---

Hardness

Statistical Charts

Control Charts

---

Quantometer

Control Charts

CRM Charts

Trend Charts

---

# Graph Layers

Graph rendering consists of independent layers.

```
Mouse Layer

↓

Marker Layer

↓

Annotation Layer

↓

Curve Layer

↓

Grid Layer

↓

Axis Layer

↓

Background
```

Each layer can be enabled independently.

---

# Internal Architecture

```
Engineering Module

↓

Graph Data Provider

↓

Graph Engine

↓

Display

↓

Operator
```

Graph Engine

never reads

TXT files directly.

---

# Graph Objects

Curve

Axis

Marker

Annotation

Legend

Grid

Selection

Cursor

Tooltip

---

# Curve Types

Polyline

Spline

Scatter

Step

Reference Line

Regression Line

Construction Line

Offset Line

---

# Axis Types

Linear

Logarithmic

Automatic

Manual

Dual Axis

---

# Coordinate Systems

Engineering Coordinates

Screen Coordinates

Mouse Coordinates

Printer Coordinates

All coordinate transformations are centralized.

---

# Rendering Pipeline

```
Load Graph

↓

Scale Axes

↓

Draw Grid

↓

Draw Curves

↓

Draw Markers

↓

Draw Labels

↓

Refresh Screen
```

---

# Refresh Strategy

Full Refresh

First Display

Partial Refresh

Marker Movement

Zoom Refresh

Scale Change

---

# Performance Target

100000 Points

Display

<1 second

Marker Dragging

Real-Time

Zoom

Smooth

---

# Supported User Operations

Zoom

Pan

Marker Move

Marker Delete

Marker Add

Region Selection

Export

Print

Undo

Redo

---

# Mouse Events

Mouse Move

Mouse Down

Mouse Up

Double Click

Wheel

Right Click

---

# Graph Modes

Read Only

Operator

Engineering

Report

Debug

Each mode enables different features.

---

# Data Flow

Raw Data

↓

Engineering Calculations

↓

Graph Dataset

↓

Rendering

↓

User Interaction

↓

Temporary Objects

↓

Display

---

# Memory Management

Raw Data

Read Only

Graph Cache

Temporary

Markers

Temporary

Undo Stack

Configurable

---

# Error Handling

Missing Dataset

↓

Display Error

Invalid Axis

↓

Reset Scale

Empty Graph

↓

Placeholder

Overflow

↓

Abort Rendering

---

# SQLite

Graph settings stored in

```
tblGraphSettings
```

Graph annotations

```
tblGraphAnnotation
```

Graph markers

```
tblGraphMarkers
```

---

# Future Expansion

3D Graphs

FFT

Digital Image Correlation

Video Synchronization

Multi-monitor Support

GPU Rendering

Reserved

---

# Acceptance Criteria

✔ Modular architecture

✔ Independent from calculations

✔ Independent from reports

✔ Supports all test types

✔ Excel 2019 compatible

✔ SQLite compatible

✔ ISO 17025 traceable

---

End of Document
