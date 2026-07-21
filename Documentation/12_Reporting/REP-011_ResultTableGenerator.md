# Result Table Generator

Document ID : MTDMS-REP-011

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Reporting

Status

Production

---

# Purpose

The Result Table Generator creates standardized engineering result tables for laboratory reports.

It formats validated engineering results into structured tables.

The module performs no engineering calculations.

The module never modifies engineering values.

---

# Objectives

The module shall

• Generate standardized result tables

• Maintain engineering accuracy

• Preserve engineering units

• Support multiple report formats

• Support configurable layouts

• Support multilingual headers

---

# Workflow

```
Validated Engineering Results

↓

Result Table Generator

↓

Table Layout

↓

Formatting

↓

Report Engine
```

---

# Data Source

The table receives data only from

Validated Engineering Results.

No value is calculated inside the report.

---

# Supported Test Types

Tensile Test

Compression Test

Bending Test

Spring Test

Ring Stiffness Test

Rockwell Hardness

Brinell Hardness

Vickers Hardness

Charpy Impact

Chemical Analysis

Future Tests

---

# Standard Table Structure

| Item | Symbol | Value | Unit |
|------|--------|------:|------|

Default layout.

Administrator configurable.

---

# Tensile Test Example

| Property | Symbol | Value | Unit |
|----------|--------|------:|------|
| Yield Strength | ReH / Rp0.2 | xxx | MPa |
| Ultimate Strength | Rm | xxx | MPa |
| Young's Modulus | E | xxx | GPa |
| Elongation | A | xx | % |
| Reduction of Area | Z | xx | % |
| Maximum Force | Fmax | xxx | N / kN / kgf |

---

# Compression Example

| Property | Symbol | Value | Unit |

Maximum Load

Compressive Strength

Displacement

Strain

Energy

---

# Hardness Example

| Property | Symbol | Value | Unit |

Hardness

Scale

Load

Holding Time

Standard

---

# Charpy Example

| Property | Symbol | Value | Unit |

Impact Energy

Temperature

Specimen Size

Orientation

Standard

---

# Chemical Analysis Example

| Element | Value | Unit |

Carbon

Silicon

Manganese

Chromium

Nickel

...

Administrator configurable.

---

# Number Formatting

Configurable

Decimal Places

Scientific Notation

Thousands Separator

Decimal Separator

Engineering values remain unchanged.

---

# Unit Formatting

Supported

MPa

GPa

N

kN

kgf

mm

%

J

HRC

HBW

HV

ppm

%

Others

---

# Empty Values

If value

does not exist

↓

Display

—

No automatic substitution is permitted.

---

# Optional Columns

Tolerance

Minimum

Maximum

Acceptance Status

Reference Value

Remark

Administrator configurable.

---

# Table Style

Supports

Grid

Borderless

Laboratory Style

Customer Style

Custom Style

---

# Sorting

Default order

defined by

selected report template.

Manual sorting is disabled.

---

# Multilingual Support

Headers

may be translated.

Engineering symbols

shall remain unchanged.

Example

Yield Strength

↓

تنش تسلیم

↓

Rm

unchanged.

---

# SQLite Database

Tables

```
tblResultTable

tblResultField

tblResultLayout
```

---

# Audit Trail

Record

Certificate Number

Revision

Report Type

Template

Operator

Timestamp

Software Version

---

# Permissions

Administrator

Modify Layout

Quality Manager

Approve

Reviewer

Generate

Operator

Generate

---

# Error Handling

Missing Value

↓

Display —

Missing Unit

↓

Warning

Unknown Property

↓

Ignore

Database Failure

↓

Abort

---

# Future Enhancements

Dynamic Tables

Interactive Reports

Customer-specific Columns

AI Result Explanation

Reserved

---

# Acceptance Criteria

✔ Engineering values unchanged

✔ Configurable layout

✔ Multilingual headers

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
