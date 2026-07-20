# TXT Data Columns Specification

Document ID : MTDMS-IMP-004

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Input

TXT Files Only

---

# Purpose

This document defines every supported data column that may appear in machine-generated TXT files.

The parser shall automatically recognize columns regardless of order.

The parser shall never rely on fixed column positions.

---

# General Rules

Columns are identified by their names.

Column order is irrelevant.

Case insensitive.

Extra columns shall be ignored unless configured.

---

# Mandatory Columns

| Column | Required |
|----------|----------|
| Time | Yes |
| Force | Yes |
| Stroke | Yes |

Without these three columns the import shall fail.

---

# Optional Columns

| Column | Description |
|----------|-------------|
| Extension | Extensometer displacement |
| Stress | Machine calculated stress |
| Strain | Machine calculated strain |
| Temperature | Test temperature |
| Cycle | Fatigue cycle number |
| Channel | DAQ channel |
| Speed | Crosshead speed |
| Load Cell | Active load cell |
| Extensometer | Active extensometer |

---

# Preferred Internal Order

After import MTDMS stores data internally as

```
Index

Time

Force

Stroke

Extension

Engineering Stress

Engineering Strain

True Stress

True Strain

Speed

Temperature

Flags
```

---

# Time Column

Description

Elapsed test time

Accepted Units

Second

Millisecond

Minute

Automatic conversion

↓

Second

---

# Force Column

Description

Measured force

Accepted Units

kgf

N

kN

Automatic conversion

↓

Newton

Internal Unit

N

---

# Stroke Column

Description

Crosshead displacement

Accepted Units

mm

cm

m

Internal Unit

mm

---

# Extension Column

Description

Extensometer displacement

Preferred Source

Extensometer

Fallback

Crosshead

Internal Unit

mm

---

# Engineering Stress

If missing

Calculated

```
σ = F / A
```

Area obtained from

Material Header

Specimen Geometry

Material Library

---

# Engineering Strain

If missing

Calculated

```
ε = ΔL / L0
```

Source

Extension

or

Corrected Stroke

---

# True Stress

Automatically calculated

After Yield

```
σt = σ (1+ε)
```

---

# True Strain

Automatically calculated

```
εt = ln(1+ε)
```

---

# Speed

Description

Crosshead Speed

Units

mm/min

mm/s

Stored

Internal only

---

# Temperature

Optional

Used for reports.

Not used in engineering calculations.

---

# Cycle

Used only

Fatigue Module

Ignored

Current Version

---

# Flags

System generated

Examples

```
Yield Point

Fracture Point

Elastic Region

Noise

Invalid Sample
```

---

# Row Number

Every imported row receives

Internal Index

Starting

1

Independent of TXT numbering.

---

# Invalid Rows

Skipped

Examples

Blank Row

Missing Force

Missing Stroke

NaN

Overflow

Corrupted Text

Logged

ERROR_LOG

---

# Duplicate Rows

Detected

Automatically

Duplicate samples

Ignored

Logged

---

# Missing Values

Missing Extension

↓

Calculated

Missing Stress

↓

Calculated

Missing Strain

↓

Calculated

Missing Temperature

↓

Null

---

# Maximum Columns

Current Version

32

Future

128

---

# Internal Storage

Imported data stored in

```
tblRawData
```

Engineering calculations stored in

```
tblEngineering
```

Results stored in

```
tblResults
```

---

# Performance Target

100000 Rows

↓

Import

<5 seconds

Engineering conversion

<3 seconds

---

# Future Columns

Hydraulic Pressure

Motor Torque

PLC Status

Digital Inputs

Digital Outputs

Encoder Position

Reserved.

---

# Compatibility

Designed for

Shimadzu

Fatek PLC Based Systems

Universal Testing Machines

Compression Machines

Spring Test Machines

Ring Stiffness Machines

Future machine profiles can map their native columns into this internal structure.

---

End of Document
