# TXT File Format Specification

Document ID : MTDMS-IMP-001

Version : 0.1.0

Platform

Microsoft Excel 2019

Input Format

TXT Only

---

# Purpose

This document defines the ONLY supported input format.

MTDMS imports machine generated TXT files.

No other file format shall be accepted.

---

# Supported File Types

✔ TXT

Unsupported

CSV

XLS

XLSX

XML

JSON

Binary

Database

---

# Encoding

Preferred

UTF-8

Supported

ANSI

UTF-16

Automatic detection required.

---

# Line Separator

Supported

CRLF

LF

---

# Decimal Separator

Supported

.

or

,

Automatically detected.

---

# Header Section

Header contains machine information.

Example

Machine

Operator

Date

Material

Specimen

Area

Gauge Length

Machine Capacity

Standard

---

# Data Section

Columns

Time

Stroke

Extension

Force

Optional

Stress

Strain

---

# Mandatory Columns

Time

Force

Stroke

---

# Optional Columns

Extension

Stress

Strain

Temperature

Cycle

Channel

---

# Time Unit

Seconds

---

# Force Unit

Automatically detected

kgf

N

kN

---

# Stroke Unit

mm

---

# Extension Unit

mm

---

# Stress Unit

MPa

Calculated if absent.

---

# Strain Unit

mm/mm

Calculated if absent.

---

# Example

Time

Stroke

Extension

Force

0.00

0.000

0.000

0

0.05

0.003

0.001

45

0.10

0.006

0.002

90

...

---

# Import Rules

Header

↓

Read

↓

Validate

↓

Detect Units

↓

Detect Columns

↓

Read Data

↓

Validation

↓

Store

tblRawData

---

# Missing Columns

Extension

↓

Calculate

Stress

↓

Calculate

Strain

↓

Calculate

---

# Invalid Data

Ignored

Blank Lines

Ignored

Repeated Header

Ignored

Non Numeric Data

Logged

Corrupted Lines

Skipped

---

# Maximum File Size

Recommended

20 MB

Maximum

100 MB

---

# Maximum Rows

Recommended

100000

Future

500000

---

# Import Result

Raw Data

↓

tblRawData

Engineering

↓

ENGINEERING

Results

↓

RESULT

Graphs

↓

GRAPH

Reports

↓

REPORT

---

# Import Restrictions

TXT is read-only.

Original file is never modified.

---

# Import Verification

Checksum

Optional

Header Validation

Required

Column Validation

Required

Unit Detection

Required

---

# Future Support

Shimadzu

Universal Testing Machines

Compression Machines

Impact Machines

Spring Test Machines

Ring Stiffness Machines

---

End of Document
