# Ribbon Specification

Document ID : MTDMS-UI-003

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

VBA

---

# Purpose

This document defines the complete Ribbon architecture of MTDMS.

The Ribbon is the primary user interface.

No UserForms shall be used.

No worksheet tabs shall be used.

---

# Ribbon Name

MTDMS

---

# Ribbon Tabs

1. Home
2. Import
3. Calculation
4. Graph
5. Report
6. Database
7. Settings
8. Help

---

# HOME TAB

## Group

Project

Buttons

New Project

Open Project

Save

Save As

Close Project

---

## Group

Navigation

Buttons

Home

Import

Analysis

Graph

Report

---

## Group

Quick Access

Buttons

Recent Projects

Material Library

Standard Library

---

# IMPORT TAB

## Group

TXT

Buttons

Browse TXT

Preview TXT

Validate TXT

Import TXT

Reload TXT

---

## Group

Information

Buttons

TXT Properties

Machine Information

Encoding

---

## Group

Utilities

Buttons

Clear Import

Import Log

---

# CALCULATION TAB

## Group

Engineering

Buttons

Calculate

Recalculate

Correction

Validation

---

## Group

Mechanical Properties

Buttons

Young

Yield

UTS

Fracture

True Stress

True Strain

---

## Group

Material

Buttons

Select Material

Material Database

---

# GRAPH TAB

## Group

Navigation

Buttons

Previous Graph

Next Graph

---

## Group

Tools

Buttons

Zoom

Pan

Crosshair

Grid

Legend

---

## Group

Engineering

Buttons

Manual Yield

Manual Fracture

Correction

Reset

Undo

---

## Group

Export

Buttons

Export Image

Export Excel

Copy Graph

---

# REPORT TAB

## Group

Preview

Buttons

Preview

Summary

---

## Group

Output

Buttons

Print

PDF

Excel

---

## Group

Laboratory

Buttons

Certificate

Calibration

History

---

# DATABASE TAB

## Group

Project

Buttons

Project Database

History

Backup

Restore

---

## Group

Libraries

Buttons

Material Library

Standard Library

Machine Library

---

## Group

Maintenance

Buttons

Compact Database

Integrity Check

---

# SETTINGS TAB

## Group

Application

Buttons

General

Appearance

Language

Units

---

## Group

Engineering

Buttons

Calculation Settings

Graph Settings

TXT Settings

---

## Group

Administrator

Buttons

Protection

Users

Permissions

---

# HELP TAB

## Group

Documentation

Buttons

User Manual

Developer Manual

Standards

---

## Group

Support

Buttons

About

License

System Information

---

# Ribbon Rules

✓ Ribbon is always visible.

✓ Ribbon controls every visible worksheet.

✓ Ribbon never performs calculations directly.

✓ Ribbon only calls VBA procedures.

✓ Ribbon never writes directly to worksheets.

✓ Ribbon communicates only through Controller modules.

---

# Callback Architecture

Ribbon Button

↓

Ribbon Callback

↓

Controller

↓

Business Logic

↓

Worksheet

↓

Database

---

# Naming Convention

Buttons

btnXXXX

Groups

grpXXXX

Tabs

tabXXXX

Callbacks

OnActionXXXX

Images

imgXXXX

---

# Future Expansion

Compression

Impact

Hardness

Calibration

SPC

Dashboard

---

End of Document
