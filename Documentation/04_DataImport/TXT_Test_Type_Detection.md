# Test Type Detection Specification

Document ID : MTDMS-IMP-023

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines how MTDMS automatically detects the mechanical test type after importing a TXT file.

The detection determines which Engineering Module shall receive the imported data.

No engineering calculation begins until the test type has been identified.

---

# Philosophy

TXT File

↓

Machine Profile

↓

Header Analysis

↓

Column Analysis

↓

Test Detection

↓

Engineering Module

---

# Detection Priority

1

Project Settings

↓

2

Header Information

↓

3

Machine Profile

↓

4

Column Analysis

↓

5

Operator Selection

---

# Supported Test Types

| Test | Engineering Module |
|-------|--------------------|
| Tensile | Tensile Module |
| Compression | Compression Module |
| Three Point Bend | Bend Module |
| Four Point Bend | Bend Module |
| Spring | Spring Module |
| Ring Stiffness | Ring Module |
| Future Impact | Impact Module |
| Future Fatigue | Fatigue Module |

---

# Tensile Detection

Typical Header

```
Tensile Test
```

or

```
ISO 6892
```

Typical Columns

```
Time

Force

Stroke

Extension
```

Result

Engineering Module

```
Tensile
```

---

# Compression Detection

Typical Header

```
Compression
```

Columns

```
Time

Force

Stroke
```

No Extension

Required

Result

Compression Module

---

# Three Point Bend

Typical Header

```
Three Point Bending
```

Columns

Force

Stroke

Support Span

Result

Bend Module

Mode

3 Point

---

# Four Point Bend

Typical Header

```
Four Point Bending
```

Result

Bend Module

Mode

4 Point

---

# Spring Test

Typical Header

```
Spring
```

Columns

Force

Compression

Result

Spring Module

---

# Ring Stiffness

Typical Header

```
Ring Stiffness

ISO9969
```

Columns

Force

Displacement

Result

Ring Module

---

# Unknown Test

If detection fails

↓

Operator Dialog

↓

Select Test

↓

Continue

Selection stored with project.

---

# Detection Confidence

100%

Explicit Header

90%

Machine Profile

80%

Column Pattern

60%

Manual Confirmation

---

# Detection Rules

## Tensile

Must contain

Force

Stroke

Area

Gauge Length

Material

---

## Compression

Must contain

Force

Stroke

No Gauge Length Required

---

## Spring

Must contain

Force

Compression

Spring Constant

Optional

---

## Ring

Must contain

Force

Displacement

Pipe Diameter

Optional

---

# SQLite Storage

Field

```
TestType
```

Examples

```
Tensile

Compression

Bending

Spring

Ring
```

---

# Ribbon Behavior

After detection

Ribbon automatically enables

Correct Module

Disables

Irrelevant Commands

Example

Spring Test

↓

Hide Tensile Yield Functions

↓

Show Spring Constant Tools

---

# Future Tests

Charpy

Hardness

Creep

Fatigue

Torsion

Reserved

---

# Logging

Store

Detected Test

Detection Method

Confidence

Operator Override

Timestamp

---

# Acceptance Criteria

✔ Automatic test recognition

✔ Machine independent

✔ SQLite compatible

✔ Ribbon adapts automatically

✔ Manual override available

✔ Complete audit trail

---

End of Document
