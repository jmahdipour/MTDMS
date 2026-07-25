# Engineering Graph Export Engine

Document ID : MTDMS-GE-013

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

The Engineering Graph Export Engine exports engineering graphs generated from validated datasets into external file formats without modifying engineering data.

The exported graphs are intended for reports, presentations, customer documentation, quality records, and technical publications.

---

# Objectives

The Graph Export Engine shall

• Export engineering graphs

• Preserve engineering quality

• Support multiple file formats

• Preserve vector quality when possible

• Maintain engineering traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Graph Engine

↓

Export Engine

↓

External File

The exported graph always originates from validated engineering data.

---

# Supported Export Formats

PNG

JPEG

BMP

EMF

SVG (future)

PDF

Excel Chart

Administrator configurable.

---

# Workflow

```
Engineering Dataset

↓

Graph Generation

↓

Apply Export Style

↓

Generate File

↓

Save

↓

Audit
```

---

# Vector Export

Preferred

EMF

PDF

Future

SVG

Vector export shall be used whenever possible to preserve engineering quality.

---

# Raster Export

Supported

PNG

JPEG

BMP

Administrator configurable.

---

# Image Resolution

Supported

150 DPI

300 DPI

600 DPI

Custom

Administrator configurable.

---

# Export Naming

Recommended

```
ReportNumber_GraphType_YYYYMMDD_HHMMSS
```

Example

```
TR-2026-015_StressStrain_20260725_143015.png
```

Administrator configurable.

---

# Export Metadata

Optional metadata

Report Number

Material

Customer

Operator

Machine

Standard

Date

Software Version

may be embedded where supported.

---

# Export Styles

Publication

Presentation

Customer

Black & White

Laboratory

Administrator configurable.

---

# Automatic Cropping

Optional

Remove Empty Margins

Center Graph

Maintain Aspect Ratio

Administrator configurable.

---

# Batch Export

The engine may export

All Graphs

Selected Graphs

Current Graph

Comparison Graphs

Administrator configurable.

---

# Engineering Independence

The Graph Export Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Export creates copies only.

---

# SQLite Interaction

SQLite stores

Export History

Export Format

Destination Folder

Operator

Timestamp

Exported image files are not stored inside SQLite.

---

# Error Handling

Invalid Folder

↓

Abort

Disk Full

↓

Abort

Permission Denied

↓

Abort

Missing Graph

↓

Abort

Unsupported Format

↓

Reject

---

# Performance Targets

PNG Export

< 300 ms

PDF Export

< 1 s

Batch Export (10 Graphs)

< 5 s

---

# Acceptance Criteria

✔ Multiple export formats supported

✔ Vector export supported

✔ Batch export supported

✔ Export metadata supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT

---

End of Document
