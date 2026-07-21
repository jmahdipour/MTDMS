# Elongation After Fracture Calculation

Document ID : MTDMS-ENG-021

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Engineering → Tensile

Status

Production

---

# Purpose

This document defines the calculation of elongation after fracture.

Elongation after fracture is one of the principal mechanical properties reported in tensile testing.

The calculation shall comply with

ISO 6892-1

ASTM E8/E8M

---

# Reference Standards

ISO 6892-1

ASTM E8 / ASTM E8M

ISO 630

ISO 898

INSO 3132

---

# Definition

Elongation after fracture is the permanent increase in gauge length measured after the fractured specimen has been carefully reassembled.

It shall **never** be calculated from crosshead displacement.

---

# Formula

```
A = ((Lu − L0) / L0) × 100
```

Where

A

Elongation After Fracture

%

Lu

Final Gauge Length After Fracture

L0

Original Gauge Length

---

# Variables

Input

Original Gauge Length

Final Gauge Length

Output

Elongation %

---

# Data Source Priority

1

Operator Measurement

↓

2

Digital Measuring Device

↓

3

Manual Entry

Crosshead displacement

Shall NEVER be used.

---

# Measurement Procedure

Operator

Joins

Fractured specimen

↓

Measures

Final Gauge Length

↓

Enters

Lu

↓

Software Calculates

Elongation

---

# Units

Length

mm

Result

%

---

# Example

Original Gauge Length

50.000 mm

Final Gauge Length

62.350 mm

```
A

=

((62.35−50)/50)

×

100

=

24.70 %
```

---

# Validation

```
Lu

>

L0
```

---

```
L0

>

0
```

---

```
A

≥

0 %
```

---

# Warning Conditions

Very Large Elongation

↓

Material Verification Recommended

Very Small Elongation

↓

Possible Measurement Error

---

# Error Conditions

Lu ≤ L0

↓

Invalid Measurement

L0 = 0

↓

Abort

Missing Lu

↓

Operator Prompt

Negative Result

↓

Engineering Error

---

# Manual Correction

Operator

May edit

Final Gauge Length

↓

Software

Immediately

Recalculates

Elongation

↓

Audit Logged

---

# Storage

SQLite

Table

```
tblEngineeringResult
```

Fields

```
OriginalGaugeLength

FinalGaugeLength

ElongationPercent
```

---

# Graph

Elongation After Fracture

Shall NOT be taken from the graph.

It is a laboratory measurement.

Graph values

remain unchanged.

---

# Report

Certificate Displays

Original Gauge Length

Final Gauge Length

Elongation %

Measurement Method

Operator

Date

---

# Audit Trail

Store

Previous Value

New Value

Operator

Timestamp

Reason

---

# Future Enhancements

Automatic Camera Measurement

Digital Caliper Interface

Image Processing

Reserved

---

# Acceptance Criteria

✔ ISO 6892-1 compliant

✔ ASTM E8 compliant

✔ Uses measured Lu only

✔ Crosshead displacement prohibited

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Full audit traceability

---

End of Document
