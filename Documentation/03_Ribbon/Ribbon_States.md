# Ribbon State Management

Document ID : MTDMS-RBN-008

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines how Ribbon controls react to application state changes.

Ribbon behavior shall always reflect the current workflow.

Users shall never be able to execute commands in an invalid sequence.

---

# State Machine

```
Application Start

↓

HOME

↓

New Project

↓

Project Open

↓

TXT Selected

↓

TXT Imported

↓

TXT Validated

↓

Engineering Calculation

↓

Graph Ready

↓

Report Ready

↓

Project Saved

↓

Close Project

↓

HOME
```

---

# State Definitions

## STATE_STARTUP

Workbook just opened.

Available Tabs

- Home
- Import
- Settings
- Help

Disabled

- Calculation
- Graph
- Report
- Database

---

## STATE_PROJECT_OPEN

Project created or opened.

Enabled

- Import

Disabled

- Graph
- Report

---

## STATE_TXT_SELECTED

TXT file selected.

Enabled

- Preview
- Validate

Disabled

- Calculate

---

## STATE_TXT_IMPORTED

TXT successfully imported.

Enabled

- Validate
- Reload
- Clear

---

## STATE_TXT_VALID

TXT successfully validated.

Enabled

- Calculate

---

## STATE_CALCULATED

Engineering calculations finished.

Enabled

- Graph
- Export
- Report Preview

---

## STATE_GRAPH_READY

Stress-Strain graph generated.

Enabled

- Zoom
- Pan
- Crosshair
- Manual Yield
- Manual Fracture

---

## STATE_REPORT_READY

Report generated.

Enabled

- PDF
- Print
- Excel Export

---

## STATE_DATABASE_CONNECTED

SQLite successfully connected.

Enabled

- Project History
- Material Library
- Standard Library
- Backup
- Restore

---

## STATE_ADMIN

Administrator logged in.

Additional Tabs

Maintenance

Developer

Calibration

Diagnostics

---

# Button Enable Matrix

| Button | Startup | Project | TXT | Valid | Calc | Graph | Report |
|----------|:------:|:------:|:---:|:-----:|:----:|:-----:|:------:|
| New Project | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Open Project | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Browse TXT | ✖ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Validate | ✖ | ✖ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Calculate | ✖ | ✖ | ✖ | ✔ | ✔ | ✔ | ✔ |
| Graph | ✖ | ✖ | ✖ | ✖ | ✔ | ✔ | ✔ |
| Report | ✖ | ✖ | ✖ | ✖ | ✖ | ✔ | ✔ |
| PDF | ✖ | ✖ | ✖ | ✖ | ✖ | ✖ | ✔ |

---

# Automatic Ribbon Refresh

Ribbon shall refresh automatically after

- Project Open
- Project Close
- TXT Import
- TXT Validation
- Calculation
- Graph Generation
- Report Generation
- SQLite Connection
- Settings Change
- Language Change

---

# Ribbon Invalidation

RibbonController shall call

```
Ribbon.Invalidate
```

when

State changes.

For individual controls

```
Ribbon.InvalidateControl(ID)
```

shall be preferred.

---

# State Transition Rules

Illegal transitions are prohibited.

Examples

Not Allowed

```
Startup

↓

Generate Report
```

Not Allowed

```
TXT Imported

↓

Print Report
```

Allowed

```
TXT Valid

↓

Calculate

↓

Graph

↓

Report
```

---

# Error State

If any controller returns an error

Ribbon shall

Disable

- Graph
- Report

Enable

- Import
- Settings
- Help

Display status

```
Calculation Error
```

---

# Recovery State

After successful recalculation

Ribbon returns automatically to

STATE_CALCULATED

without restarting the workbook.

---

# Future States

STATE_COMPRESSION

STATE_IMPACT

STATE_FATIGUE

STATE_CALIBRATION

STATE_CLOUD

Reserved for future versions.

---

# Design Rules

✔ Ribbon state is controlled only by the application state.

✔ Worksheets shall never enable or disable Ribbon controls directly.

✔ All state changes shall pass through RibbonController.

✔ Every state transition shall be logged in Debug mode.

---

End of Document
