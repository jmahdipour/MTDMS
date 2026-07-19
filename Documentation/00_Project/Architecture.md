# System Architecture

Document ID: MTDMS-ARC-001

Version: 0.1.0

Status: Draft

---

# 1. Purpose

This document defines the software architecture of the Mechanical Testing Data Management System (MTDMS).

The architecture follows a layered design to maximize maintainability, extensibility and reliability.

---

# 2. Technology Stack

Platform

Microsoft Excel 2019

Programming Language

Visual Basic for Applications (VBA)

User Interface

Ribbon XML

Database

SQLite

Input

TXT Files

Output

PDF

Excel

SQLite

---

# 3. High-Level Architecture

```
TXT File

↓

Import Layer

↓

Validation Layer

↓

Calculation Layer

↓

Graph Layer

↓

Report Layer

↓

Database Layer
```

---

# 4. Layer Description

## Layer 1

Import Layer

Responsibilities

• Open TXT

• Read file

• Detect format

• Parse columns

Modules

TXTParser

TXTImport

TXTPreview

TXTMapping

---

## Layer 2

Validation Layer

Responsibilities

Validate

Header

Rows

Columns

Missing values

Invalid values

Machine compatibility

Output

Validated Dataset

---

## Layer 3

Calculation Layer

Responsibilities

Engineering calculations

Modules

Stress

Strain

Young

Yield

UTS

Fracture

Correction

Regression

---

## Layer 4

Graph Layer

Responsibilities

Graph generation

Graph correction

Crosshair

Zoom

Pan

Manual Yield

Manual Fracture

Export

---

## Layer 5

Report Layer

Responsibilities

Report generation

PDF

Excel

Print

Summary

---

## Layer 6

Database Layer

Responsibilities

SQLite

Projects

Materials

Standards

History

Settings

Results

---

# 5. Workbook Architecture

Workbook

```
WorkbookTemplate.xlsm
```

Worksheets

HOME

IMPORT

ANALYSIS

GRAPH

REPORT

RAW_DATA

ENGINEERING

RESULT

MATERIAL_DB

STANDARD_DB

SETTINGS

SYSTEM

ERROR_LOG

HISTORY

---

# 6. Ribbon Architecture

Ribbon Tabs

Home

Import

Calculation

Graph

Report

Database

Settings

Help

Ribbon contains no engineering logic.

Ribbon only calls VBA procedures.

---

# 7. VBA Architecture

```
Modules

Classes

Ribbon

Import

Calculation

Graph

Report

SQLite

Utilities
```

Each module has a single responsibility.

---

# 8. Data Flow

TXT

↓

Import

↓

Validation

↓

Engineering Dataset

↓

Calculations

↓

Graph

↓

Results

↓

Report

↓

SQLite

---

# 9. Graph Engine

Input

Engineering Dataset

Output

Interactive Graph

Features

Zoom

Pan

Cursor

Correction

Yield Selection

Fracture Selection

---

# 10. Report Engine

Input

Result Table

Output

Engineering Report

PDF

Excel

Print

---

# 11. Database

SQLite

Tables

Projects

Materials

Standards

Results

History

Settings

Users (future)

---

# 12. Error Handling

Central Error Handler

Log

Timestamp

Module

Procedure

Message

Severity

Recovery Action

---

# 13. Design Principles

Single Responsibility

Loose Coupling

High Cohesion

Reusable Modules

No Circular Dependencies

No Worksheet Logic

No Hidden Calculations Outside ENGINEERING Sheet

---

# 14. Coding Rules

No UserForms

No ActiveX

No Worksheet Event Calculations

No Hard-Coded Cell References

All engineering calculations executed through dedicated modules.

---

# 15. Future Expansion

Compression

Fatigue

Impact

Hardness

Calibration

SPC

Cloud Synchronization

REST API

---

End of Document
