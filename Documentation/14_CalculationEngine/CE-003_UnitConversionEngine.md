# Unit Conversion Engine

Document ID : MTDMS-CE-003

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Input

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Unit Conversion Engine converts all imported measurement units into a single internal engineering unit system before any engineering calculation is performed.

The conversion process is automatic, deterministic, and fully traceable.

The original imported values remain unchanged.

---

# Objectives

The Unit Conversion Engine shall

• Detect imported engineering units

• Convert values to internal units

• Preserve original imported values

• Prevent mixed-unit calculations

• Supply normalized data to the Calculation Engine

---

# Engineering Philosophy

Imported TXT

↓

Imported Units

↓

Unit Conversion

↓

Normalized Engineering Data

↓

Engineering Calculation

Engineering calculations are performed only on normalized values.

---

# Internal Engineering Units

The application shall internally use SI-based units.

| Quantity | Internal Unit |
|----------|---------------|
| Force | N |
| Stress | MPa |
| Length | mm |
| Extension | mm |
| Displacement | mm |
| Strain | mm/mm |
| Time | s |
| Temperature | °C |
| Energy | J |

Reports may display different units without affecting calculations.

---

# Conversion Workflow

```
Read TXT

↓

Detect Units

↓

Verify Units

↓

Convert to Internal Units

↓

Store Internal Dataset

↓

Engineering Calculation
```

---

# Force Conversion

Supported imported units

N

kN

kgf

lbf

Examples

1 kN

↓

1000 N

----------------------------

1 kgf

↓

9.80665 N

----------------------------

1 lbf

↓

4.44822 N

---

# Stress Conversion

Supported

MPa

GPa

N/mm²

psi

Examples

1 GPa

↓

1000 MPa

---

# Length Conversion

Supported

mm

cm

m

inch

Examples

1 cm

↓

10 mm

----------------------------

1 m

↓

1000 mm

----------------------------

1 inch

↓

25.4 mm

---

# Strain Conversion

Supported

%

mm/mm

Examples

1 %

↓

0.01 mm/mm

Internal calculations use mm/mm.

Report formatting may convert back to %.

---

# Time Conversion

Supported

ms

s

min

Examples

1000 ms

↓

1 s

---

# Energy Conversion

Supported

J

kJ

Examples

1 kJ

↓

1000 J

---

# Temperature Conversion

Supported

°C

K

Examples

293.15 K

↓

20 °C

---

# Original Values

The engine shall preserve

Original Value

Original Unit

Converted Value

Internal Unit

for complete traceability.

---

# Unit Database

All conversion factors are obtained from

tblUnit

No conversion factors shall be hardcoded inside the VBA calculation modules.

---

# Engineering Independence

Unit conversion

shall never

change

Imported TXT

Original Measurements

Only the internal working dataset is converted.

---

# SQLite Interaction

Converted values are not stored permanently.

SQLite stores

Final engineering results

Original imported units

Import history

Configuration

---

# Error Handling

Unknown Unit

↓

Abort

Missing Conversion Factor

↓

Abort

Mixed Unit Error

↓

Reject

Invalid Unit Symbol

↓

Reject

---

# Performance Targets

Unit Detection

< 20 ms

Unit Conversion

< 50 ms

Typical Tensile Dataset

< 100 ms

---

# Acceptance Criteria

✔ Automatic unit detection

✔ Automatic SI normalization

✔ Original imported values preserved

✔ No hardcoded conversion factors

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
