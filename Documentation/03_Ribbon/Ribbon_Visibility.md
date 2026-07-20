# Ribbon Visibility Rules

Document ID : MTDMS-RBN-005

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines when every Ribbon Tab, Group and Control is visible or hidden.

Visibility shall always be controlled by the application state.

The operator shall never manually hide or show Ribbon controls.

---

# Visibility Controller

Ribbon XML

↓

GetVisible()

↓

RibbonController

↓

Application State

↓

Boolean Result

---

# Application States

STATE_STARTUP

Workbook opened

---

STATE_NO_PROJECT

No project loaded

---

STATE_PROJECT

Project opened

---

STATE_TXT_IMPORTED

TXT imported

---

STATE_TXT_VALID

TXT validated

---

STATE_CALCULATED

Engineering calculations completed

---

STATE_GRAPH_READY

Graph generated

---

STATE_REPORT_READY

Report generated

---

STATE_DATABASE_CONNECTED

SQLite connected

---

STATE_ADMIN

Administrator Mode

---

# Ribbon Tab Visibility

| Tab | Visible |
|------|----------|
| Home | Always |
| Import | Always |
| Calculation | Project Loaded |
| Graph | TXT Imported |
| Report | Calculation Finished |
| Database | SQLite Connected |
| Settings | Always |
| Help | Always |

---

# HOME

Always Visible

Groups

Project

Navigation

Recent

Libraries

Application

---

# IMPORT

Always Visible

Groups

TXT

Validation

Utilities

---

# CALCULATION

Visible Only

Project Loaded

AND

TXT Imported

---

Hidden During

Startup

No Project

---

# GRAPH

Visible Only

Engineering Calculation Completed

---

Hidden During

Startup

Project Only

TXT Import

---

# REPORT

Visible Only

Graph Ready

---

Hidden Until

Engineering Results Exist

---

# DATABASE

Visible Only

SQLite Connected

---

Hidden If

SQLite unavailable

Database error

---

# SETTINGS

Always Visible

---

# HELP

Always Visible

---

# HOME Controls

New Project

Always

---

Open Project

Always

---

Save Project

Project Loaded

---

Save As

Project Loaded

---

Close Project

Project Loaded

---

Recent Projects

Always

---

Material Library

Always

---

Standard Library

Always

---

# IMPORT Controls

Browse TXT

Project Loaded

---

Preview TXT

TXT Selected

---

Validate TXT

TXT Imported

---

Import TXT

TXT Valid

---

Reload TXT

TXT Imported

---

Clear TXT

TXT Imported

---

# CALCULATION Controls

Calculate

TXT Valid

---

Recalculate

Calculation Completed

---

Correction

Calculation Completed

---

Young

Calculation Completed

---

Yield

Calculation Completed

---

UTS

Calculation Completed

---

Fracture

Calculation Completed

---

# GRAPH Controls

Zoom

Graph Ready

---

Pan

Graph Ready

---

Crosshair

Graph Ready

---

Grid

Graph Ready

---

Manual Yield

Graph Ready

---

Manual Fracture

Graph Ready

---

Undo

Graph Ready

---

Reset

Graph Ready

---

Export Image

Graph Ready

---

# REPORT Controls

Preview

Report Ready

---

Print

Report Ready

---

PDF

Report Ready

---

Excel

Report Ready

---

Certificate

Report Ready

---

# DATABASE Controls

Projects

SQLite Connected

---

History

SQLite Connected

---

Material Library

Always

---

Standard Library

Always

---

Backup

SQLite Connected

---

Restore

SQLite Connected

---

Compact

SQLite Connected

---

# SETTINGS Controls

Always Visible

General

Units

Theme

Language

TXT

Graph

Calculation

Protection

---

# HELP Controls

Always Visible

User Manual

Developer Manual

About

License

System Information

---

# Administrator Controls

Visible Only

STATE_ADMIN

Includes

Database Maintenance

Workbook Maintenance

Developer Options

Calibration

System Configuration

---

# Hidden Features

Compression

Impact

Fatigue

Hardness

Calibration

SPC

Cloud

Remain hidden until implemented.

---

# Performance

Visibility callback execution

Target

< 10 ms

No worksheet access allowed.

No database queries allowed.

Only application state variables shall be evaluated.

---

# Visibility Priority

1. Workbook State

2. Project State

3. TXT State

4. Calculation State

5. Graph State

6. Report State

7. User Permission

---

End of Document
