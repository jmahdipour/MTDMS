# TXT Warning Handling Specification

Document ID : MTDMS-IMP-036

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

This document defines how non-critical import warnings shall be handled.

Unlike errors, warnings do not stop the import process.

They notify the operator that imported data requires attention.

Warnings shall always be recorded in the Audit Trail.

---

# Philosophy

TXT

↓

Import

↓

Warning Detection

↓

Operator Notification

↓

Continue Import

↓

Audit Trail

---

# Warning Levels

## Level 1

Information

Color

Blue

Import

Continues

No operator action required.

---

## Level 2

Recommendation

Color

Green

Operator

May review.

Import continues.

---

## Level 3

Attention

Color

Yellow

Operator

Should verify.

Import continues.

---

## Level 4

Serious Warning

Color

Orange

Operator confirmation recommended.

Import continues.

---

# Typical Warnings

Material Alias Used

Standard Alias Used

Area Difference

Young's Modulus Estimated

Unknown Temperature

Large TXT File

Duplicate Sample Removed

Blank Rows Ignored

Unused Columns Found

Header Field Ignored

Automatic Unit Conversion Applied

Unknown Optional Column

Graph Correction Suggested

---

# Material Warnings

Example

```
Material

ST37

Matched

S235JR
```

Warning

```
Material Alias Applied
```

Import

Continues

---

# Standard Warning

Example

```
ISO6892

↓

ISO 6892-1
```

Warning

Alias used.

---

# Area Difference

Imported Area

↓

Calculated Area

Difference

>1%

↓

Warning

Operator should verify.

---

# Large File Warning

Rows

>100000

↓

Display

Large file detected.

Import continues.

---

# Unknown Optional Columns

Example

```
Channel5

Humidity

Operator Notes
```

Ignored.

Warning stored.

---

# Unit Conversion Warning

Example

```
kgf

↓

N
```

Import continues.

Conversion logged.

---

# Blank Row Warning

Blank rows

Removed

Count stored.

---

# Duplicate Sample Warning

Duplicate rows

Ignored

Count logged.

---

# Graph Warning

Engineering data valid

↓

Elastic region uncertain

↓

Recommend

Manual Yield Verification

---

# Warning Dialog

Displays

Warning Code

Description

Recommendation

Buttons

Continue

Details

Hide

---

# SQLite Table

```
tblWarnings
```

Fields

WarningID

ProjectID

SessionID

WarningCode

Description

Operator

Timestamp

Resolved

---

# Warning Codes

WRN-0001

Material Alias

WRN-0002

Standard Alias

WRN-0003

Area Difference

WRN-0004

Large File

WRN-0005

Blank Rows

WRN-0006

Duplicate Rows

WRN-0007

Unknown Optional Column

WRN-0008

Automatic Unit Conversion

WRN-0009

Graph Correction Recommended

WRN-0010

Engineering Review Recommended

---

# Operator Actions

Operator may

Ignore

Review

Resolve

Every action logged.

---

# Report

Warnings appear in

Import Summary

Audit Report

Project History

They do not appear on the final mechanical test certificate unless configured.

---

# Future Warnings

AI Confidence Low

Machine Drift

Calibration Expired

Material Outlier

Reserved

---

# Acceptance Criteria

✔ Import never stops because of warnings

✔ Every warning logged

✔ Operator informed

✔ SQLite compatible

✔ ISO 17025 traceability maintained

✔ Warning history searchable

---

End of Document
