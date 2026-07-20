# Workbook Protection Specification

Document ID : MTDMS-WB-006

Version : 0.1.0

Platform

Microsoft Excel 2019

Workbook

WorkbookTemplate.xlsm

Programming Language

VBA

---

# Purpose

This document defines the protection strategy of WorkbookTemplate.xlsm.

The goal is

• Prevent accidental modification

• Protect engineering calculations

• Protect application structure

• Protect database information

• Allow only authorized user input

---

# Protection Philosophy

Users shall interact only with

Visible Worksheets

Ribbon

Input Cells

Everything else shall remain protected.

---

# Protection Levels

Level 1

Workbook

Level 2

Worksheet

Level 3

Objects

Level 4

Named Ranges

Level 5

VBA Project

---

# Workbook Protection

Workbook Structure

Locked

Workbook Windows

Unlocked

Workbook Encryption

Optional

Workbook Password

Administrator

---

# Worksheet Protection

## HOME

Protected

Unlocked Cells

Buttons only

---

## IMPORT

Protected

Unlocked

TXT Selection

Browse Button

Import Button

---

## ANALYSIS

Protected

Unlocked

Specimen Dimensions

Material Selection

Manual Inputs

---

## GRAPH

Protected

Unlocked

Graph Interaction

Zoom

Pan

Crosshair

Manual Yield

Manual Fracture

---

## REPORT

Protected

Unlocked

Report Notes

Approval Information

---

# Hidden Worksheets

RAW_DATA

VeryHidden

Protected

---

ENGINEERING

VeryHidden

Protected

---

RESULT

VeryHidden

Protected

---

MATERIAL_DB

VeryHidden

Protected

---

STANDARD_DB

VeryHidden

Protected

---

SETTINGS

VeryHidden

Protected

---

SYSTEM

VeryHidden

Protected

---

ERROR_LOG

VeryHidden

Protected

---

HISTORY

VeryHidden

Protected

---

# Cell Protection

Locked Cells

Engineering Formulas

Named Ranges

Headers

System Variables

Workbook Information

---

Unlocked Cells

Project Name

Operator

Customer

Material

Specimen Dimensions

Secondary Inputs

Manual Yield

Manual Fracture

Report Notes

---

# VBA Project

Protection

Enabled

View Source

Disabled

Password

Administrator Only

---

# Ribbon Protection

Ribbon is always enabled.

Ribbon cannot be customized by operator.

Ribbon XML is protected.

---

# Database Protection

SQLite File

Read/Write

Application Only

Direct User Editing

Not Allowed

---

# Import Protection

TXT

Read Only

Original TXT shall never be modified.

Imported TXT shall remain unchanged inside

tblRawData

---

# Formula Protection

Engineering formulas shall never exist inside visible worksheets.

All engineering calculations occur inside

ENGINEERING

worksheet.

Visible sheets display values only.

---

# Object Protection

Charts

Locked

Shapes

Locked

Images

Locked

Headers

Locked

Logos

Locked

---

# Error Recovery

If worksheet protection is accidentally removed

Application shall

Warn User

Restore Protection

Write Error Log

---

# Backup

Workbook

Automatic Backup

Project

Automatic Backup

SQLite

Automatic Backup

---

# Administrator Mode

Administrator may

Unlock Workbook

Modify Material Library

Modify Standard Library

Modify Settings

Update Workbook Version

Normal users cannot.

---

# Security Rules

✔ Workbook Structure Locked

✔ Hidden Sheets VeryHidden

✔ VBA Protected

✔ SQLite Protected

✔ Ribbon Controlled

✔ TXT Read Only

✔ Engineering Locked

✔ Input Cells Only Editable

---

# Future

Digital Signature

Certificate Protection

Multi-user Permissions

Windows Authentication

---

End of Document
