# TXT Unit Conversion Engine

Document ID : MTDMS-IMP-040

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Module

Import Engine

---

# Purpose

The Unit Conversion Engine converts every imported value into the internal engineering unit system before the data is stored inside SQLite.

The remainder of MTDMS shall always work with one unified unit system regardless of the testing machine manufacturer.

No engineering calculation shall use the original TXT units.

---

# Design Philosophy

TXT

↓

Read Original Unit

↓

Recognize Unit

↓

Convert

↓

Validate

↓

Store Internal Value

↓

Engineering Engine

---

# Internal Standard Units

| Quantity | Internal Unit |
|-----------|---------------|
| Force | Newton (N) |
| Stress | MPa |
| Length | mm |
| Extension | mm |
| Stroke | mm |
| Strain | mm/mm |
| Time | s |
| Speed | mm/min |
| Temperature | °C |
| Angle | Degree |

---

# Conversion Sequence

Read Header

↓

Detect Unit

↓

Read Numeric Value

↓

Apply Conversion Factor

↓

Store Converted Value

↓

Audit Log

---

# Force Conversion

Supported Units

N

kN

kgf

tf

lbf

kip

---

## Newton

```
N

↓

N
```

Factor

1.0

---

## Kilonewton

```
kN

↓

N
```

Factor

1000

---

## Kilogram Force

```
kgf

↓

N
```

Factor

9.80665

---

## Ton Force

```
tf

↓

N
```

Factor

9806.65

---

## Pound Force

```
lbf

↓

N
```

Factor

4.448221615

---

## Kip

```
kip

↓

N
```

Factor

4448.221615

---

# Stress Conversion

Supported

MPa

GPa

psi

ksi

Pa

---

## MPa

Factor

1

---

## GPa

```
GPa

↓

MPa
```

Factor

1000

---

## psi

```
psi

↓

MPa
```

Factor

0.006894757

---

## ksi

```
ksi

↓

MPa
```

Factor

6.894757

---

## Pascal

```
Pa

↓

MPa
```

Factor

0.000001

---

# Length Conversion

Supported

mm

cm

m

inch

µm

---

## mm

Factor

1

---

## cm

Factor

10

---

## m

Factor

1000

---

## inch

Factor

25.4

---

## µm

Factor

0.001

---

# Time Conversion

Supported

s

ms

min

---

Second

Factor

1

Millisecond

0.001

Minute

60

---

# Speed Conversion

Supported

mm/min

mm/s

m/min

m/s

inch/min

---

All converted to

```
mm/min
```

---

# Temperature

Supported

°C

°F

K

Internal

°C

Conversion

```
°F

↓

°C
```

```
(°F-32)/1.8
```

---

```
K

↓

°C
```

```
K-273.15
```

---

# Strain

Supported

mm/mm

%

µε

Internal

```
mm/mm
```

Conversion

```
%

↓

0.01
```

```
µε

↓

1×10⁻⁶
```

---

# Automatic Detection

Examples

```
Force(kN)

↓

kN
```

```
Stress(MPa)

↓

MPa
```

```
Stroke(mm)

↓

mm
```

Parser extracts units automatically from

Header

Column Name

Machine Profile

---

# Unknown Units

Unknown Unit

↓

Warning

↓

Operator Selection

↓

Store Mapping

↓

Continue Import

---

# SQLite Tables

```
tblUnits

tblUnitAliases

tblConversionFactors
```

---

# Audit Trail

Every conversion records

Original Unit

Converted Unit

Conversion Factor

Operator Override

Timestamp

---

# Precision

Internal storage

Double Precision

Minimum

15 significant digits

---

# Administrator Functions

Administrator may

Add Units

Modify Factors

Disable Units

Export Dictionary

Import Dictionary

Without changing VBA code

---

# Future Units

bar

MPsi

kg/cm²

N/mm²

Reserved

---

# Acceptance Criteria

✔ Automatic unit detection

✔ Automatic conversion

✔ SQLite configurable

✔ Double precision

✔ Audit logged

✔ Excel 2019 compatible

✔ Engineering Engine receives unified units only

---

End of Document
