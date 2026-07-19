# Workbook Architecture

Document ID : MTDMS-WB-001

Version : 0.1.0

Platform

Microsoft Excel 2019

Programming Language

VBA

Ribbon XML

Database

SQLite

Input

TXT Only

---

# Purpose

This document defines the internal architecture of the workbook.

WorkbookTemplate.xlsm is the entire application.

Excel is only the runtime environment.

---

# Workbook Philosophy

Workbook

↓

Application

↓

Worksheets

↓

Application Pages

↓

Ribbon

↓

Navigation

↓

VBA

↓

Business Logic

---

# Workbook File

WorkbookTemplate.xlsm

Only one workbook shall exist.

Multiple workbook architecture is prohibited.

---

# Workbook Layers

Presentation Layer

↓

Business Layer

↓

Calculation Layer

↓

Persistence Layer

---

# Presentation Layer

Visible Worksheets

HOME

IMPORT

ANALYSIS

GRAPH

REPORT

Purpose

Display only.

No engineering calculations.

---

# Business Layer

Ribbon

Ribbon Controller

Navigation Controller

Project Controller

TXT Controller

Graph Controller

Report Controller

Purpose

Coordinates user actions.

---

# Calculation Layer

Hidden Worksheet

ENGINEERING

VBA Modules

Stress

Strain

Young

Yield

UTS

Fracture

Correction

Purpose

All engineering calculations.

---

# Persistence Layer

SQLite

Projects

History

Material Library

Standard Library

Settings

Results

---

# Workbook Hierarchy

Workbook

↓

Ribbon

↓

Worksheet

↓

Table

↓

Named Range

↓

Cell

---

# Visible Worksheets

HOME

Application Dashboard

IMPORT

TXT Import

ANALYSIS

Engineering Workspace

GRAPH

Interactive Charts

REPORT

Report Preview

---

# Hidden Worksheets

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

# Worksheet Communication

Worksheet

↓

Controller

↓

Calculation

↓

Database

Worksheet-to-Worksheet communication is forbidden.

---

# Data Flow

TXT

↓

RAW_DATA

↓

ENGINEERING

↓

RESULT

↓

GRAPH

↓

REPORT

↓

SQLite

---

# Workbook Startup

Workbook_Open()

↓

Initialize System

↓

Load Settings

↓

Connect SQLite

↓

Load Material Library

↓

Open HOME

---

# Workbook Shutdown

Workbook_BeforeClose()

↓

Save Settings

↓

Backup

↓

Close SQLite

↓

Release Memory

---

# Memory Rules

RAW_DATA

Stores imported TXT only.

ENGINEERING

Stores calculated values only.

RESULT

Stores report-ready values only.

---

# Protection

Visible Worksheets

Protected

Hidden Worksheets

VeryHidden

Workbook Structure

Locked

VBA Project

Password Protected

---

# Performance Rules

Maximum TXT Rows

100000

Target Workbook Opening

< 2 sec

TXT Import

< 5 sec

Graph Refresh

< 1 sec

---

# Design Constraints

✔ Excel 2019 Only

✔ VBA Only

✔ Ribbon XML Only

✔ SQLite Only

✔ TXT Only

✘ UserForms

✘ ActiveX

✘ External Add-ins

---

# Future Expansion

Compression Module

Impact Module

Fatigue Module

Calibration Module

SPC Module

Multi-language Support

---

End of Document
