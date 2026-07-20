# Dimension Validation Specification

Document ID : MTDMS-IMP-025

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines all dimensional validation rules applied immediately after importing a TXT file.

Dimension validation ensures engineering calculations are performed only with physically valid specimen dimensions.

No engineering calculations shall start until every mandatory dimension has passed validation.

---

# Validation Sequence

TXT Import

↓

Geometry Recognition

↓

Dimension Validation

↓

Area Calculation

↓

Engineering Engine

---

# Validation Philosophy

Every dimension shall be

Present

Numeric

Positive

Within Engineering Limits

Consistent with Geometry

Traceable

---

# General Rules

Every dimension shall satisfy

```
Value > 0
```

No negative values accepted.

No zero values accepted.

---

# Accepted Numeric Formats

```
12

12.5

12,5

0.250

125.000
```

Automatically normalized.

---

# Invalid Values

Rejected

```
0

-12

ABC

NaN

Infinity

Blank
```

---

# Round Specimen Validation

Required

Diameter

Validation

Diameter > 0

Typical Range

1 mm

↓

100 mm

Outside limits

↓

Warning

Operator confirmation required.

---

# Flat Specimen Validation

Required

Width

Thickness

Validation

Width > 0

Thickness > 0

Typical Range

Width

2–100 mm

Thickness

0.2–50 mm

---

# Pipe Validation

Required

Outside Diameter

Wall Thickness

Validation

Outside Diameter > 0

Wall Thickness > 0

Wall Thickness < Radius

Otherwise

↓

Error

---

# Spring Validation

Required

Wire Diameter

Mean Coil Diameter

Free Length

Validation

All values > 0

Coil Diameter > Wire Diameter

---

# Ring Specimen Validation

Required

Diameter

Thickness

Length

Validation

All dimensions > 0

---

# Compression Specimen

Required

Length

Width

Height

or

Diameter

Height

Validation

All dimensions > 0

---

# Gauge Length Validation

Required

L0

Validation

```
L0 > 0
```

Recommended

10–250 mm

Outside range

↓

Warning

---

# Area Validation

Imported Area

↓

Calculated Area

Difference

```
≤ 1%
```

Accepted

Difference

```
>1%
```

↓

Operator Warning

↓

May continue

---

# Area Recalculation Rules

Round

```
A = πd²/4
```

Flat

```
A = b × t
```

Pipe

```
A = π(D²-(D-2t)²)/4
```

---

# Unit Validation

Dimensions must be converted to

Millimeter

before validation.

---

# Engineering Limits

Administrator configurable.

Stored in

SQLite

```
tblDimensionLimits
```

Fields

Minimum

Maximum

Warning Limit

Critical Limit

---

# Error Codes

DIM-0001

Missing Dimension

DIM-0002

Negative Dimension

DIM-0003

Zero Dimension

DIM-0004

Invalid Numeric Value

DIM-0005

Area Mismatch

DIM-0006

Geometry Conflict

---

# Operator Override

Allowed

Only

Warnings

Not Allowed

Critical Errors

All overrides logged.

---

# SQLite Logging

Stores

Original Value

Validated Value

Converted Value

Operator Override

Timestamp

Validation Result

---

# Future Validation

3D Geometry

CAD Import

Optical Measurement

Barcode Specimen

Reserved

---

# Acceptance Criteria

✔ Every dimension validated

✔ Automatic unit conversion

✔ Automatic area verification

✔ SQLite logging

✔ Operator override for warnings only

✔ Critical errors stop engineering calculations

---

End of Document
