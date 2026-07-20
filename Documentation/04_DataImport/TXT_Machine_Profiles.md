# TXT Machine Profiles Specification

Document ID : MTDMS-IMP-016

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines the Machine Profile architecture.

Machine Profiles isolate machine-specific TXT formats from the Engineering Engine.

Regardless of the testing machine manufacturer, the Engineering Engine always receives the same internal data structure.

---

# Philosophy

Machine

↓

Machine Profile

↓

TXT Parser

↓

Universal Data Structure

↓

Engineering Engine

---

# Benefits

✔ Universal TXT Import

✔ No Engineering Engine modification

✔ Easy addition of new machines

✔ ISO 17025 traceability

✔ Future compatibility

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

Universal Data
```

---

# Profile Components

Every Machine Profile contains

Machine Information

Column Definitions

Header Mapping

Unit Mapping

Geometry Rules

Validation Rules

Capabilities

---

# Machine Information

Fields

Manufacturer

Model

Version

PLC

Communication

Export Format

Software Version

---

Example

```
Manufacturer

Shimadzu

Model

AG-25TB

Communication

TXT

Software

Trapezium X
```

---

# Header Mapping

Machine Header

↓

Universal Header

Example

```
Load Cell

↓

MachineLoadCell
```

```
Gauge Length

↓

L0
```

```
Specimen

↓

SpecimenID
```

---

# Column Mapping

Machine Column

↓

Universal Column

Example

```
Elapsed Time

↓

Time
```

```
Load

↓

Force
```

```
Travel

↓

Stroke
```

```
Extension

↓

Extension
```

---

# Unit Mapping

Machine Unit

↓

Internal Unit

Example

```
kN

↓

N
```

```
inch

↓

mm
```

---

# Geometry Rules

Supported

Round

Flat

Pipe

Spring

Ring

Future

Compression Block

---

# Validation Rules

Machine-specific

Minimum Force

Maximum Force

Supported Units

Mandatory Columns

Header Rules

---

# Machine Capabilities

Flags

Has Extensometer

Supports Stress

Supports Strain

Supports Temperature

Supports Multi Load Cell

Supports Multi Channel

---

# Internal Profile Object

```
MachineProfile

Manufacturer

Model

HeaderMap

ColumnMap

UnitMap

Geometry

Capabilities

Validation
```

---

# Current Supported Profiles

Profile 001

Shimadzu AG Series

Status

Supported

---

Profile 002

FATEK PLC Universal

Status

Supported

---

Profile 003

Generic Universal Testing Machine

Status

Supported

---

# Future Profiles

Instron

MTS

Zwick

Tinius Olsen

Galdabini

Reserved

---

# Profile Selection

Priority

Header

↓

Manufacturer

↓

Model

↓

Machine Signature

↓

Manual Selection

---

# Unknown Machine

If profile not found

↓

Generic Profile

↓

Warning

↓

Operator Confirmation

↓

Continue

---

# Profile Storage

Profiles stored inside

```
MachineProfiles.db
```

or

```
MachineProfiles.xml
```

Future

SQLite

---

# Version Control

Every profile has

Profile ID

Version

Release Date

Author

Revision History

---

# Profile Update

Administrator may

Add Profile

Update Profile

Disable Profile

Delete Profile

Operator

Read Only

---

# Logging

Import Log stores

Machine Profile ID

Machine Model

Profile Version

Parser Version

---

# Acceptance Criteria

✔ Machine independent architecture

✔ Engineering Engine independent of machine

✔ Easy profile expansion

✔ Excel 2019 compatible

✔ VBA compatible

✔ TXT only

---

End of Document
