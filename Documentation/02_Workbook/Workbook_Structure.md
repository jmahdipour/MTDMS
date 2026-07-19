# Workbook Structure

Document ID : MTDMS-WB-002

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines every worksheet contained in the workbook.

It also specifies which worksheets are visible, hidden or system worksheets.

---

# Workbook

```
WorkbookTemplate.xlsm
```

---

# Worksheet List

| No | Worksheet | Visibility | Purpose |
|----|------------|------------|----------|
| 01 | HOME | Visible | Main Dashboard |
| 02 | IMPORT | Visible | TXT Import |
| 03 | ANALYSIS | Visible | Engineering Analysis |
| 04 | GRAPH | Visible | Interactive Graph |
| 05 | REPORT | Visible | Report Preview |
| 06 | RAW_DATA | VeryHidden | Imported TXT Data |
| 07 | ENGINEERING | VeryHidden | Engineering Calculations |
| 08 | RESULT | VeryHidden | Final Results |
| 09 | MATERIAL_DB | VeryHidden | Material Library |
| 10 | STANDARD_DB | VeryHidden | Standards Library |
| 11 | SETTINGS | VeryHidden | Application Settings |
| 12 | HISTORY | VeryHidden | Project History |
| 13 | ERROR_LOG | VeryHidden | Runtime Errors |
| 14 | SYSTEM | VeryHidden | Internal Variables |

---

# HOME

Purpose

Main application dashboard.

Contains

Project Information

Recent Projects

Quick Access

System Status

Navigation

Engineering Calculations

NO

---

# IMPORT

Purpose

TXT Import.

Contains

Browse

Preview

Validation

Import

Engineering Calculations

NO

---

# ANALYSIS

Purpose

Engineering calculations.

Contains

Specimen Information

Stress

Strain

Mechanical Properties

Engineering Result Table

Engineering Calculations

YES

---

# GRAPH

Purpose

Interactive graph.

Contains

Stress–Strain Graph

Force–Stroke Graph

Zoom

Pan

Crosshair

Manual Yield

Manual Fracture

Engineering Calculations

NO

---

# REPORT

Purpose

Report preview.

Contains

Report Header

Result Table

Graph

Signature Area

Export Buttons

Engineering Calculations

NO

---

# RAW_DATA

Visibility

VeryHidden

Purpose

Stores imported TXT exactly as received.

Never edited manually.

Never formatted.

One record per imported line.

---

# ENGINEERING

Visibility

VeryHidden

Purpose

Intermediate calculations.

Contains

Stress

Strain

True Stress

True Strain

Young

Yield

UTS

Regression

Correction

---

# RESULT

Visibility

VeryHidden

Purpose

Stores only validated final values.

Used by

GRAPH

REPORT

SQLite

---

# MATERIAL_DB

Visibility

VeryHidden

Purpose

Material Library.

Contains

Material Name

Young's Modulus

Yield

UTS

Density

Poisson Ratio

Reference

---

# STANDARD_DB

Visibility

VeryHidden

Purpose

Standard Library.

Contains

ISO

ASTM

DIN

INSO

Calculation Rules

---

# SETTINGS

Visibility

VeryHidden

Purpose

Application Configuration.

Contains

Units

Theme

Language

Graph Options

TXT Options

Ribbon Options

---

# HISTORY

Visibility

VeryHidden

Purpose

Project History.

Contains

Project ID

Date

Operator

Material

Machine

Result

---

# ERROR_LOG

Visibility

VeryHidden

Purpose

Stores runtime errors.

Columns

Timestamp

Procedure

Module

Description

Severity

---

# SYSTEM

Visibility

VeryHidden

Purpose

Stores application variables.

Examples

Current Project

Workbook Version

SQLite Status

TXT Status

Application State

---

# Worksheet Naming Rules

Worksheet names shall remain fixed.

Renaming worksheets is prohibited.

---

# Worksheet Order

Worksheets shall always remain in the defined order.

No worksheet insertion between existing sheets.

---

# Protection

Visible Worksheets

Protected

Hidden Worksheets

VeryHidden

Workbook Structure

Locked

---

# Future Worksheets

Compression

Impact

Fatigue

Calibration

SPC

Dashboard+

---

End of Document
