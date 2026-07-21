# Chart Rendering Engine

Document ID : MTDMS-GRH-002

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

This document defines the rendering engine responsible for drawing all engineering graphs inside MTDMS.

The rendering engine converts engineering datasets into interactive graphical objects while preserving numerical accuracy.

The rendering engine shall be independent from

• Engineering calculations

• Database

• Report generator

---

# Design Objectives

The rendering engine shall

• Render large datasets efficiently

• Preserve numerical accuracy

• Support interactive editing

• Support multiple curves

• Support multiple graph types

• Produce publication-quality graphs

---

# Rendering Pipeline

```
Dataset

↓

Validation

↓

Scaling

↓

Coordinate Transformation

↓

Axis Rendering

↓

Grid Rendering

↓

Curve Rendering

↓

Marker Rendering

↓

Annotation Rendering

↓

Refresh Screen
```

---

# Supported Graph Types

Stress – Strain

True Stress – True Strain

Force – Extension

Force – Time

Extension – Time

Deflection – Force

Ring Stiffness

Spring Curve

Control Charts

Calibration Curves

Custom XY

---

# Supported Curve Styles

Polyline

Spline

Scatter

Step

Reference Line

Regression Line

Construction Line

Offset Line

Trend Line

---

# Rendering Layers

Layer 1

Background

Layer 2

Grid

Layer 3

Axes

Layer 4

Curves

Layer 5

Reference Lines

Layer 6

Markers

Layer 7

Annotations

Layer 8

Mouse Cursor

---

# Coordinate Transformation

Internal Engineering Coordinates

↓

Normalized Coordinates

↓

Screen Coordinates

↓

Excel Chart Coordinates

Transformation must preserve

Double Precision.

---

# Scaling

Supported

Automatic Scale

Manual Scale

Locked Scale

Equal Scale

Dual Axis

Symmetric Scale

---

# Axis Configuration

Horizontal

Linear

Vertical

Linear

Future

Logarithmic

---

# Rendering Precision

Internal

Double Precision

Display

Configurable

Default

6 Decimal Places

---

# Dataset Validation

Before rendering

Verify

Dataset Exists

Equal Array Length

No NaN

No Infinity

Ascending X

Valid Axis Range

---

# Point Reduction

For datasets larger than

100,000 samples

display optimization

may be enabled.

Raw data

shall never be removed.

Only displayed points

may be simplified.

---

# Anti-Aliasing

Preferred

Enabled

If unsupported

Fallback

Standard Excel Rendering

---

# Redraw Policy

Full Redraw

Initial Display

Partial Redraw

Marker Movement

Zoom

Axis Change

Window Resize

---

# Refresh Priority

Highest

Marker Movement

Medium

Zoom

Lowest

Complete Graph Rebuild

---

# Performance Targets

Graph Size

100,000 points

Render Time

< 1 second

Zoom Refresh

< 200 ms

Marker Drag

Real Time

---

# Curve Colors

Default

Engineering Curve

Blue

True Curve

Red

Reference

Gray

Regression

Green

Offset

Orange

User configurable.

---

# Line Width

Engineering

2 px

Reference

1 px

Regression

2 px

Construction

1 px

Future

Dynamic Width

Reserved

---

# Error Handling

Dataset Missing

↓

Display Message

Coordinate Overflow

↓

Abort Render

Axis Failure

↓

Reset Scale

Memory Error

↓

Clear Cache

---

# Rendering Cache

Temporary cache

may be used for

Coordinates

Markers

Annotations

Cache shall be invalidated after

Zoom

Scale Change

Dataset Update

---

# Excel Compatibility

Compatible with

Excel 2019

No ActiveX dependency

No external graphics library

Uses native Excel Chart Objects

---

# SQLite

No graph image stored.

Only graph settings

and user annotations

are stored.

---

# Future Enhancements

GPU Rendering

OpenGL

Direct2D

SVG Export

High DPI Rendering

Dark Mode

Reserved

---

# Acceptance Criteria

✔ Supports all engineering graphs

✔ Supports 100,000+ points

✔ Double precision

✔ Fast rendering

✔ Modular architecture

✔ Excel 2019 compatible

✔ Independent from calculations

✔ Independent from reports

---

End of Document
