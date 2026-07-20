# Ribbon Groups Specification

Document ID : MTDMS-RBN-007

Version : 0.1.0

Platform

Microsoft Excel 2019

Ribbon XML

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines every Ribbon Group.

Groups organize commands according to engineering workflow.

Users should complete work from left to right.

---

# Ribbon Workflow

```
HOME

↓

IMPORT

↓

CALCULATION

↓

GRAPH

↓

REPORT

↓

DATABASE

↓

SETTINGS
```

---

# HOME TAB

## Group

Project

Purpose

Project Management

Contains

New Project

Open

Save

Save As

Close

---

## Group

Navigation

Purpose

Application Navigation

Contains

Home

Import

Analysis

Graph

Report

---

## Group

Libraries

Purpose

Engineering Databases

Contains

Material Library

Standard Library

---

## Group

Application

Purpose

General Application

Contains

Settings

Help

About

---

# IMPORT TAB

## Group

TXT

Purpose

TXT Operations

Contains

Browse

Preview

Import

Reload

Clear

---

## Group

Validation

Purpose

Input Verification

Contains

Validate TXT

Show Errors

Validation Report

---

## Group

Utilities

Purpose

Import Tools

Contains

Encoding

TXT Information

Machine Information

---

# CALCULATION TAB

## Group

Engineering

Purpose

Main Engineering Calculations

Contains

Calculate

Recalculate

Correction

Verification

---

## Group

Mechanical Properties

Purpose

Mechanical Results

Contains

Young

Yield

UTS

Fracture

True Stress

True Strain

---

## Group

Material

Purpose

Material Information

Contains

Material Library

Select Material

Reload Material

---

# GRAPH TAB

## Group

View

Purpose

Graph Navigation

Contains

Zoom

Pan

Crosshair

Grid

---

## Group

Engineering

Purpose

Engineering Markers

Contains

Manual Yield

Manual Fracture

Undo

Reset

---

## Group

Export

Purpose

Graph Export

Contains

Export Image

Export Excel

Copy Graph

---

# REPORT TAB

## Group

Preview

Purpose

Report Review

Contains

Preview

Refresh

---

## Group

Output

Purpose

Export

Contains

Print

PDF

Excel

---

## Group

Certificate

Purpose

Quality Documentation

Contains

Certificate

Summary

Approval

---

# DATABASE TAB

## Group

Projects

Purpose

Project Database

Contains

Projects

History

Search

---

## Group

Libraries

Purpose

Engineering Libraries

Contains

Material Library

Standard Library

---

## Group

Maintenance

Purpose

Database Maintenance

Contains

Backup

Restore

Compact

---

# SETTINGS TAB

## Group

General

Purpose

Application Settings

Contains

General

Theme

Language

Units

---

## Group

Engineering

Purpose

Engineering Preferences

Contains

Graph

TXT

Calculation

---

## Group

Security

Purpose

Protection

Contains

Users

Permissions

Workbook Protection

---

# HELP TAB

## Group

Documentation

Purpose

Documentation

Contains

User Manual

Developer Manual

---

## Group

Support

Purpose

Support

Contains

About

License

System Information

---

# Administrator Groups

Visible only in Administrator Mode

Maintenance

Calibration

Developer

Diagnostics

Database Repair

---

# Group Order

Groups shall always remain in the defined order.

Changing order is prohibited.

---

# Group Visibility

Project

Always

Navigation

Always

TXT

Project Loaded

Engineering

TXT Imported

Graph

Calculation Finished

Output

Report Ready

Database

SQLite Connected

---

# Future Groups

Compression

Impact

Fatigue

Hardness

Calibration

SPC

Cloud

Reserved.

---

# Design Rules

✔ Groups shall contain related commands only.

✔ Groups shall be arranged according to engineering workflow.

✔ Groups shall never exceed 8 controls.

✔ Large groups shall be divided into multiple groups.

✔ Group captions shall remain short and descriptive.

---

End of Document
