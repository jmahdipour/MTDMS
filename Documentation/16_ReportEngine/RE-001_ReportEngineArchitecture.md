# Report Engine Architecture

Document ID : MTDMS-RE-001

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

The Report Engine is responsible for generating all engineering reports, laboratory certificates, summaries, and printable documents from validated engineering data reconstructed from the original TXT file.

The Report Engine performs **no engineering calculations**.

Its responsibility begins only after engineering calculations have been completed and validated.

---

# Objectives

The Report Engine shall

• Generate engineering reports

• Generate laboratory certificates

• Produce printable documents

• Generate PDF reports

• Preserve engineering traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Calculation Engine

↓

Validation

↓

Report Engine

↓

Report

Reports are generated only from validated engineering results.

---

# Engine Position

```
TXT File

↓

Calculation Engine

↓

Validation

↓

Graph Engine

↓

Report Engine

↓

PDF / Print
```

---

# Responsibilities

Generate Engineering Report

Generate Test Certificate

Generate Summary Report

Generate Customer Report

Generate Internal Report

Generate PDF

Generate Excel Report

---

# Report Sources

Validated Engineering Results

Validated Graphs

Material Library

Customer Library

Machine Library

Operator Library

Report Template

Application Settings

---

# Supported Reports

Tensile Test Report

Compression Test Report

Spring Test Report

Ring Stiffness Report

Three Point Bending

Four Point Bending

Raw Data Report

Comparison Report

Statistical Report

Administrator configurable.

---

# Report Components

Header

Customer Information

Material Information

Machine Information

Operator Information

Engineering Results

Engineering Graphs

Summary

Approval Section

Footer

---

# Report Workflow

```
Engineering Results

↓

Select Template

↓

Populate Fields

↓

Insert Graphs

↓

Validate

↓

Generate Report
```

---

# Engineering Independence

The Report Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It creates report copies only.

---

# SQLite Interaction

SQLite stores

Report Metadata

Report History

Certificate History

Audit Information

Generated reports themselves remain external files.

---

# Error Handling

Missing Template

↓

Abort

Missing Engineering Results

↓

Abort

Missing Graph

↓

Generate Report Without Graph (configurable)

Missing Customer

↓

Warning

---

# Performance Targets

Typical Engineering Report

< 1 s

Large Report

< 3 s

PDF Export

< 5 s

---

# Acceptance Criteria

✔ Engineering reports generated

✔ Certificate generation supported

✔ Graph insertion supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT

---

End of Document
