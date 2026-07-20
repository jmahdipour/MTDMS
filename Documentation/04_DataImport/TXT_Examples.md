# TXT Examples

Document ID : MTDMS-IMP-010

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Input

TXT Files Only

---

# Purpose

This document provides reference TXT files supported by MTDMS.

These examples define the expected structure used by the parser.

The Engineering Engine shall work with all examples without modification.

---

# Example 1

Standard Tensile Test

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

--------------------------------------------------

Time    Stroke    Extension    Force

0.000   0.000     0.000        0.000

0.050   0.003     0.001        0.041

0.100   0.006     0.002        0.083

0.150   0.009     0.003        0.126

...
```

Result

Accepted

---

# Example 2

No Extension Column

```
Machine = Shimadzu

Material = AISI1045

Area = 50

L0 = 25

Force Unit = N

Length Unit = mm

-----------------------------------

Time    Stroke    Force

0.000   0.000     0

0.050   0.005     120

0.100   0.010     248

...
```

Result

Extension calculated from Stroke.

Accepted.

---

# Example 3

Machine Already Calculates Stress

```
Time

Stroke

Force

Stress

Strain
```

Result

Stress and Strain imported.

Engineering Engine verifies consistency.

---

# Example 4

Round Specimen

```
Diameter = 12.50

L0 = 50
```

Area calculated

```
A = πd²/4
```

---

# Example 5

Flat Specimen

```
Width = 12.50

Thickness = 6.00
```

Area

```
A = Width × Thickness
```

---

# Example 6

Pipe Specimen

```
Outside Diameter = 90

Thickness = 8
```

Parser loads Pipe Geometry Module.

---

# Example 7

Spring Test

```
Time

Force

Compression
```

Parser activates

Spring Module

---

# Example 8

Three Point Bend

```
Time

Stroke

Force
```

Parser activates

Bending Module

---

# Example 9

Ring Stiffness

```
Time

Displacement

Force
```

Parser activates

Ring Stiffness Module

---

# Example 10

Invalid File

Missing

Force Column

```
Time

Stroke
```

Result

Rejected

Error

IMP-0302

---

# Example 11

Mixed Units

```
Force = kgf

Stroke = inch

Stress = psi
```

Result

Automatic conversion

↓

N

↓

mm

↓

MPa

---

# Example 12

Corrupted Rows

```
0.100

ABC

0.352
```

Result

Row skipped

Logged

Import continues.

---

# Example 13

Duplicate Samples

```
0.100

0.100
```

Result

Duplicate ignored.

---

# Example 14

Large File

Rows

100000

Result

Accepted

Performance target

<5 sec

---

# Example 15

Future Machine

Unknown Header

```
LoadValue

Travel

Elapsed
```

Machine Profile

↓

Alias Dictionary

↓

Mapped

Force

Stroke

Time

---

# Example Acceptance

Every example shall produce

✔ Successful Import

✔ Valid Engineering Data

✔ Correct Graph

✔ Correct Report

✔ SQLite Record

without modifying WorkbookTemplate.xlsm.

---

End of Document
