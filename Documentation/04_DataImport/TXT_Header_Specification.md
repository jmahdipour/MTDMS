# TXT Header Specification

Document ID : MTDMS-IMP-003

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Input

TXT Files Only

---

# Purpose

This document defines the standard header format expected by MTDMS.

The Header contains all metadata required before engineering calculations begin.

Engineering calculations shall never start until the Header has been successfully validated.

---

# General Layout

```
Header

↓

Machine Information

↓

Project Information

↓

Specimen Information

↓

Material Information

↓

Test Configuration

↓

Data Table
```

---

# Header Requirements

Header must appear before the first numeric data row.

Blank lines are allowed.

Order is not mandatory.

Field names are case insensitive.

---

# Required Header Fields

Machine Name

Machine Model

Machine Serial Number

Operator

Test Date

Test Time

Material

Specimen ID

Cross Section Area

Original Gauge Length (L0)

Standard

Force Unit

Length Unit

---

# Optional Header Fields

Customer

Project Number

Heat Number

Batch Number

Drawing Number

Sample Description

Temperature

Humidity

Extensometer Type

Load Cell Capacity

Machine Software Version

Remarks

---

# Example Header

```
Machine = Shimadzu AG-25TB

Operator = J. Mahdipour

Material = ST37

Specimen = T-001

Area = 78.54

L0 = 50

Standard = ISO 6892-1

Force Unit = kN

Length Unit = mm

Date = 2026-07-20

Time = 09:45:13
```

---

# Required Engineering Fields

Material

Mandatory

Area

Mandatory

Gauge Length

Mandatory

Standard

Mandatory

Force Unit

Mandatory

Length Unit

Mandatory

---

# Material Recognition

Material name shall be matched against

Material Library

If found

↓

Load Engineering Properties

Young's Modulus

Yield Range

Expected UTS

Density

Poisson Ratio

---

# Standard Recognition

Recognized

ISO 6892-1

ISO 630

ISO 898

INSO 3132

ASTM

Future standards shall be loaded from Standard Library.

---

# Area

Area may be supplied

Directly

or

Calculated

Round Specimen

```
Area = π d² / 4
```

Flat Specimen

```
Area = Width × Thickness
```

---

# Specimen Geometry

Round

Diameter only

Flat

Width

Thickness

Pipe

Outside Diameter

Wall Thickness

Spring

Wire Diameter

Mean Diameter

Active Coils

---

# Date Format

Accepted

```
YYYY-MM-DD

DD/MM/YYYY

MM/DD/YYYY
```

Automatically normalized.

---

# Time Format

Accepted

```
HH:MM

HH:MM:SS
```

---

# Unit Detection

Force

kgf

N

kN

Length

mm

cm

m

Automatic conversion performed.

---

# Header Validation

Checks

Required Fields

Duplicate Fields

Unknown Fields

Invalid Units

Missing Material

Missing Area

Missing Gauge Length

---

# Unknown Fields

Unknown fields are

Stored

Logged

Ignored

Never deleted.

---

# Duplicate Fields

If duplicated

Last valid value is used.

Warning written to

ERROR_LOG

---

# Missing Fields

Critical

↓

Import Blocked

Optional

↓

Warning

↓

Continue

---

# Header Storage

Header information stored in

tblProject

SQLite

Project History

Report Metadata

---

# Engineering Lock

No calculation shall begin until

Header Status

=

VALID

---

# Future Fields

Machine Firmware

PLC Version

Calibration Certificate

Extensometer Serial

Load Cell ID

Reserved.

---

End of Document
