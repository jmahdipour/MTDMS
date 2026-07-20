# Machine Profile Configuration

Document ID : MTDMS-IMP-020

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines how Machine Profiles are configured inside MTDMS.

Machine Profiles allow the software to support any testing machine without changing the VBA source code.

The Engineering Engine remains completely independent of machine manufacturers.

---

# Architecture

```
Machine

↓

Machine Profile

↓

Header Mapping

↓

Column Mapping

↓

Unit Mapping

↓

Validation Rules

↓

Universal Internal Data
```

---

# Configuration Storage

Machine Profiles may be stored in

SQLite Database

or

XML

or

JSON

Future

For Excel 2019 the preferred method is SQLite.

---

# SQLite Table

MachineProfiles

| Field | Type |
|---------|------|
| ProfileID | Integer |
| Manufacturer | Text |
| Model | Text |
| Version | Text |
| Active | Boolean |
| Created | DateTime |
| Updated | DateTime |

---

# Header Mapping Table

HeaderMap

| Field | Description |
|---------|-------------|
| ProfileID | Foreign Key |
| ExternalName | Machine Header |
| InternalName | MTDMS Header |

Example

```
Load Cell

↓

MachineLoadCell
```

---

# Column Mapping Table

ColumnMap

| Field | Description |
|---------|-------------|
| ProfileID | Foreign Key |
| ExternalColumn | Machine Column |
| InternalColumn | Universal Column |

Example

```
Travel

↓

Stroke
```

---

# Unit Mapping Table

UnitMap

| Field | Description |
|---------|-------------|
| ProfileID | Foreign Key |
| Quantity | Force |
| ExternalUnit | kgf |
| InternalUnit | N |
| Factor | 9.80665 |

---

# Validation Rules

ValidationProfile

Contains

Required Header

Required Columns

Allowed Units

Maximum Load

Minimum Load

Geometry Types

Engineering Limits

---

# Geometry Profile

Supported

Round

Flat

Pipe

Spring

Ring

Each profile defines

Area Calculation

Required Dimensions

Default Units

---

# Load Cell Configuration

Each Machine Profile may define

Load Cell Count

Capacity

Accuracy

Calibration Date

Example

```
100 kg

500 kg

2 ton

10 ton

25 ton
```

---

# Extensometer Configuration

Each profile may define

Number of Extensometers

Measurement Range

Resolution

Calibration Date

---

# Parser Initialization

```
Read Profile

↓

Load Header Map

↓

Load Column Map

↓

Load Units

↓

Load Validation Rules

↓

Ready
```

---

# Unknown Profile

If no profile found

↓

Load Generic Profile

↓

Warn Operator

↓

Continue

---

# Profile Versioning

Every profile contains

Major Version

Minor Version

Revision

Compatibility Level

---

# Administrator Functions

Administrator may

Create Profile

Edit Profile

Disable Profile

Duplicate Profile

Delete Profile

Export Profile

Import Profile

---

# Operator Permissions

Operator may

View Profile

Select Profile

Cannot Modify

---

# Backup

Profiles included in

SQLite Backup

Workbook Backup

Configuration Export

---

# Future Extensions

Automatic Profile Detection

Online Profile Repository

Manufacturer SDK

Cloud Synchronization

Reserved

---

# Acceptance Criteria

✔ Configuration stored outside VBA code

✔ Machine independent

✔ Expandable

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No Engineering Engine modification required

---

End of Document
