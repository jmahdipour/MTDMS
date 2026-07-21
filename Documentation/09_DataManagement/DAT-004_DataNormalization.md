# Data Normalization

Document ID : MTDMS-DAT-004

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

The Data Normalization module converts parsed raw measurement data into a standardized internal representation before engineering calculations begin.

Normalization ensures that all Engineering Modules receive data in a uniform format regardless of the originating machine software version or export format.

This module performs **data standardization only**.

It shall **not** perform engineering calculations.

---

# Scope

The module

Receives

Raw Parsed Data

Produces

Normalized Engineering Dataset

---

# Responsibilities

Normalize Units

Normalize Time Base

Normalize Channel Names

Normalize Numeric Format

Normalize Missing Values

Normalize Metadata

Normalize Sample Information

Generate Internal Dataset

---

# Workflow

```
Parsed Data

↓

Metadata Normalization

↓

Unit Normalization

↓

Channel Normalization

↓

Value Normalization

↓

Internal Dataset

↓

Engineering Engine
```

---

# Engineering Independence

This module

does NOT calculate

Yield Strength

Ultimate Strength

Young's Modulus

Stress

Strain

Fracture Point

Any engineering property.

It only prepares data.

---

# Unit Normalization

Internal Units

Force

N

Stress

MPa

Length

mm

Extension

mm

Time

s

Temperature

°C

---

# Accepted Input Units

Force

N

kN

kgf

Length

mm

cm

m

Time

s

ms

Temperature

°C

Administrator configurable.

---

# Channel Name Normalization

Examples

```
Force

Load

LOAD

LOAD CELL

↓

Force
```

```
Extension

Elongation

Deformation

↓

Extension
```

```
Crosshead

Displacement

Stroke

↓

Displacement
```

---

# Numeric Normalization

Convert

Scientific Notation

↓

Decimal

Convert

Comma Separator

↓

Decimal Point

Remove

Leading Spaces

Trailing Spaces

Invalid Characters

---

# Missing Values

NULL

↓

Internal NULL

Empty Text

↓

Empty String

No interpolation performed.

---

# Metadata Normalization

Normalize

Material Name

Material Grade

Standard Name

Specimen Shape

Operator Name

Certificate Number

Customer Name

---

# Specimen Normalization

Supported Shapes

Round

Flat

Pipe

Wire

Spring

Custom

Dimensions stored in standard format.

---

# Internal Dataset Structure

```
NormalizedTest

 ├── Header

 ├── Metadata

 ├── Channels

 ├── Measurements

 ├── Units

 └── Status
```

---

# Ordering

Measurements shall be ordered by

Time

Ascending

Duplicate timestamps are logged.

---

# Precision

Internal precision

Double Precision Floating Point

No rounding performed.

Display rounding occurs only during reporting.

---

# Validation

Verify

Normalized Units

Required Channels

Time Sequence

Numeric Format

Metadata Completeness

---

# Database

SQLite

Tables

```
tblNormalizedTest

tblNormalizedChannel

tblNormalizedData
```

---

# Logging

Each normalization stores

Normalization ID

Operator

Timestamp

File ID

Version

Warnings

Errors

---

# Error Handling

Unknown Unit

↓

Reject

Unknown Channel

↓

Warning

Corrupted Numeric Value

↓

Reject

Invalid Metadata

↓

Warning

---

# Future Enhancements

Automatic Metadata Recognition

AI Channel Mapping

Custom Normalization Profiles

Reserved

---

# Acceptance Criteria

✔ Engineering independent

✔ Unit normalization

✔ Channel normalization

✔ Metadata normalization

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No machine communication

✔ ISO/IEC 17025 compliant

---

End of Document
