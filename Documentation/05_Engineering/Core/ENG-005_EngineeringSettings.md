# Engineering Settings Specification

Document ID : MTDMS-ENG-005

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

Engineering Core

---

# Purpose

This document defines every configurable engineering parameter used by MTDMS.

All calculation parameters shall be editable through the Engineering Settings page.

Engineering algorithms shall never contain hard-coded constants unless they are physical constants.

---

# Design Philosophy

Engineering Settings

↓

SQLite

↓

Engineering Engine

↓

Calculation

Every calculation reads its configuration before execution.

---

# Storage

SQLite

Table

```
tblEngineeringSettings
```

---

# Table Structure

| Setting | Value | Unit | Description |
|----------|-------|------|-------------|
| YoungTolerance | 1 | % | Maximum deviation |
| RegressionR2 | 0.999 | - | Minimum acceptable R² |

---

# Categories

Geometry

Elastic Region

Young's Modulus

Yield

True Stress

Fracture

Statistics

Graphs

Validation

Reports

---

# Geometry Settings

Minimum Area

Maximum Area

Minimum Gauge Length

Maximum Gauge Length

Area Difference Tolerance

Default

±0.5 %

---

# Elastic Region Settings

Minimum Points

50

Maximum Points

Automatic

Regression Method

Least Squares

Minimum R²

0.9990

Preferred

0.9995

---

# Young's Modulus Settings

Reference Source

Material Library

Allowed Difference

±1 %

Maximum Difference

±3 %

Correction Mode

Display Only

Raw Data

Never Modified

---

# Yield Settings

Default Method

Rp0.2

Available Methods

Upper Yield

Lower Yield

Rp0.2

Rp0.1

Rp0.05

Rt

Manual

Operator Default

Rp0.2

---

# Rp Offset

Default

0.2 %

Editable

Yes

Range

0.01 %

↓

1 %

---

# True Stress Settings

Formula

ISO 6892

Editable

No

Engineering Data

Required

---

# Fracture Settings

Automatic Detection

Enabled

Noise Filter

Enabled

Minimum Drop

Configurable

---

# Statistics

Standard Deviation

Population

Sample

Selectable

Default

Sample

Outlier Detection

Disabled

Future

Reserved

---

# Graph Settings

Elastic Line

Visible

Yield Marker

Visible

Fracture Marker

Visible

Correction Layer

Visible

Engineering Layer

Visible

Raw Layer

Optional

---

# Validation Settings

Minimum Young R²

Configurable

Maximum Area Difference

Configurable

Maximum Geometry Difference

Configurable

Allow Warning Override

Yes

Allow Fail Override

No

---

# Report Settings

Display Units

SI

Default Decimal Places

Stress

2

Strain

5

Force

1

Extension

3

Young

0

---

# Physical Constants

Gravitational Acceleration

```
9.80665 m/s²
```

Editable

No

Pi

System Constant

Editable

No

---

# Administrator Functions

Administrator may

Add Settings

Modify Settings

Export Settings

Import Settings

Restore Defaults

No source code modification required.

---

# User Functions

Operator may modify

Graph Options

Yield Method

Decimal Places

Display Preferences

Operator may NOT modify

Physical Constants

Validation Rules

Database Parameters

---

# Version Control

Every change stores

Operator

Timestamp

Old Value

New Value

Reason

Audit Trail ID

---

# Restore Defaults

Ribbon Command

```
Restore Engineering Defaults
```

Confirmation Required

Yes

---

# Acceptance Criteria

✔ SQLite configurable

✔ No hard-coded engineering parameters

✔ Administrator editable

✔ Operator permissions respected

✔ Audit logged

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

---

End of Document
