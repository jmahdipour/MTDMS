# TXT Import Sequence

Document ID : MTDMS-IMP-012

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines the exact execution sequence of the TXT import process.

Every imported file shall pass through the same deterministic pipeline.

No engineering calculation shall begin before the parser finishes successfully.

---

# Overall Sequence

```
Open Workbook

↓

Create/Open Project

↓

Select TXT

↓

Read TXT

↓

Validate Header

↓

Detect Columns

↓

Detect Units

↓

Validate Data

↓

Normalize Data

↓

Store Raw Data

↓

Initialize Engineering

↓

Ready
```

---

# Detailed Sequence

## Step 1

User clicks

```
Browse TXT
```

Ribbon Controller

↓

Import Controller

↓

TXT Parser

---

## Step 2

Open File Dialog

Allowed

```
*.TXT
```

Rejected

Everything else

---

## Step 3

Check

File Exists

↓

Readable

↓

Extension

↓

Encoding

---

## Step 4

Read Entire File

```
TXT

↓

Variant()

↓

String()
```

No worksheet access.

---

## Step 5

Split

Header

↓

Data

↓

Footer

---

## Step 6

Header Validation

Checks

Machine

Material

Area

L0

Units

Standard

Operator

---

## Step 7

Column Recognition

Recognize

Time

Force

Stroke

Extension

Stress

Strain

Temperature

---

## Step 8

Unit Recognition

Force

↓

Length

↓

Stress

↓

Time

↓

Temperature

---

## Step 9

Normalize

Decimal Separator

↓

Units

↓

Column Names

↓

Internal Format

---

## Step 10

Validate Dataset

Rows

Columns

Numeric Values

Missing Values

Duplicate Rows

Monotonic Time

---

## Step 11

Create

Raw Data Objects

```
RawRecord

↓

Collection

↓

tblRawData
```

---

## Step 12

Store Metadata

Project

Machine

Operator

Material

Standard

TXT Name

Checksum

Import Time

---

## Step 13

Generate Import Summary

Contains

Rows

Warnings

Errors

Import Duration

Status

---

## Step 14

Notify Engineering Engine

```
Import Finished

↓

EngineeringController.Initialize()
```

Parser work ends here.

---

# Sequence Diagram

```
Operator

↓

Ribbon

↓

ImportController

↓

TXTParser

↓

Validator

↓

Normalizer

↓

RawDataStore

↓

SQLite

↓

EngineeringController
```

---

# Error Sequence

If

Header Error

↓

Abort

↓

Log

↓

Display Error

↓

Return

---

If

Unit Error

↓

Abort

↓

Log

↓

Return

---

If

Data Error

↓

Skip Row

↓

Continue

↓

Log Warning

---

# Success Sequence

```
TXT Imported

↓

Validation Passed

↓

Raw Data Stored

↓

SQLite Updated

↓

Ribbon Refreshed

↓

Calculation Enabled
```

---

# State Transition

```
STATE_PROJECT

↓

STATE_TXT_SELECTED

↓

STATE_TXT_IMPORTED

↓

STATE_TXT_VALID

↓

STATE_CALCULATION_READY
```

---

# Logging Sequence

Import Start

↓

Header

↓

Validation

↓

Storage

↓

SQLite

↓

Import End

---

# Performance Targets

File Open

<100 ms

Header

<50 ms

Validation

<2 sec

Import

<5 sec

SQLite

<300 ms

---

# Design Rules

✔ Sequential execution only

✔ No skipped validation

✔ No worksheet dependency

✔ No engineering calculations inside parser

✔ Parser always returns ImportResult

✔ Every stage logged

---

End of Document
