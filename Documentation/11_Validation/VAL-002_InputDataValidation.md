# Input Data Validation

Document ID : MTDMS-VAL-002

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Validation

Status

Production

---

# Purpose

The Input Data Validation module verifies that imported data is suitable for engineering calculations.

The objective is to prevent invalid, incomplete or physically impossible data from entering the Engineering Engine.

This module validates input data only.

It does not repair or modify imported data.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ISO 12135

ASTM E8/E8M

Applicable test standard

---

# Objectives

The module shall

• Verify mandatory fields

• Verify numeric values

• Verify engineering dimensions

• Verify measurement channels

• Detect corrupted datasets

• Prevent invalid calculations

---

# Validation Sequence

```
Imported File

↓

Header Validation

↓

Metadata Validation

↓

Channel Validation

↓

Measurement Validation

↓

Engineering Input Validation

↓

Ready
```

---

# Metadata Validation

Verify

Certificate Number

Sample ID

Material

Standard

Specimen Type

Operator

Import Date

Missing mandatory fields

↓

FAIL

---

# Geometry Validation

Verify

Area > 0

Gauge Length > 0

Diameter > 0

Width > 0

Thickness > 0

Dimensions shall be physically possible.

---

# Measurement Validation

Verify

Force Channel Exists

Time Channel Exists

Displacement Exists

No Empty Dataset

Minimum Measurement Count

Administrator configurable.

---

# Numeric Validation

Reject

NaN

Infinity

Text inside numeric column

Overflow

Unexpected symbols

---

# Engineering Limits

Verify

Force ≥ 0

Time ≥ 0

Area > 0

Gauge Length > 0

Negative displacement

Allowed

depending on test configuration.

---

# Time Validation

Verify

Monotonic increase

No duplicated timestamps

No missing sequence

---

# Channel Validation

Recognized channels

Force

Displacement

Extension

Time

Engineering Stress

Engineering Strain

Unknown channels

↓

Ignored

↓

Logged

---

# Unit Validation

Recognized units

N

kN

kgf

mm

MPa

s

Unknown units

↓

WARNING

---

# Sample Validation

Supported

Round

Flat

Pipe

Wire

Spring

Custom

Unsupported types

↓

Review Required

---

# Validation Results

PASS

PASS WITH WARNING

FAIL

REJECTED

---

# User Actions

PASS

↓

Continue

WARNING

↓

Operator Confirmation

FAIL

↓

Abort Engineering Calculation

---

# SQLite Database

Tables

```
tblInputValidation

tblInputValidationRule

tblInputValidationHistory
```

---

# Audit Trail

Record

Validation Rule

Input Value

Status

Timestamp

Operator

Computer Name

---

# Error Handling

Missing Force Channel

↓

FAIL

Area = 0

↓

FAIL

Invalid Number

↓

FAIL

Unknown Unit

↓

WARNING

---

# Future Enhancements

Automatic Geometry Recognition

AI Input Inspection

Standard-Specific Rules

Reserved

---

# Acceptance Criteria

✔ Mandatory field validation

✔ Numeric validation

✔ Geometry validation

✔ Channel validation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ No automatic data modification

---

End of Document
