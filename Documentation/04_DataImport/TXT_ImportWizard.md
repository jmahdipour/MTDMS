# TXT Import Wizard

Document ID : MTDMS-IMP-044

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Interface

Ribbon UI

Database

SQLite

Application

MTDMS

---

# Purpose

This document defines the Excel Ribbon based Import Wizard.

Unlike traditional software, MTDMS does not use UserForms.

All operator interaction shall be performed using:

- Ribbon Controls
- Excel Task Pane (Future)
- Excel Worksheets
- Status Bar

This design provides maximum compatibility with Microsoft Excel 2019.

---

# Design Philosophy

```
Ribbon

↓

Import Wizard

↓

Parser

↓

Validation

↓

Engineering

↓

Ready
```

The wizard is only responsible for guiding the operator.

No engineering calculations are performed here.

---

# Ribbon Group

Tab

```
MTDMS
```

Group

```
Data Import
```

---

# Ribbon Controls

| Control | Type |
|----------|------|
| Select TXT | Button |
| Machine Profile | DropDown |
| Material | DropDown |
| Standard | DropDown |
| Validate | Button |
| Import | Button |
| Cancel | Button |
| Settings | Button |

---

# Step 1

Select TXT File

Ribbon Button

```
Select TXT
```

Action

Open Windows File Dialog

Filter

```
*.txt
```

After selection

↓

Filename displayed

↓

Import Summary updated

---

# Step 2

Machine Profile

Automatically detected.

If detection fails

↓

Operator selects

Example

Shimadzu

FATEK

Generic

---

# Step 3

Material

Automatically detected.

If multiple matches exist

↓

Ribbon DropDown

Displayed

Operator selects

Correct material.

---

# Step 4

Testing Standard

Automatically detected.

Examples

ISO 6892-1

ASTM E8

ISO 630

ISO 898

INSO 3132

Unknown

↓

Operator Selection

---

# Step 5

Validation

Ribbon Button

```
Validate
```

Checks

Header

Columns

Units

Dimensions

Material

Standard

Machine Profile

Area

Gauge Length

Result

PASS

WARNING

ERROR

---

# Step 6

Import

Ribbon Button

```
Import
```

Actions

Create Project

Create Import Session

Store Raw Data

Generate Engineering Data

Prepare Graph

Complete

---

# Step 7

Finish

Ribbon

Automatically Enables

Engineering

Graphs

Reports

Analysis

---

# Cancel

Ribbon Button

```
Cancel
```

Stops

Current Import

Performs

Rollback

Returns

IDLE

---

# Import Summary

Ribbon displays

Selected File

Machine

Material

Standard

Rows

Columns

Units

Status

---

# Progress

During import

Status Bar

Displays

Reading File

Parsing

Validation

Database

Engineering

Completed

---

# Warning Display

Ribbon

Yellow Notification

Examples

Unknown Material

Area Difference

Unknown Column

Import continues.

---

# Error Display

Ribbon

Red Notification

Import stopped.

Rollback executed.

---

# Ribbon Behaviour

State Driven

IDLE

↓

Import Enabled

READY

↓

Engineering Enabled

ERROR

↓

Retry Enabled

---

# Keyboard Shortcuts

Future

Ctrl+I

Import

Ctrl+R

Recalculate

Ctrl+G

Graph

Reserved

---

# Excel Compatibility

No UserForms

No ActiveX Controls

Ribbon XML

Standard VBA

Excel 2019 Compatible

---

# Future Enhancements

Task Pane

Drag & Drop TXT

Recent Files

Import History

Batch Import

Cloud Import

Reserved

---

# Acceptance Criteria

✔ Ribbon only

✔ No UserForms

✔ Excel 2019 compatible

✔ State-driven workflow

✔ SQLite integration

✔ Operator-friendly

✔ ISO 17025 compliant

---

End of Document
