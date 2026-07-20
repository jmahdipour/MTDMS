# TXT Validation Specification

Document ID : MTDMS-IMP-006

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Input

TXT Files Only

---

# Purpose

This document defines every validation rule applied before a TXT file is accepted.

Engineering calculations shall never begin until validation is completed successfully.

Validation shall comply with ISO 17025 traceability requirements.

---

# Validation Pipeline

TXT Selected

↓

Header Validation

↓

Encoding Validation

↓

Structure Validation

↓

Column Validation

↓

Unit Validation

↓

Data Validation

↓

Engineering Validation

↓

Project Validation

↓

Accepted

---

# Validation Levels

## Level 1

File Validation

Checks

• File Exists

• File Extension

• File Size

• File Read Permission

Failure

Import Aborted

---

## Level 2

Encoding Validation

Supported

UTF-8

ANSI

UTF-16

Failure

Encoding Error

---

## Level 3

Header Validation

Required Fields

Machine

Material

Area

Gauge Length

Standard

Force Unit

Length Unit

Date

Operator

Failure

Import Blocked

---

## Level 4

Column Validation

Required

Time

Force

Stroke

Optional

Extension

Stress

Strain

Failure

Missing Mandatory Column

Import Blocked

---

## Level 5

Unit Validation

Checks

Recognized Units

Consistent Units

Conversion Available

Failure

Unknown Unit

Import Blocked

---

## Level 6

Data Validation

Checks

Numeric Values

Finite Values

No NaN

No Infinity

No Empty Mandatory Cells

---

# Time Validation

Rules

Time

≥ 0

Monotonic Increasing

No Duplicate Samples

Failure

Time Error

---

# Force Validation

Rules

Numeric

Finite

No Missing Values

Negative values allowed only if machine profile permits.

---

# Stroke Validation

Rules

Numeric

Finite

Continuous

No Missing Values

---

# Extension Validation

If Available

Numeric

Finite

Continuous

If Missing

Calculated Later

---

# Engineering Validation

Checks

Area > 0

Gauge Length > 0

Material Exists

Standard Exists

Failure

Engineering Validation Error

---

# Material Validation

Material Name

↓

Search Material Library

↓

Found

↓

Load Engineering Properties

↓

Continue

Not Found

↓

Warning

↓

Operator Decision

---

# Standard Validation

Recognized Standards

ISO 6892-1

ISO 630

ISO 898

INSO 3132

ASTM

Unknown Standard

↓

Warning

↓

Continue only with operator confirmation

---

# Duplicate Detection

Checks

Duplicate Header

Duplicate Time

Duplicate Entire Row

Failure

Row Ignored

Logged

---

# Missing Data

Allowed

Optional Columns

Not Allowed

Mandatory Columns

---

# Blank Lines

Ignored

Automatically

---

# Corrupted Lines

Skipped

Logged

ERROR_LOG

Line Number

Reason

---

# Row Count Validation

Minimum

10 Rows

Maximum

500000 Rows

Failure

Import Blocked

---

# File Size Validation

Maximum

100 MB

Recommended

20 MB

---

# Statistical Validation

Checks

Force Range

Stroke Range

Time Range

Outlier Percentage

Unexpected Constant Values

---

# Engineering Plausibility

Examples

Young's Modulus

Must be positive

Yield Strength

Must be below UTS

UTS

Must exceed Yield

Fracture Point

Must exist

Failure

Engineering Warning

---

# Validation Result

Three possible states

VALID

Import Allowed

WARNING

Import Allowed

Operator Confirmation Required

INVALID

Import Blocked

---

# Validation Report

Generated Automatically

Contains

Header Status

Column Status

Unit Status

Data Status

Engineering Status

Warnings

Errors

---

# Logging

Every validation writes

Timestamp

Operator

TXT Name

Validation Result

Warning Count

Error Count

SQLite Log

---

# Performance

Header Validation

<100 ms

Column Validation

<100 ms

100000 Rows

Validation

<2 seconds

---

# Future Validation

Digital Signature

Checksum

Machine Certificate

Calibration Certificate

Cloud Verification

Reserved

---

# Acceptance Criteria

✔ TXT Structure Valid

✔ Header Complete

✔ Mandatory Columns Present

✔ Units Recognized

✔ Numeric Data Valid

✔ Engineering Data Valid

✔ Material Identified

✔ Standard Identified

✔ Validation Report Generated

---

End of Document
