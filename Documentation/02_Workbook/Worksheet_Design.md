# Worksheet Design Specification

Document ID : MTDMS-WB-003

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

---

# Purpose

This document defines the physical design of every worksheet inside MTDMS.

It specifies

- Layout
- Controls
- Tables
- Named Ranges
- Protection
- Interaction

No VBA implementation is described here.

---

# HOME

Purpose

Application Dashboard

Layout

--------------------------------------------------------

Header

--------------------------------------------------------

Project Information

Quick Actions

System Status

--------------------------------------------------------

Recent Projects

--------------------------------------------------------

Material Summary

Standard Summary

Machine Status

--------------------------------------------------------

Footer

--------------------------------------------------------

Objects

Table_RecentProjects

Panel_Project

Panel_System

Panel_Material

Panel_Standard

Buttons

Import TXT

Open Project

Save Project

Settings

Help

---

# IMPORT

Purpose

TXT Import

Layout

--------------------------------------------------------

Header

--------------------------------------------------------

TXT Information

--------------------------------------------------------

TXT Preview

--------------------------------------------------------

Validation

--------------------------------------------------------

Import

--------------------------------------------------------

Objects

Table_TXTPreview

Table_Validation

Buttons

Browse

Preview

Validate

Import

Clear

Reload

---

# ANALYSIS

Purpose

Engineering Workspace

Layout

--------------------------------------------------------

Header

--------------------------------------------------------

Specimen Information

--------------------------------------------------------

Mechanical Properties

--------------------------------------------------------

Engineering Result Table

--------------------------------------------------------

Graph Preview

--------------------------------------------------------

Objects

Table_Result

Table_Specimen

Chart_Preview

Buttons

Calculate

Correction

Update

---

# GRAPH

Purpose

Interactive Graph

Layout

--------------------------------------------------------

Header

--------------------------------------------------------

Graph

--------------------------------------------------------

Graph Toolbar

--------------------------------------------------------

Cursor Information

--------------------------------------------------------

Engineering Result

--------------------------------------------------------

Objects

Chart_StressStrain

Chart_ForceStroke

Table_Cursor

Buttons

Zoom

Pan

Crosshair

Yield

Fracture

Undo

Reset

Export

---

# REPORT

Purpose

Report Preview

Layout

--------------------------------------------------------

Header

--------------------------------------------------------

Company Logo

Laboratory Information

--------------------------------------------------------

Mechanical Result Table

--------------------------------------------------------

Stress-Strain Graph

--------------------------------------------------------

Signatures

--------------------------------------------------------

Buttons

Preview

PDF

Print

Excel

---

# RAW_DATA

Purpose

Imported TXT

No formatting.

Only Excel Table.

Objects

Table_RawData

Columns generated automatically.

---

# ENGINEERING

Purpose

Calculation Engine

Contains

Stress

Strain

Correction

Regression

Elastic Region

Yield

UTS

Fracture

No user interaction.

---

# RESULT

Purpose

Validated Results

Contains

Only final engineering values.

Referenced by

GRAPH

REPORT

SQLite

---

# MATERIAL_DB

Purpose

Material Library

Table

Table_Material

Columns

Material

Young

Yield

UTS

Density

Poisson

Reference

---

# STANDARD_DB

Purpose

Standard Library

Table

Table_Standard

Columns

Standard

Method

Calculation

Tolerance

Reference

---

# SETTINGS

Purpose

Application Configuration

Sections

General

Units

Graph

Ribbon

TXT

Database

Report

---

# HISTORY

Purpose

Project History

Table

Table_History

---

# ERROR_LOG

Purpose

Runtime Errors

Table

Table_Error

Columns

Time

Module

Procedure

Error

Severity

---

# SYSTEM

Purpose

Internal Variables

Not visible to user.

---

# Common Header

Every visible worksheet contains

Project

Material

Standard

Operator

Machine

Specimen

Date

Status

Workbook Version

---

# Common Footer

Displays

SQLite Status

TXT Status

Calculation Status

Application Version

---

# Protection Rules

Visible Worksheets

Protected

Unlocked Cells

Input Only

Hidden Worksheets

VeryHidden

Workbook Structure

Locked

---

# Worksheet Naming Convention

Visible

HOME

IMPORT

ANALYSIS

GRAPH

REPORT

Hidden

RAW_DATA

ENGINEERING

RESULT

MATERIAL_DB

STANDARD_DB

SETTINGS

HISTORY

ERROR_LOG

SYSTEM

Worksheet names shall never change.

---

End of Document
