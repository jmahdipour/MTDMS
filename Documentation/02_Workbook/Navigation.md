# Workbook Navigation Specification

Document ID : MTDMS-WB-007

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

Ribbon XML

---

# Purpose

This document defines how users navigate inside the workbook.

The workbook behaves as a software application.

Users shall never navigate using Excel worksheet tabs.

Navigation shall be performed exclusively through the Ribbon.

---

# Navigation Philosophy

```
Ribbon

↓

Navigation Controller

↓

Worksheet Activation

↓

Initialize Worksheet

↓

Refresh UI

↓

Ready
```

---

# Navigation Sequence

```
HOME

↓

IMPORT

↓

ANALYSIS

↓

GRAPH

↓

REPORT

↓

HOME
```

---

# Startup Navigation

Workbook_Open()

↓

Initialize Workbook

↓

Load Settings

↓

Load Material Library

↓

Connect SQLite

↓

Activate HOME

↓

Ready

---

# Shutdown Navigation

Workbook_BeforeClose()

↓

Check Modified Project

↓

Ask Save

↓

Save Settings

↓

Backup Database

↓

Close Workbook

---

# Ribbon Navigation

Only Ribbon Buttons are allowed to activate worksheets.

Allowed

```
btnHome

btnImport

btnAnalysis

btnGraph

btnReport

btnDatabase

btnSettings

btnHelp
```

---

# Worksheet Tabs

Worksheet Tabs

Hidden

Navigation by tabs

Forbidden

---

# Keyboard Navigation

Allowed

Tab

Enter

Arrow Keys

Page Up

Page Down

---

Forbidden

Ctrl + PageUp

Ctrl + PageDown

Worksheet Shortcuts

---

# Navigation Controller

Single VBA Module

```
NavigationController.bas
```

Main Procedure

```
NavigateTo(PageName)
```

Example

```
NavigateTo("GRAPH")
```

---

# Before Navigation

Controller shall

Save Current Worksheet

Refresh Status

Validate Current Page

Update Header

---

# After Navigation

Controller shall

Activate Worksheet

Refresh Header

Refresh Footer

Refresh Status

Initialize Controls

---

# HOME Navigation

Buttons

Import

↓

IMPORT

Recent Project

↓

Load Project

Settings

↓

SETTINGS

---

# IMPORT Navigation

Import Completed

↓

ANALYSIS

Cancel

↓

HOME

---

# ANALYSIS Navigation

Calculate

↓

GRAPH

Back

↓

IMPORT

---

# GRAPH Navigation

Report

↓

REPORT

Back

↓

ANALYSIS

---

# REPORT Navigation

Finish

↓

HOME

Print

↓

Remain REPORT

PDF

↓

Remain REPORT

---

# Hidden Worksheet Access

Not Allowed

RAW_DATA

ENGINEERING

RESULT

SYSTEM

SETTINGS

ERROR_LOG

HISTORY

MATERIAL_DB

STANDARD_DB

Only VBA may activate these sheets.

---

# Breadcrumb

Every visible worksheet displays

```
HOME

>

IMPORT

>

ANALYSIS
```

Current page highlighted.

---

# Status Bar

Displays

Current Page

Current Project

Current Material

SQLite Status

TXT Status

Workbook Version

---

# Error Navigation

If destination worksheet unavailable

↓

Show Error

↓

Return HOME

↓

Write Error Log

---

# Refresh Rules

Navigation always refreshes

Header

Footer

Status

Current Project

Current Material

Current Standard

Current User

---

# Future

Navigation History

Favorites

Search

Recent Pages

Split View

Multiple Project Windows

---

# Navigation Rules

✔ Ribbon Only

✔ Worksheet Tabs Hidden

✔ Central Navigation Controller

✔ Automatic Header Refresh

✔ Automatic Status Refresh

✔ Automatic Footer Refresh

✔ Hidden Worksheets Accessible Only Through VBA

---

End of Document
