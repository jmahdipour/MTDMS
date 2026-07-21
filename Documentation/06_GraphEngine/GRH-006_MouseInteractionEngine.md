# Mouse Interaction Engine

Document ID : MTDMS-GRH-006

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

This document defines the Mouse Interaction Engine responsible for all user interactions with engineering graphs.

The engine converts mouse events into engineering operations while maintaining full numerical accuracy.

It is the primary interface between the operator and the graph.

---

# Design Objectives

The Mouse Interaction Engine shall provide

• Precise coordinate tracking

• Real-time response

• Marker manipulation

• Region selection

• Zoom control

• Pan control

• Engineering point identification

without modifying the original engineering dataset.

---

# Architecture

```
Mouse Device

↓

Windows Event

↓

Excel Event

↓

Mouse Interaction Engine

↓

Graph Engine

↓

Display
```

---

# Event Types

Supported Events

Mouse Move

Mouse Down

Mouse Up

Mouse Click

Double Click

Right Click

Mouse Wheel

Mouse Enter

Mouse Leave

Drag

---

# Event Processing

```
Mouse Event

↓

Determine Graph Object

↓

Determine Graph Coordinates

↓

Determine Engineering Coordinates

↓

Execute Action

↓

Refresh Display
```

---

# Coordinate Conversion

Screen Coordinates

↓

Chart Coordinates

↓

Viewport Coordinates

↓

Engineering Coordinates

---

# Cursor Position

During mouse movement

the engine shall continuously calculate

Engineering X

Engineering Y

Screen X

Screen Y

Sample Index

Nearest Curve

Nearest Marker

---

# Coordinate Display

Operator shall always see

X Coordinate

Y Coordinate

Stress

Strain

Force

Extension

Time

depending on graph type.

Display refresh

shall occur in real time.

---

# Snap Engine

Cursor may operate in

Free Mode

or

Snap Mode

---

## Free Mode

Cursor follows the mouse exactly.

---

## Snap Mode

Cursor automatically snaps to

Nearest Sample

Nearest Marker

Nearest Intersection

Nearest Construction Line

Tolerance configurable.

---

# Selection Modes

Single Point

Multiple Points

Rectangle

Free Polygon

Horizontal Band

Vertical Band

Entire Curve

---

# Marker Interaction

Single Click

Select Marker

Drag

Move Marker

Double Click

Marker Properties

Right Click

Context Menu

---

# Curve Interaction

Single Click

Nearest Sample

Double Click

Engineering Information

Right Click

Curve Menu

---

# Region Selection

Operator may drag

a rectangular area

to

Measure

Zoom

Export

Statistics

Engineering Analysis

---

# Tooltip Engine

Mouse Hover

↓

Tooltip appears

Contents

Curve Name

Sample Number

Stress

Strain

Force

Extension

Time

Marker Name

---

# Cursor Styles

Arrow

Crosshair

Hand

Resize

Move

Selection

Administrator configurable.

---

# Mouse Wheel

Default

Zoom

Optional

Scroll

Optional

Parameter Adjustment

---

# Double Click Behaviour

Default

Auto Fit

or

Marker Editor

depending on selected object.

---

# Right Click Menu

Zoom

Reset

Fit

Marker

Export

Copy Coordinates

Engineering Properties

Print

---

# Keyboard Integration

Ctrl

Multi-selection

Shift

Pan

Alt

Temporary Snap Disable

Esc

Cancel Current Operation

---

# Performance

Mouse Position Update

< 10 ms

Marker Drag

Real Time

Tooltip Refresh

< 20 ms

---

# Error Handling

Cursor Outside Graph

↓

Hide Tooltip

Invalid Coordinate

↓

Ignore

Marker Locked

↓

Reject Move

Unknown Object

↓

Default Cursor

---

# SQLite

User preferences stored in

```
tblGraphSettings
```

Items

Snap Mode

Tooltip Enabled

Cursor Type

Wheel Mode

Selection Mode

---

# Future Enhancements

Touch Support

Stylus Support

Pressure Detection

Gesture Recognition

3D Interaction

Reserved

---

# Acceptance Criteria

✔ Real-time coordinate tracking

✔ Snap mode

✔ Marker interaction

✔ Region selection

✔ Zoom integration

✔ Tooltip support

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering data never modified

---

End of Document
