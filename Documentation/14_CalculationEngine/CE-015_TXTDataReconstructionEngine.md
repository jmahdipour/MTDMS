# TXT Data Reconstruction Engine

Document ID : MTDMS-CE-015

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The TXT Data Reconstruction Engine reconstructs the complete engineering dataset directly from the imported machine TXT file every time a test is opened.

This module guarantees that engineering calculations are always regenerated from the original source data.

No engineering result is reused from previous calculations stored in SQLite.

---

# Objectives

The TXT Data Reconstruction Engine shall

• Read the original TXT file

• Reconstruct the engineering dataset

• Regenerate engineering calculations

• Verify data integrity

• Detect modifications

• Eliminate dependency on previously stored engineering values

---

# Fundamental Principle

TXT File

↓

ONLY SOURCE OF ENGINEERING DATA

↓

Engineering Reconstruction

↓

Engineering Calculations

↓

Engineering Results

SQLite

↓

History Only

Configuration

Reports

Audit

Never Engineering Source

---

# Workflow

```
User Opens Test

↓

Locate Original TXT

↓

Verify SHA256

↓

Verify File Size

↓

Verify Import Metadata

↓

Read TXT Again

↓

Rebuild Dataset

↓

Run Calculation Engine

↓

Run Validation

↓

Generate Graph

↓

Generate Report
```

---

# Reconstruction Inputs

Original TXT File

Geometry

Material Library

Calculation Profile

Machine Configuration

Standard

Operator Parameters

Application Settings

---

# Reconstruction Outputs

Engineering Stress

Engineering Strain

True Stress

True Strain

Young's Modulus

Yield Strength

Ultimate Strength

Fracture Position

Graphs

Validation

Reports

Certificates

Everything is regenerated.

---

# File Verification

Before reconstruction

verify

TXT Exists

TXT Readable

SHA256 Match

File Size Match

Encoding Valid

Header Valid

Measurement Table Valid

---

# Modified TXT Detection

If

SHA256 differs

↓

Display Warning

Operator chooses

Continue

or

Abort

The modification is recorded in the audit trail.

---

# Missing TXT File

If

TXT cannot be found

↓

Engineering reconstruction

is impossible.

Previously stored engineering values

shall never be used automatically.

The operator shall receive a critical warning.

---

# SQLite Interaction

SQLite stores

TXT metadata

SHA256

Import date

Results

Reports

Audit

SQLite is never treated as the engineering source.

---

# Recalculation Policy

Every time a report is opened

↓

Recalculate

Every time a certificate is generated

↓

Recalculate

Every time a graph is displayed

↓

Recalculate (configurable)

Administrator may disable automatic recalculation for very large datasets.

---

# Engineering Independence

The reconstruction engine ensures

all engineering calculations originate from

the TXT file.

This guarantees

full reproducibility

and

compliance with ISO/IEC 17025.

---

# Error Handling

TXT Missing

↓

Abort

SHA256 Different

↓

Warning

Encoding Invalid

↓

Abort

Measurement Table Invalid

↓

Abort

Geometry Missing

↓

Abort

---

# Performance Targets

TXT Verification

< 100 ms

Dataset Reconstruction

< 300 ms

Complete Engineering Rebuild

< 2 s

Typical Tensile Test

---

# Acceptance Criteria

✔ Engineering data reconstructed from TXT

✔ SQLite never used as engineering source

✔ SHA256 verification supported

✔ Automatic recalculation supported

✔ Excel 2019 compatible

✔ SQLite compatible

✔ Complete engineering reproducibility

✔ ISO/IEC 17025 compliant

✔ Full audit trace

---

End of Document
