# TXT Parsing Engine

Document ID : MTDMS-CE-002

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Input

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The TXT Parsing Engine reads the original machine-generated TXT file and converts it into structured engineering data.

The parser performs **no engineering calculations**.

Its only responsibility is to correctly interpret the TXT file.

---

# Objectives

The TXT Parsing Engine shall

• Read TXT files

• Detect file format

• Parse metadata

• Parse measured data

• Detect invalid records

• Produce structured datasets

---

# Engineering Philosophy

TXT File

↓

Parser

↓

Structured Data

↓

Engineering Calculation

The parser never modifies

the original TXT file.

---

# Input File

Machine exported TXT file

Supported

UTF-8

ANSI

Windows-1252

Administrator configurable.

---

# Parser Workflow

```
Open TXT

↓

Verify File

↓

Detect Encoding

↓

Read Header

↓

Read Metadata

↓

Read Measurement Data

↓

Validate Structure

↓

Generate Internal Dataset

↓

Pass Dataset to Calculation Engine
```

---

# TXT Structure

The parser shall recognize two logical sections.

## Section 1 — Metadata

Examples

Machine Name

Operator

Date

Time

Sample ID

Material

Standard

Diameter

Width

Thickness

Gauge Length

Cross Section

Load Cell

Extensometer

Units

---

## Section 2 — Measurement Data

Typical columns

Time

Force

Displacement

Extension

Strain

Stress

Other machine-dependent values

The parser shall identify columns by their headers rather than fixed positions whenever possible.

---

# Internal Dataset

After parsing, data shall be stored internally as:

- Metadata object
- Measurement table
- Column definition table
- Unit definition table
- File information

No calculations are performed at this stage.

---

# Supported Units

Typical imported units

Force

N

kN

kgf

---

Length

mm

cm

m

---

Stress

MPa

---

Strain

%

mm/mm

Units are preserved exactly as imported.

Conversion is performed later.

---

# Column Recognition

The parser shall recognize standard engineering column names.

Examples

Force

Load

Displacement

Crosshead

Extension

Elongation

Time

Stress

Strain

Machine-specific aliases may be configured.

---

# Missing Columns

If optional columns are missing

↓

Continue

If mandatory columns are missing

↓

Abort Import

---

# Invalid Records

Invalid numeric values

↓

Ignored

Logged

Missing records

↓

Logged

Unexpected text

↓

Logged

File continues

when possible.

---

# File Integrity

Before parsing

the engine shall verify

File Exists

Readable

Non-empty

Valid Encoding

Valid Structure

Checksum

---

# Duplicate Detection

SHA256

File Size

File Name

Import Date

are passed to

Import History

for duplicate verification.

---

# Engineering Independence

The parser

never

calculates

Stress

Strain

Young's Modulus

Yield Strength

Ultimate Strength

Any engineering value.

---

# SQLite Interaction

The parser

does not

write directly

to SQLite.

Only

Import History

receives

file metadata.

---

# Error Handling

File Missing

↓

Abort

Encoding Error

↓

Abort

Unreadable File

↓

Abort

Missing Metadata

↓

Warning

Missing Data Table

↓

Abort

---

# Performance Targets

Open File

< 100 ms

Metadata Parsing

< 100 ms

Measurement Parsing

Depends on file size

Typical tensile test

< 500 ms

---

# Acceptance Criteria

✔ TXT interpreted correctly

✔ Metadata extracted

✔ Measurement table extracted

✔ Original TXT unchanged

✔ SQLite not modified directly

✔ Excel 2019 compatible

✔ SQLite compatible

✔ ISO/IEC 17025 compliant

---

End of Document
