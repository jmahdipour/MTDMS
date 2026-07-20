# Ribbon Controller Specification

Document ID : MTDMS-RBN-009

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Workbook

WorkbookTemplate.xlsm

---

# Purpose

RibbonController is the central coordinator of the Ribbon.

Ribbon XML never communicates directly with

- Worksheets
- SQLite
- Engineering Calculations
- Charts

Everything passes through RibbonController.

---

# Architecture

```
Ribbon XML

↓

RibbonController

↓

NavigationController

ProjectController

ImportController

CalculationController

GraphController

ReportController

DatabaseController

SettingsController

HelpController
```

---

# Responsibilities

RibbonController is responsible for

• Ribbon Initialization

• Ribbon Refresh

• Control Visibility

• Control Enable State

• Ribbon Callback Routing

• Ribbon State Management

• Application Mode

---

# Responsibilities NOT Allowed

RibbonController shall never

✘ Calculate Engineering Properties

✘ Read TXT

✘ Write SQLite

✘ Draw Charts

✘ Generate Reports

---

# Main Procedures

```
InitializeRibbon()

InvalidateRibbon()

InvalidateControl()

UpdateRibbonState()

GetApplicationState()

RefreshRibbon()

ResetRibbon()

ShutdownRibbon()
```

---

# InitializeRibbon()

Called From

Workbook_Open()

Tasks

Store Ribbon Reference

Load State

Refresh Controls

Activate Home

---

# InvalidateRibbon()

Purpose

Refresh complete Ribbon.

Equivalent

```
Ribbon.Invalidate
```

Used When

Project Loaded

Language Changed

Settings Changed

---

# InvalidateControl()

Purpose

Refresh one control.

Equivalent

```
Ribbon.InvalidateControl(ID)
```

Preferred over full invalidate whenever possible.

---

# RefreshRibbon()

Updates

Visible Tabs

Visible Groups

Visible Buttons

Enabled Controls

Icons

Labels

---

# UpdateRibbonState()

Reads

Application State

Updates

Internal Ribbon Variables

Calls

RefreshRibbon()

---

# GetApplicationState()

Returns

```
STATE_STARTUP

STATE_PROJECT

STATE_TXT

STATE_VALID

STATE_CALCULATED

STATE_GRAPH

STATE_REPORT

STATE_ADMIN
```

---

# Callback Routing

Example

```
btnCalculate

↓

RibbonController

↓

CalculationController.Calculate()
```

Another Example

```
btnImportTXT

↓

RibbonController

↓

ImportController.ImportTXT()
```

---

# Ribbon Reference

Ribbon reference stored only once.

```
Private pRibbon As IRibbonUI
```

No other module stores Ribbon reference.

---

# State Variables

```
CurrentProject

CurrentMaterial

CurrentStandard

CurrentUser

CurrentWorksheet

CurrentLanguage

SQLiteConnected

TXTImported

CalculationFinished

GraphReady

ReportReady
```

---

# Refresh Priority

1

Application State

↓

2

Visible Tabs

↓

3

Groups

↓

4

Buttons

↓

5

Icons

↓

6

Labels

---

# Error Handling

Every public procedure

```
On Error GoTo ErrorHandler
```

ErrorHandler

↓

Write ERROR_LOG

↓

Display Message

↓

Recover Safe State

---

# Logging

Debug Mode

Logs

Ribbon Loaded

Ribbon Refreshed

State Changed

Control Invalidated

Callback Executed

---

# Performance

Initialize Ribbon

Target

<100 ms

Refresh Ribbon

<50 ms

Invalidate Control

<10 ms

---

# Security

RibbonController

Public Interface Only

Internal Variables

Private

Ribbon Reference

Private

No external module may directly modify Ribbon state.

---

# Future

Theme Manager

Language Manager

Cloud Commands

Plugin Manager

Module Loader

---

# Design Rules

✔ Single RibbonController

✔ Single Ribbon Reference

✔ Controllers perform business logic

✔ RibbonController performs UI logic

✔ Separation of concerns strictly enforced

---

End of Document
