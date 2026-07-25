# PDF Export Engine

Document ID : MTDMS-RE-009

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

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

The PDF Export Engine converts engineering reports and laboratory certificates into secure, high-quality PDF documents.

PDF files are generated only from validated reports created by the Report Engine.

The engine performs **no engineering calculations**.

---

# Objectives

The PDF Export Engine shall

• Export engineering reports as PDF

• Preserve engineering quality

• Preserve report formatting

• Support laboratory archiving

• Maintain engineering traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Engineering Report

↓

PDF Engine

↓

PDF Document

The PDF is a published copy of an approved engineering report.

---

# Supported Sources

Engineering Test Report

Laboratory Certificate

Comparison Report

Summary Report

Customer Report

Administrator configurable.

---

# Workflow

```
Validated Report

↓

Prepare Print Layout

↓

Embed Graphs

↓

Generate PDF

↓

Save

↓

Audit
```

---

# PDF Quality

Preferred

Vector Graphics

Embedded Fonts

High Resolution

Searchable Text

Selectable Text

Rasterization shall be avoided whenever possible.

---

# Supported Paper Sizes

A4 Portrait

A4 Landscape

Letter

Custom

Administrator configurable.

---

# PDF Metadata

The PDF may include

Title

Subject

Author

Keywords

Laboratory

Report Number

Revision

Creation Date

Software Version

Administrator configurable.

---

# File Naming

Recommended

```
ReportNumber_Revision.pdf
```

Example

```
TR-2026-00125_R01.pdf
```

Administrator configurable.

---

# Security

Optional

Read Only

Print Allowed

Copy Disabled

Password Protection (future)

Digital Signature (future)

Administrator configurable.

---

# Embedded Graphs

Engineering graphs are inserted directly from the Graph Engine.

Graphs shall preserve

Aspect Ratio

Resolution

Engineering Labels

Vector Quality

---

# Multi-Page Reports

Supported

Automatic Page Break

Table Continuation

Header Repetition

Footer Repetition

Page Numbering

---

# Engineering Independence

The PDF Export Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

PDF generation is read-only.

---

# SQLite Interaction

SQLite stores

PDF Export History

Destination

Operator

Timestamp

Revision

Audit Information

PDF files remain external documents.

---

# Error Handling

Destination Missing

↓

Abort

Disk Full

↓

Abort

PDF Generator Failure

↓

Retry

Missing Report

↓

Abort

---

# Performance Targets

Typical Report

< 3 s

Large Report

< 8 s

Multiple Reports

< 30 s

---

# Acceptance Criteria

✔ High-quality PDF export

✔ Embedded engineering graphs

✔ Searchable PDF

✔ Automatic metadata

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
