# Engineering Calculation Validation

Document ID : MTDMS-VAL-003

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Validation

Status

Production

---

# Purpose

The Engineering Calculation Validation module verifies that all engineering calculations produced by MTDMS are mathematically, physically and logically consistent before they are accepted for reporting.

The module validates results.

It never recalculates or modifies engineering values.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ASTM E8/E8M

ASTM E111

Applicable product standards

---

# Objectives

The module shall

• Verify calculated engineering values

• Verify mathematical consistency

• Verify physical plausibility

• Detect impossible results

• Detect missing calculations

• Prevent invalid reports

---

# Validation Workflow

```
Engineering Engine

↓

Calculated Results

↓

Calculation Validation

↓

PASS

WARNING

FAIL

↓

Report Engine
```

---

# Validation Scope

Engineering Stress

Engineering Strain

True Stress

True Strain

Young's Modulus

Yield Strength

Ultimate Tensile Strength

Elongation

Reduction of Area

Proof Strength

Maximum Force

Fracture Point

---

# Mathematical Validation

Verify

No division by zero

No overflow

No undefined values

No NaN

No Infinity

All equations completed successfully

---

# Physical Validation

Verify

Young's Modulus > 0

Yield Strength ≥ 0

Ultimate Strength ≥ Yield Strength

Maximum Force ≥ Yield Force

Elongation ≥ 0

Reduction of Area

0%

≤ RA ≤

100%

---

# Consistency Validation

Verify

Stress corresponds to Force / Area

Engineering strain corresponds to extension

True stress exists only when applicable

True strain exists only when applicable

Fracture point exists

Maximum load exists

---

# Material-Based Validation

If Material Library contains reference values

↓

Compare

Expected Range

↓

Measured Result

Outside tolerance

↓

Warning

Material library values are used

only

as engineering references.

They never replace measured values.

---

# Standard Validation

Verify

Required properties for selected standard exist.

Example

ISO 6892-1

requires

Yield

UTS

Elongation

Young's Modulus (when applicable)

Missing mandatory result

↓

FAIL

---

# Graph Consistency

Verify

Maximum force matches graph peak

Yield marker lies on graph

Fracture point exists

Graph length equals imported dataset

---

# Precision Validation

Internal calculations

Double Precision

Displayed values

Rounded according to report settings.

No validation uses rounded values.

---

# Validation Results

PASS

PASS WITH WARNING

FAIL

MANUAL REVIEW REQUIRED

---

# Warning Examples

Young's Modulus unusually low

Yield manually selected

Material outside reference range

Unexpected fracture extension

---

# Failure Examples

UTS < Yield

Negative Young's Modulus

Stress undefined

Fracture before yield

Missing maximum force

Division by zero

---

# SQLite Database

Tables

```
tblCalculationValidation

tblCalculationValidationRule

tblCalculationValidationHistory
```

---

# Audit Trail

Record

Validation Rule

Calculated Value

Expected Condition

Status

Timestamp

Operator

Reviewer

---

# Permissions

Administrator

Full Access

Reviewer

Approve Warning

Operator

View Results

---

# Error Handling

Undefined Result

↓

FAIL

Impossible Engineering Value

↓

FAIL

Missing Required Result

↓

FAIL

Reference Range Missing

↓

Ignore

---

# Future Enhancements

Statistical Validation

AI Engineering Review

Automatic Cross-Standard Validation

Material Family Validation

Reserved

---

# Acceptance Criteria

✔ Mathematical validation

✔ Physical validation

✔ Standard validation

✔ Material reference comparison

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering values never modified

✔ ISO/IEC 17025 compliant

---

End of Document
