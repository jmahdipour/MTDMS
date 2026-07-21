# File Validation

Document ID : MTDMS-DAT-002

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Data Management

Status

Production

---

# Purpose

The File Validation module verifies that every imported machine output file is complete, readable and internally consistent before engineering calculations begin.

No engineering calculations shall start until validation has successfully completed.

The validation module operates only on exported files.

It has no communication with the testing machine.

---

# Objectives

The module shall

• Verify file structure

• Verify file integrity

• Verify metadata

• Verify engineering data format

• Detect corruption

• Detect incomplete files

• Detect duplicated files

---

# Validation Workflow

```
Select File

↓

Read Header

↓

Validate Header

↓

Read Data

↓

Validate Structure

↓

Validate Values

↓

Checksum Verification

↓

Validation Result
```

---

# Validation Levels

Level 1

File Exists

↓

Level 2

Extension

↓

Level 3

Header

↓

Level 4

Data Format

↓

Level 5

Engineering Consistency

↓

PASS

or

FAIL

---

# Supported File Types

TXT

CSV

DAT

Administrator configurable.

---

# Header Validation

Verify

Machine Identifier

Software Version

Export Date

Export Time

Specimen Information

Material Information

Data Columns

Units

Missing mandatory fields

↓

Validation Failure

---

# Data Validation

Verify

Column Count

Numeric Format

Missing Values

Duplicate Rows

Invalid Characters

Unexpected Delimiters

---

# Engineering Value Validation

Verify

Force values

Displacement values

Extension values

Time values

Gauge Length

Area

Dimensions

Negative values are allowed only where physically meaningful.

---

# Unit Validation

Supported Units

Force

N

kN

kgf

Stress

MPa

Length

mm

Time

s

Unknown units

↓

Validation Warning

---

# Sequence Validation

Verify

Time is monotonic

Sample order is correct

No duplicated record index

No unexpected gaps

---

# File Completeness

The file shall contain

Header

Measurement Data

End of File

If measurement data is missing

↓

Reject

---

# Duplicate Detection

Based on

SHA-256

File Size

Creation Time

Original File Name

Administrator configurable.

---

# Validation Result

PASS

PASS with Warning

FAIL

Critical FAIL

---

# Warning Examples

Unknown Material

Unknown Standard

Unused Columns

Missing Optional Field

Old Software Version

---

# Failure Examples

Missing Header

Corrupted Data

Invalid Delimiter

Non-numeric Engineering Data

Unexpected File Format

Checksum Failure

---

# SQLite Database

Tables

```
tblValidation

tblValidationHistory

tblValidationRule
```

---

# Audit Trail

Each validation stores

Validation ID

Operator

Timestamp

File ID

Validation Result

Rule Violated

Computer Name

---

# Error Handling

Unreadable File

↓

Abort

Invalid Header

↓

Reject

Corrupted Data

↓

Reject

Database Error

↓

Abort

---

# Future Enhancements

Automatic Standard Recognition

Automatic Material Recognition

AI Validation

Statistical File Health Analysis

Reserved

---

# Acceptance Criteria

✔ Header validation

✔ Data validation

✔ Engineering consistency validation

✔ Duplicate detection

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No machine communication

✔ ISO/IEC 17025 compliant

---

End of Document
