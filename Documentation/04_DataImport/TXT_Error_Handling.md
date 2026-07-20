# TXT Error Handling Specification

Document ID : MTDMS-IMP-035

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Database

SQLite

---

# Purpose

This document defines the complete error handling architecture for TXT import.

Every error shall be:

- Detected
- Classified
- Logged
- Presented clearly to the operator
- Recoverable whenever possible

The application shall never crash because of an invalid TXT file.

---

# Design Philosophy

```
TXT

↓

Parser

↓

Validation

↓

Error Detection

↓

Recovery

↓

Continue
```

Fatal errors stop only the current import.

They shall never corrupt:

- Workbook
- SQLite Database
- Project
- Existing Reports

---

# Error Categories

## 1 File Errors

Examples

File not found

Access denied

File locked

Unsupported extension

Empty file

---

## 2 Header Errors

Examples

Missing Material

Missing Standard

Missing Area

Missing Gauge Length

Unknown Machine

Invalid Header Format

---

## 3 Column Errors

Examples

Force column missing

Stroke column missing

Time column missing

Duplicate columns

Invalid column names

---

## 4 Unit Errors

Examples

Unknown force unit

Unknown length unit

Mixed unit system

Unsupported temperature unit

---

## 5 Data Errors

Examples

Negative force

Negative dimensions

NaN

Overflow

Duplicate samples

Missing values

Non-numeric values

---

## 6 Geometry Errors

Examples

Negative diameter

Pipe thickness larger than radius

Width = 0

Area mismatch

---

## 7 Database Errors

Examples

SQLite unavailable

Transaction failure

Duplicate key

Database locked

---

## 8 Engineering Errors

Examples

Young's modulus unavailable

Material not found

Standard profile missing

Yield calculation impossible

---

# Error Severity

## Information

Blue

Import continues.

---

## Warning

Yellow

Operator notified.

Import continues.

---

## Recoverable Error

Orange

Operator chooses

Retry

Ignore

Cancel

---

## Critical Error

Red

Import stops immediately.

Rollback executed.

---

# Error Code Structure

```
IMP-XXXX
```

Example

```
IMP-0001

File Not Found
```

```
IMP-0102

Header Missing
```

```
IMP-0203

Column Missing
```

```
IMP-0304

Invalid Unit
```

```
IMP-0405

Engineering Failure
```

---

# File Error Codes

| Code | Description |
|--------|-------------|
| IMP-0001 | File Not Found |
| IMP-0002 | File Locked |
| IMP-0003 | Access Denied |
| IMP-0004 | Empty File |
| IMP-0005 | Unsupported Extension |

---

# Header Error Codes

| Code | Description |
|--------|-------------|
| IMP-0101 | Missing Machine |
| IMP-0102 | Missing Material |
| IMP-0103 | Missing Area |
| IMP-0104 | Missing L0 |
| IMP-0105 | Missing Standard |

---

# Column Error Codes

| Code | Description |
|--------|-------------|
| IMP-0201 | Missing Time |
| IMP-0202 | Missing Force |
| IMP-0203 | Missing Stroke |
| IMP-0204 | Duplicate Columns |

---

# Unit Error Codes

| Code | Description |
|--------|-------------|
| IMP-0301 | Unknown Force Unit |
| IMP-0302 | Unknown Length Unit |
| IMP-0303 | Unknown Stress Unit |

---

# Geometry Error Codes

| Code | Description |
|--------|-------------|
| IMP-0401 | Invalid Diameter |
| IMP-0402 | Invalid Thickness |
| IMP-0403 | Invalid Area |

---

# Database Error Codes

| Code | Description |
|--------|-------------|
| IMP-0501 | SQLite Locked |
| IMP-0502 | Transaction Failed |
| IMP-0503 | Database Corrupted |

---

# Engineering Error Codes

| Code | Description |
|--------|-------------|
| IMP-0601 | Material Missing |
| IMP-0602 | Standard Missing |
| IMP-0603 | Calculation Failed |

---

# Error Dialog

Displays

Error Code

Description

Possible Cause

Suggested Action

Buttons

Retry

Ignore

Cancel

Help

---

# Recovery Strategy

Recoverable

↓

Retry

↓

Continue

Critical

↓

Rollback

↓

Abort Import

↓

Keep Project Safe

---

# Rollback

Rollback removes

Temporary Arrays

Temporary SQLite Records

Temporary Graph Data

Temporary Engineering Data

Raw imported projects remain unchanged.

---

# Logging

Every error stores

Timestamp

Operator

Project

Session

Module

Error Code

Description

Recovery Action

---

# Error Statistics

Future dashboard

Top Errors

Import Failure Rate

Recovery Success Rate

Machine Reliability

Reserved

---

# Acceptance Criteria

✔ Every error has unique code

✔ Every error logged

✔ Rollback supported

✔ Workbook never crashes

✔ SQLite integrity maintained

✔ Operator receives clear instructions

✔ Fully compatible with ISO 17025

---

End of Document
