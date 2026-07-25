# Engineering Graph Printing Engine

Document ID : MTDMS-GE-012

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

The Engineering Graph Printing Engine prepares engineering graphs for printing and inclusion in reports, certificates, and PDF documents.

The engine guarantees that printed graphs are generated directly from validated engineering datasets reconstructed from the original TXT file.

---

# Objectives

The Graph Printing Engine shall

• Produce print-ready engineering graphs

• Support laboratory reports

• Support certificates

• Support PDF export

• Preserve engineering readability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Graph Engine

↓

Print Engine

↓

Printed Graph

The printed graph is always regenerated from engineering data.

---

# Supported Output

Excel Worksheet

Laboratory Report

Certificate

PDF

PNG

EMF

Administrator configurable.

---

# Print Workflow

```
Engineering Dataset

↓

Graph Generation

↓

Apply Print Style

↓

Hide Temporary Objects

↓

Print Preview

↓

Print / PDF
```

---

# Print Style

The print engine shall apply

White Background

Black Axes

Optimized Grid

Publication Fonts

Report Margins

High Resolution

---

# Hidden Objects

The following objects shall normally be removed from printed output

Temporary Construction Lines

Debug Information

Inspection Cursor

Temporary Markers

Selection Boxes

Zoom Window

Administrator configurable.

---

# Visible Objects

Printed graphs may include

Engineering Curve

Yield Marker

Ultimate Strength

Fracture Point

Reference Deformation

Legend

Axis Labels

Graph Title

Report Number

Material

Standard

depending on report configuration.

---

# Resolution

Minimum

300 DPI

Preferred

600 DPI

Administrator configurable.

---

# Page Formats

Supported

A4 Portrait

A4 Landscape

Letter

Custom

Administrator configurable.

---

# Scaling

Supported

Fit to Page

Actual Size

Maintain Aspect Ratio

Administrator configurable.

---

# Graph Metadata

Optional metadata

Report Number

Certificate Number

Material

Operator

Date

Standard

Machine

Software Version

---

# PDF Export

The engine shall generate

vector-quality PDF graphics whenever possible.

Rasterization shall be avoided.

---

# Engineering Independence

The Graph Printing Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It prepares printed output only.

---

# SQLite Interaction

SQLite stores

Print History

Print Settings

Operator

Timestamp

Destination

Printed graphs themselves are regenerated.

---

# Error Handling

Printer Not Found

↓

Abort

PDF Failure

↓

Retry

Missing Graph

↓

Abort

Page Too Large

↓

Scale Automatically

---

# Performance Targets

Print Preparation

< 500 ms

PDF Preparation

< 1 s

Preview Refresh

< 300 ms

---

# Acceptance Criteria

✔ Print-ready graphs generated

✔ PDF supported

✔ Temporary objects hidden

✔ Publication-quality output

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
