# Report Engine Architecture

Document ID : MTDMS-RPT-001

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Report Engine

Status

Production

---

# Purpose

This document defines the architecture of the Report Engine used by MTDMS.

The Report Engine is responsible for producing official laboratory reports and certificates compliant with

• ISO 17025

• ISO 6892-1

• ASTM Standards

• National Standards (INSO)

The Report Engine is completely independent from

Engineering Calculations

Graph Engine

Import Engine

Database Layer

---

# Design Philosophy

Engineering Modules

↓

Generate Results

↓

Report Engine

↓

Certificate

↓

PDF

↓

Print

↓

Archive

Reports never perform calculations.

They only display approved engineering results.

---

# Report Categories

Mechanical Tests

Tensile

Bending

Compression

Spring

Ring Stiffness

Impact

Hardness

Chemical Analysis

Calibration

Quality Control

Custom Reports

---

# Report Pipeline

```
SQLite

↓

Engineering Results

↓

Graph Engine

↓

Template Manager

↓

Report Generator

↓

Preview

↓

PDF

↓

Printer

↓

Archive
```

---

# Report Components

Header

Customer Information

Material Information

Test Information

Results Table

Engineering Graph

Remarks

Standards

Approval

Footer

---

# Header

Contains

Laboratory Name

Logo

ISO 17025 Accreditation

Certificate Number

Page Number

Document Revision

---

# Customer Information

Customer Name

Project

Purchase Order

Sample ID

Heat Number

Batch Number

Operator

---

# Material Information

Material Name

Standard

Grade

Dimensions

Original Area

Specimen Type

Heat Treatment

Optional

---

# Test Information

Machine

Load Cell

Extensometer

Software Version

Operator

Test Date

Test Time

Ambient Temperature

Humidity

Optional

---

# Results Table

Displays only

Approved Results

Engineering Units

Configured Precision

Pass / Fail

Optional

---

# Graph Section

Obtained from

Graph Engine

Displays

Corrected Graph

Approved Markers

No Construction Lines

No Temporary Objects

---

# Remarks

Operator Notes

Customer Notes

Engineering Notes

Failure Mode

Optional

---

# Approval Section

Prepared By

Verified By

Approved By

Digital Signature

Optional

---

# Footer

Laboratory Address

Telephone

Email

Website

Confidentiality Statement

Revision

---

# Report Generator

The generator receives

Approved Results

↓

Template

↓

Company Configuration

↓

Language

↓

Creates

Final Report

---

# Languages

Persian

English

Bilingual

Future

Arabic

Reserved

---

# Report Number

Automatic

```
YYYY-XXXXX
```

Example

```
2026-00125
```

Report numbers shall never repeat.

---

# Units

Automatically selected

According to

Test Type

Standard

Customer Requirements

---

# Database

SQLite

Tables

```
tblReport

tblReportTemplate

tblReportHistory

tblApproval
```

---

# Preview

Supports

Zoom

Print Preview

Page Navigation

Export

No editing

---

# Performance

Report Generation

< 2 seconds

Preview

Instant

PDF Export

< 5 seconds

---

# Error Handling

Missing Results

↓

Abort

Missing Template

↓

Default Template

Missing Logo

↓

Default Logo

Database Failure

↓

Abort

---

# Future Enhancements

Barcode

QR Code

Electronic Signature

Cloud Archive

Automatic Email

Multi-page Reports

Reserved

---

# Acceptance Criteria

✔ ISO 17025 compatible

✔ Independent architecture

✔ Uses approved results only

✔ Supports PDF

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Multi-language ready

---

End of Document
