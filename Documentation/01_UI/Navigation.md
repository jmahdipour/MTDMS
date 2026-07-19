# Navigation Specification

Document ID : MTDMS-UI-002

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

VBA

---

# Purpose

This document defines the navigation system of MTDMS.

Navigation shall be performed exclusively through the Ribbon.

Users shall never navigate using worksheet tabs.

---

# Navigation Philosophy

Workbook behaves as an application.

Worksheets are application pages.

Ribbon is the application menu.

---

# Main Workflow

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

---

# Ribbon Navigation

## HOME

Purpose

Main Dashboard

Buttons

Import TXT

Recent Projects

Material Library

Settings

Help

---

## IMPORT

Purpose

TXT Import

Buttons

Browse

Preview

Validate

Import

Back

---

## ANALYSIS

Purpose

Engineering Calculation

Buttons

Calculate

Correction

Next

Back

---

## GRAPH

Purpose

Interactive Engineering Graph

Buttons

Zoom

Pan

Yield

Fracture

Undo

Reset

Export

Back

---

## REPORT

Purpose

Report Preview

Buttons

Preview

PDF

Print

Excel

Back

---

# Hidden Worksheets

Users shall never navigate directly to

RAW_DATA

ENGINEERING

RESULT

SYSTEM

SETTINGS

ERROR_LOG

HISTORY

MATERIAL_DB

STANDARD_DB

---

# Allowed Navigation

HOME

↓

IMPORT

↓

ANALYSIS

↓

GRAPH

↓

REPORT

Only Ribbon may change worksheet.

---

# Disabled Navigation

Sheet Tabs

Ctrl + PageUp

Ctrl + PageDown

Direct Worksheet Selection

Formula Hyperlinks

---

# Navigation Controller

Every Ribbon button calls

NavigationController

↓

OpenWorksheet()

↓

Initialize Page

↓

Refresh Header

↓

Refresh Status

---

# Initial Page

When Workbook opens

HOME

shall always be displayed.

---

# Close Workbook

If project modified

Ask

Save

Don't Save

Cancel

---

# Future

Navigation History

Recent Pages

Favorites

Search
