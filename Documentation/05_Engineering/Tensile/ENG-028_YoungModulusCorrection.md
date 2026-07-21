# Young's Modulus Based Graph Correction

Document ID : MTDMS-ENG-028

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

This document defines the algorithm used to correct the horizontal axis (strain/displacement) of the tensile curve using the Young's Modulus stored in the Material Library.

This correction is performed **only for graphical representation**.

The original imported data shall never be modified.

---

# Reference Standards

ISO 6892-1

ASTM E111

ISO 17025

---

# Background

In many universal testing machines,

Force measurement is highly accurate,

while displacement contains systematic errors caused by

• Grip compliance

• Machine frame deformation

• Crosshead backlash

• Fixture deformation

• Extensometer installation

As a result,

the initial elastic slope of the measured curve may differ from the theoretical Young's Modulus.

---

# Objective

Modify the horizontal axis so that

```
Elastic Slope

=

Young's Modulus

(Material Library)
```

without changing

• Force

• Stress

• Raw data

• Stored engineering values

---

# Scope

Correction applies only to

Display Graph

Exported Corrected Graph

Presentation

Report Figure

The following shall NEVER be modified

Raw TXT File

Imported Database

Engineering Results

Original Stress Array

Original Force Array

---

# Inputs

Engineering Stress Array

Engineering Strain Array

Measured Young's Modulus

Reference Young's Modulus

Material Library

Yield Point

---

# Outputs

Corrected Strain Array

Corrected Graph

Correction Factor

Correction Report

---

# Definitions

Measured Young

```
E_measured
```

Reference Young

```
E_reference
```

Correction Factor

```
CF
```

---

# Correction Factor

```
CF

=

E_measured

/

E_reference
```

---

# Horizontal Axis Correction

Corrected strain

```
εcorrected

=

εmeasured

×

CF
```

Equivalent displacement

```
ΔLcorrected

=

ΔLmeasured

×

CF
```

---

# Stress Values

Engineering Stress

Shall NEVER be modified.

Force

Shall NEVER be modified.

---

# Correction Region

Correction starts

Sample 0

Correction ends

Yield Point

---

# Behaviour After Yield

After Yield,

the correction gradually transitions to

Measured Data.

Reason

Plastic deformation shall remain unchanged.

---

# Transition Algorithm

Region A

Elastic

100% Corrected

↓

Region B

Transition

Linear Blend

↓

Region C

Plastic

Raw Data

---

# Blend Function

Between

Yield

and

Transition End

```
εdisplay

=

w εcorrected

+

(1−w) εraw
```

Where

```
0 ≤ w ≤ 1
```

---

# Transition Length

Default

10 %

after Yield

Administrator configurable.

---

# Material Verification

Difference

```
|Emeasured−Ereference|

/

Ereference
```

If

Difference

>

3 %

↓

Warning

Material Verification Recommended

---

# Graph Behaviour

Original Graph

Hidden

Corrected Graph

Displayed

Operator may switch between

Original

Corrected

Overlay

---

# Database

Original Data

Stored

Corrected Data

Not Stored

Only

Correction Parameters

are stored.

---

# SQLite Storage

Table

```
tblGraphCorrection
```

Fields

ReferenceYoung

MeasuredYoung

CorrectionFactor

CorrectionMethod

Operator

Timestamp

---

# Audit Requirements

Every correction shall record

Original Young

Reference Young

Correction Factor

Operator

Date

Reason

---

# Report

Final Report

Displays

Corrected Graph

Original numerical values

remain unchanged.

---

# Error Conditions

Reference Young Missing

↓

Abort Correction

Measured Young Missing

↓

Abort Correction

Correction Factor ≤ 0

↓

Engineering Error

Overflow

↓

Abort

---

# Performance

Complexity

```
O(n)
```

One multiplication

per sample

---

# Future Enhancements

Nonlinear Compliance Correction

Machine Compliance Compensation

Grip Compliance Compensation

Polynomial Correction

Automatic Calibration Learning

Reserved

---

# Acceptance Criteria

✔ Raw data never modified

✔ Stress never modified

✔ Force never modified

✔ Elastic slope matches Material Library

✔ ISO 17025 traceability

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Supports Original / Corrected graph switching

---

End of Document
