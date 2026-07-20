# Ribbon Architecture

Document ID : MTDMS-RBN-001

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

VBA

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines the complete Ribbon architecture.

Ribbon is the only user interface of MTDMS.

Users never work directly with worksheets.

---

# Architecture

Ribbon XML

↓

Ribbon Callback

↓

Ribbon Controller

↓

Business Controller

↓

Calculation Engine

↓

SQLite

↓

Worksheet Refresh

---

# Ribbon Design Rules

✔ Ribbon controls entire application

✔ Ribbon contains no engineering calculations

✔ Ribbon contains no SQL

✔ Ribbon contains no worksheet logic

✔ Ribbon calls Controllers only

---

# Ribbon Tabs

```
Home

Import

Calculation

Graph

Report

Database

Settings

Help
```

---

# Controller Layer

```
Ribbon

↓

RibbonController

↓

NavigationController

↓

ImportController

↓

CalculationController

↓

GraphController

↓

ReportController

↓

DatabaseController
```

---

# Callback Rules

Every Ribbon Button

↓

One Callback

↓

One Controller

↓

One Responsibility

---

# Forbidden

Ribbon

↓

Worksheet

Ribbon

↓

Database

Ribbon

↓

Engineering Formula

Ribbon

↓

Chart Object

---

# Ribbon Loading

Workbook_Open()

↓

Load XML

↓

Load Icons

↓

Initialize Ribbon

↓

Ready

---

# Ribbon Refresh

Used only when

Project Loaded

Material Changed

Standard Changed

Settings Changed

Language Changed

---

# Ribbon Visibility

Ribbon always visible.

Never minimized automatically.

---

# Security

Ribbon cannot modify

Hidden Worksheets

SQLite

Engineering Tables

Without Controller authorization.

---

# Future

Compression Module

Impact Module

Fatigue Module

Calibration Module

SPC Module

---

End of Document
