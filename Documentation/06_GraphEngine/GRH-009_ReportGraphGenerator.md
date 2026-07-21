# Report Graph Generator

Document ID : MTDMS-GRH-009

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

This document defines the Report Graph Generator responsible for producing publication-quality engineering graphs for reports, certificates and PDF exports.

The generated graph shall be independent of the interactive graph.

Interactive objects shall never appear in the report.

---

# Reference Standards

ISO 6892-1

ISO 17025

ISO 7500-1

ASTM E8 / ASTM E8M

---

# Objectives

The Report Graph Generator shall

• Produce clean engineering graphs

• Remove temporary editing objects

• Maintain numerical accuracy

• Support A4 reports

• Support company logo

• Support monochrome printing

• Support color printing

• Generate identical output every time

---

# Data Source

Engineering Results

↓

Graph Dataset

↓

Report Graph Generator

↓

Report Image

↓

Certificate

---

# Graph Types

Engineering Stress–Strain

True Stress–True Strain

Force–Extension

Force–Time

Extension–Time

Ring Stiffness

Spring Curve

Bending Curve

Control Charts

---

# Report Graph Layout

Title

↓

Graph Area

↓

Legend

↓

Material Information

↓

Axes

↓

Footer

---

# Graph Size

Default

A4 Portrait

Width

160 mm

Height

100 mm

Administrator configurable.

---

# Resolution

Screen

96 DPI

Export

300 DPI

PDF

Vector Preferred

PNG

Lossless

---

# Curves

Displayed

Engineering Curve

True Curve

Reference Curve

Regression Line

Optional

Construction lines

Hidden

---

# Markers Included

Yield

Ultimate Tensile Strength

Necking

Fracture

Maximum

Minimum

Operator Approved Markers

Only

---

# Markers Excluded

Temporary Markers

Construction Markers

Elastic Region Handles

Correction Handles

Debug Objects

Selection Boxes

Mouse Cursor

Hidden Layers

---

# Axes

Horizontal

Engineering Strain

or

Extension

Vertical

Engineering Stress

or

Force

Automatic units

according to test type.

---

# Grid

Major Grid

Enabled

Minor Grid

Optional

Default

Light Gray

---

# Legend

Automatic

Displays

Curve Name

Marker Name

Reference Curve

Regression

Optional

---

# Company Branding

Company Logo

Laboratory Name

ISO 17025 Accreditation Number

Certificate Number

Administrator configurable.

---

# Graph Caption

May include

Material

Standard

Specimen ID

Test Date

Machine ID

Operator

Optional

---

# Color Mode

Full Color

Monochrome

High Contrast

Print Mode

Administrator configurable.

---

# Export Formats

Embedded Excel Chart

PDF

PNG

SVG (Future)

EMF

Clipboard

---

# File Naming

Default

```
CertificateNo_Graph.png
```

Example

```
2026-00125_Graph.png
```

---

# Database

Generated graph image

shall NOT be stored.

Only

generation parameters

are stored.

SQLite

Table

```
tblReportGraph
```

Fields

Template

Theme

ColorMode

ExportFormat

Operator

Timestamp

---

# Error Handling

Missing Dataset

↓

Abort

Missing Marker

↓

Ignore

Missing Logo

↓

Default Logo

Printer Failure

↓

Retry

Export Failure

↓

Abort

Rollback

---

# Future Enhancements

Interactive PDF

SVG Export

Dark Theme

Multiple Graph Layout

Automatic Watermark

Digital Signature

Reserved

---

# Acceptance Criteria

✔ Engineering quality output

✔ Temporary objects hidden

✔ Approved markers only

✔ A4 compatible

✔ PDF compatible

✔ Excel 2019 compatible

✔ SQLite compatible

✔ ISO 17025 report ready

---

End of Document
