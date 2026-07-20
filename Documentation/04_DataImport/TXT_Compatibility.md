# TXT Compatibility Specification

Document ID : MTDMS-IMP-008

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Input

TXT Files Only

---

# Purpose

This document defines compatibility requirements for TXT files imported into MTDMS.

The objective is to support multiple testing machines without modifying the engineering engine.

Machine-specific TXT formats shall be translated into one common internal data structure.

---

# Design Philosophy

```
Machine TXT

↓

Machine Profile

↓

TXT Parser

↓

Universal Internal Format

↓

Engineering Engine

↓

Graphs

↓

Reports
```

The Engineering Engine shall never depend on a specific machine manufacturer.

---

# Supported Machine Categories

Universal Testing Machines

Compression Testing Machines

Bending Testing Machines

Spring Testing Machines

Ring Stiffness Testing Machines

Future Modules

Impact Machines

Fatigue Machines

Hardness Systems

---

# Manufacturer Compatibility

## Shimadzu

Status

Supported

Expected Export

TXT

Typical Units

kN

mm

Second

Remarks

Primary reference implementation.

---

## FATEK PLC Based Systems

Status

Supported

Communication

Ethernet

TXT Export

Supported

Typical Units

Configurable

Remarks

Machine profile determines mapping.

---

## Custom Industrial Machines

Status

Supported

Requirement

TXT export with configurable column mapping.

---

# Internal Universal Column Mapping

Every imported file is converted into the following internal structure:

```
Index

Time

Force

Stroke

Extension

EngineeringStress

EngineeringStrain

Temperature

Flags
```

Regardless of the original TXT format.

---

# Header Compatibility

Recognized Header Names

```
Force

Load

F

TestForce
```

All map to

```
Force
```

Likewise

```
Stroke

Displacement

Crosshead

Travel
```

↓

Stroke

---

# Time Compatibility

Recognized

```
Time

Elapsed

t

Seconds
```

↓

Time

---

# Extension Compatibility

Recognized

```
Extension

Elongation

Extensometer

GaugeExtension
```

↓

Extension

---

# Force Compatibility

Recognized

```
Force

Load

TestingForce

AppliedLoad
```

↓

Force

---

# Automatic Alias Dictionary

Parser shall contain an alias dictionary.

Example

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
Elapsed Time

↓

Time
```

---

# Unit Compatibility

Force

N

kN

kgf

tf

Length

mm

cm

m

inch

Stress

MPa

N/mm²

psi

ksi

Automatic conversion required.

---

# Decimal Compatibility

Accepted

```
125.32

125,32
```

Automatically normalized.

---

# Date Compatibility

Accepted

```
2026-07-20

20/07/2026

07/20/2026
```

---

# Character Encoding

Supported

UTF-8

ANSI

UTF-16

Automatic detection.

---

# Delimiter Compatibility

Supported

Tab

Comma

Semicolon

Space

Automatic delimiter detection required.

---

# Missing Columns

If missing

Engineering Stress

↓

Calculated

Engineering Strain

↓

Calculated

Extension

↓

Fallback to Stroke

when permitted by selected standard.

---

# Unsupported Features

Binary files

Encrypted TXT

Compressed TXT

Multi-sheet exports

Database exports

XML exports

JSON exports

are not supported.

---

# Machine Profile Files

Every supported machine may have

```
MachineProfile.xml

or

MachineProfile.db
```

containing

Header aliases

Column aliases

Units

Default settings

Calibration information

---

# Backward Compatibility

Older TXT files shall remain readable after software updates whenever possible.

New parser versions shall not invalidate archived laboratory data.

---

# Forward Compatibility

Unknown columns

↓

Ignored

Unknown header fields

↓

Logged

Future versions may use these fields without affecting current imports.

---

# Validation Priority

Machine Profile

↓

Header

↓

Column Names

↓

Units

↓

Data

---

# Performance Requirement

Machine identification

< 50 ms

Alias mapping

< 100 ms

100000-row compatibility conversion

< 2 seconds

---

# Future Compatibility

Reserved support

Instron

Zwick/Roell

MTS

Tinius Olsen

Galdabini

Custom PLC Systems

Additional profiles shall require no modification to the Engineering Engine.

---

# Acceptance Criteria

✔ TXT format independent

✔ Machine independent

✔ Automatic alias recognition

✔ Automatic unit conversion

✔ Universal internal data structure

✔ Backward compatible

✔ Forward compatible

---

End of Document
