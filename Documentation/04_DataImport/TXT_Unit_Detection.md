# TXT Unit Detection Specification

Document ID : MTDMS-IMP-005

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Input

TXT Files Only

---

# Purpose

This document defines how MTDMS automatically detects engineering units contained in machine-generated TXT files.

The software shall automatically convert all imported values into a single internal engineering unit system.

Users shall never manually convert units.

---

# Philosophy

Machine Unit

↓

Automatic Detection

↓

Validation

↓

Conversion

↓

Internal Standard Unit

↓

Engineering Calculation

---

# Internal Standard Units

| Quantity | Internal Unit |
|------------|---------------|
| Force | N |
| Stress | MPa |
| Length | mm |
| Extension | mm |
| Stroke | mm |
| Time | s |
| Temperature | °C |
| Speed | mm/min |
| Area | mm² |
| Young's Modulus | MPa |

---

# Force Detection

Supported

N

Newton

kN

KN

kgf

Kgf

kg

Ton

tf

kgf

---

# Force Conversion

| Imported | Internal |
|------------|----------|
| N | N |
| kN | ×1000 |
| kgf | ×9.80665 |
| tf | ×9806.65 |
| ton | ×9806.65 |

---

# Stress Detection

Supported

MPa

N/mm²

kgf/mm²

kg/mm²

psi

ksi

---

# Stress Conversion

| Imported | MPa |
|------------|------|
| MPa | 1 |
| N/mm² | 1 |
| kgf/mm² | 9.80665 |
| psi | 0.00689476 |
| ksi | 6.89476 |

---

# Length Detection

Supported

mm

cm

m

inch

in

---

# Length Conversion

| Imported | mm |
|------------|------|
| mm | 1 |
| cm | ×10 |
| m | ×1000 |
| inch | ×25.4 |

---

# Area Detection

Supported

mm²

cm²

m²

in²

---

# Area Conversion

| Imported | mm² |
|------------|-------|
| mm² | 1 |
| cm² | ×100 |
| m² | ×1000000 |
| in² | ×645.16 |

---

# Time Detection

Supported

s

sec

ms

min

---

# Time Conversion

| Imported | Second |
|------------|---------|
| s | 1 |
| ms | ÷1000 |
| min | ×60 |

---

# Speed Detection

Supported

mm/min

mm/s

cm/min

m/min

---

# Internal Storage

mm/min

---

# Temperature Detection

Supported

°C

C

°F

K

---

# Temperature Conversion

Internal

°C

---

# Young's Modulus Detection

Supported

MPa

GPa

kgf/mm²

---

# Conversion

| Imported | MPa |
|------------|------|
| MPa | 1 |
| GPa | ×1000 |
| kgf/mm² | ×9.80665 |

---

# Automatic Recognition

The parser checks

Header

↓

Column Names

↓

Units

↓

Machine Profile

↓

Material Library

---

# Unknown Units

Unknown unit

↓

Warning

↓

Import suspended

↓

Operator confirmation required

---

# Mixed Units

Allowed

Example

Force

kN

Stroke

mm

Stress

MPa

Automatic conversion performed.

---

# Unit Consistency Check

Example

Header

Force

kN

Column

Force(N)

↓

Conflict

↓

Import Error

---

# Unit Validation Priority

1

Header

↓

2

Column Name

↓

3

Machine Profile

↓

4

Default Configuration

---

# Machine Profiles

Future machine profiles may override automatic detection.

Example

Shimadzu

Always exports

kN

mm

Second

---

# Storage Rules

Original Unit

Stored

Converted Unit

Stored

Conversion Factor

Stored

SQLite History

Stores all three values.

---

# Logging

Every import logs

Detected Units

Conversion Factors

Warnings

Operator Override

---

# Future Units

lbf

kip

bar

MPsi

μm

μstrain

Reserved.

---

# Acceptance Criteria

✔ Automatic force detection

✔ Automatic stress detection

✔ Automatic length detection

✔ Automatic area detection

✔ Automatic time detection

✔ Automatic temperature detection

✔ Automatic engineering conversion

✔ Internal unit consistency guaranteed

---

End of Document
