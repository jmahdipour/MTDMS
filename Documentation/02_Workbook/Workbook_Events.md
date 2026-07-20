# Workbook Events Specification

Document ID : MTDMS-WB-008

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

Language

VBA

---

# Purpose

This document defines every Workbook Event used by MTDMS.

Workbook Events coordinate application behavior.

Engineering calculations shall never be executed directly inside Workbook Events.

Workbook Events only call Controller procedures.

---

# Event Philosophy

Workbook Event

↓

Controller

↓

Business Logic

↓

Worksheet

↓

Database

---

# Supported Events

Workbook_Open

Workbook_BeforeClose

Workbook_BeforeSave

Workbook_AfterSave

Workbook_SheetActivate

Workbook_SheetDeactivate

Workbook_SheetChange

Workbook_SheetSelectionChange

Workbook_WindowResize

Workbook_WindowActivate

Workbook_WindowDeactivate

---

# Workbook_Open

Purpose

Application Startup

Sequence

Initialize Environment

↓

Load Settings

↓

Connect SQLite

↓

Load Material Library

↓

Load Standard Library

↓

Initialize Ribbon

↓

Refresh Header

↓

Refresh Footer

↓

Navigate HOME

↓

Ready

Engineering Calculations

NO

---

# Workbook_BeforeClose

Purpose

Safe Shutdown

Sequence

Check Unsaved Project

↓

Ask User

↓

Save Project

↓

Backup SQLite

↓

Save Settings

↓

Disconnect Database

↓

Close Workbook

---

# Workbook_BeforeSave

Purpose

Validation

Checks

Project Name

Material

TXT Imported

No Database Errors

No Invalid Results

---

# Workbook_AfterSave

Purpose

Update History

Sequence

Save Timestamp

↓

Update History

↓

Refresh Status

---

# Workbook_SheetActivate

Purpose

Refresh Current Page

Actions

Refresh Header

Refresh Footer

Refresh Status

Refresh Ribbon

No Engineering Calculations

---

# Workbook_SheetDeactivate

Purpose

Save Temporary UI State

Actions

Cursor Position

Selected Table

Graph Zoom

---

# Workbook_SheetChange

Purpose

Detect User Input

Allowed Worksheets

IMPORT

ANALYSIS

REPORT

Ignored

ENGINEERING

RAW_DATA

SYSTEM

SETTINGS

---

# Workbook_SheetSelectionChange

Purpose

Update Cursor Information

Used In

GRAPH

REPORT

ANALYSIS

---

# Workbook_WindowResize

Purpose

Responsive Layout

Actions

Resize Panels

Resize Graph

Resize Tables

Reposition Controls

---

# Workbook_WindowActivate

Purpose

Restore Application State

Actions

Refresh Ribbon

Refresh Header

Refresh Status

---

# Workbook_WindowDeactivate

Purpose

Suspend Refresh

Actions

Pause Timer

Save Temporary State

---

# Forbidden Events

Worksheet_Calculate

Worksheet_Change Engineering Logic

Worksheet_Activate Engineering Logic

Application.OnTime Calculation

Any Recursive Event

---

# Controller Modules

WorkbookController.bas

NavigationController.bas

ProjectController.bas

DatabaseController.bas

RibbonController.bas

---

# Error Handling

Every Workbook Event

Must

Use Error Handler

Log Error

Continue Safe Execution

---

# Event Execution Rules

✔ Never perform engineering calculations.

✔ Never access SQLite directly.

✔ Never modify hidden worksheets.

✔ Never modify graphs directly.

✔ Only call Controllers.

---

# Performance

Workbook_Open

< 2 sec

SheetActivate

< 100 ms

WindowResize

< 100 ms

SheetSelectionChange

< 20 ms

---

# Future Events

Auto Backup Timer

Idle Detection

License Validation

Cloud Synchronization

Automatic Update Checker

---

End of Document
