# Zoom & Pan Engine

Document ID : MTDMS-GRH-003

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

This document defines the Zoom and Pan subsystem used by the Graph Engine.

The subsystem allows the operator to inspect large engineering datasets without altering the original data.

Zooming and panning shall affect only the visualization.

Engineering calculations shall remain unchanged.

---

# Design Objectives

The Zoom & Pan Engine shall provide

• Smooth zooming

• Fast panning

• Mouse-wheel zoom

• Drag navigation

• Keyboard shortcuts

• Reset view

• High precision

---

# Supported Operations

Zoom In

Zoom Out

Rectangle Zoom

Mouse Wheel Zoom

Horizontal Pan

Vertical Pan

Free Pan

Reset View

Fit to Data

Fit X

Fit Y

---

# Architecture

```
Mouse Event

↓

Zoom Controller

↓

Viewport Manager

↓

Coordinate Converter

↓

Chart Renderer

↓

Display
```

---

# Viewport

The viewport defines the visible region of the graph.

Only the viewport changes.

Underlying data remain unchanged.

---

# Zoom Types

## Mouse Wheel

Cursor-centered zoom

---

## Rectangle Zoom

Operator drags a rectangle.

The selected rectangle becomes the new viewport.

---

## Axis Zoom

Zoom only X-axis

Zoom only Y-axis

---

## Fixed Ratio Zoom

Both axes scale equally.

Useful for geometry-based graphs.

---

# Pan Operation

Operator presses

Middle Mouse Button

or

Shift + Left Mouse

↓

Drag

↓

Viewport moves

↓

Graph refresh

---

# Keyboard Shortcuts

Ctrl + Mouse Wheel

Zoom

Shift + Mouse Wheel

Horizontal Pan

Arrow Keys

Pan

Home

Reset View

End

Fit to Data

---

# Zoom Limits

Minimum Zoom

0.001 %

Maximum Zoom

1000 %

Administrator configurable.

---

# Coordinate Conversion

Engineering Coordinates

↓

Viewport Coordinates

↓

Screen Coordinates

↓

Excel Chart Coordinates

---

# Refresh Strategy

Only visible region

is redrawn.

Entire dataset

shall not be regenerated.

---

# Performance

Target Dataset

100,000 Samples

Zoom Response

<100 ms

Pan Response

Real-Time

---

# Precision

Internal

Double Precision

No cumulative coordinate rounding

is permitted.

---

# Cursor Position

During zoom

cursor coordinates remain visible.

Displayed

X

Y

Stress

Strain

Force

Extension

depending on graph type.

---

# Synchronization

Multiple graphs

may be synchronized.

Example

Stress–Strain

↓

Force–Extension

↓

Time Graph

All graphs

zoom together

if synchronization is enabled.

---

# Reset View

Reset shall restore

Original Scale

Original Center

Original Aspect Ratio

without recalculation.

---

# Error Handling

Viewport Outside Data

↓

Clamp to Data Range

Invalid Zoom Factor

↓

Ignore

Division by Zero

↓

Abort

Overflow

↓

Reset View

---

# SQLite

Store

Last Zoom

Last Pan

Synchronization Mode

Table

```
tblGraphSettings
```

---

# Future Enhancements

Touch Support

Multi-Touch Zoom

Inertial Panning

Mini Map

Bookmarks

Multiple Viewports

Reserved

---

# Acceptance Criteria

✔ Smooth zoom

✔ Smooth pan

✔ Cursor-centered zoom

✔ Rectangle zoom

✔ Reset view

✔ Fit to data

✔ Double precision

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No modification of engineering data

---

End of Document
