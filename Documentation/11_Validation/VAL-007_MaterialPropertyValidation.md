# Material Property Validation

Document ID : MTDMS-VAL-007

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

The Material Property Validation module verifies that calculated engineering properties are compatible with the material selected by the user.

The module provides engineering consistency checks only.

It shall never modify measured values.

It shall never replace measured values with library values.

Material Library values are used only as engineering references.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ASTM E8/E8M

ISO 630

ISO 898

INSO 3132

Applicable customer specifications

---

# Objectives

The module shall

• Verify material selection

• Compare measured values with reference ranges

• Detect impossible combinations

• Detect material mismatch

• Assist reviewers

• Preserve measured values

---

# Workflow

```
Material Selected

↓

Material Library

↓

Engineering Results

↓

Reference Comparison

↓

Validation Result

↓

Reviewer
```

---

# Validation Scope

Material Grade

Material Family

Heat Treatment

Mechanical Properties

Chemical Properties (optional)

Product Form

Applicable Standard

---

# Material Families

Carbon Steel

Low Alloy Steel

Tool Steel

Stainless Steel

Cast Iron

Aluminium

Copper

Brass

Bronze

Titanium

Nickel Alloys

Plastic

Composite

Custom

---

# Verified Properties

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Hardness

Impact Energy

Density

Poisson Ratio
(Optional)

---

# Reference Values

Reference values are obtained from

Material Library

or

Applicable Standard

or

Customer Specification

Priority

Customer Specification

↓

Applicable Standard

↓

Material Library

---

# Comparison Logic

Measured Value

↓

Reference Range

↓

Inside Range

PASS

Outside Range

WARNING

Impossible Value

FAIL

---

# Important Rule

Reference values

shall NEVER

replace measured values.

The measured values remain the official test results.

---

# Material Mismatch Detection

Examples

Material selected

S235

Measured UTS

2400 MPa

↓

FAIL

Material selected

Aluminium

Young's Modulus

210 GPa

↓

WARNING

---

# Heat Treatment Validation

If Heat Treatment is defined

Compare

Annealed

Normalized

Quenched

Tempered

Solution Treated

Aged

Unknown

Only reference comparison is performed.

---

# Warning Examples

Measured value outside normal range

Material grade not found

Heat treatment unknown

Reference unavailable

---

# Failure Examples

Impossible Young's Modulus

Negative Strength

Negative Hardness

Negative Density

Undefined Material

---

# Validation Status

PASS

PASS WITH WARNING

FAIL

REFERENCE NOT AVAILABLE

---

# Reviewer Actions

Accept

Reject

Comment

Request Retest

Reference Updated

---

# SQLite Database

Tables

```
tblMaterialValidation

tblMaterialReference

tblMaterialValidationHistory
```

---

# Audit Trail

Record

Material

Reference Source

Measured Value

Reference Range

Validation Status

Reviewer

Timestamp

---

# Permissions

Administrator

Modify Reference Data

Quality Manager

Approve

Reviewer

Review

Operator

Read Only

---

# Error Handling

Material Missing

↓

WARNING

Reference Missing

↓

REFERENCE NOT AVAILABLE

Impossible Value

↓

FAIL

Database Error

↓

Abort Validation

---

# Future Enhancements

AI Material Recognition

Automatic Material Classification

Heat Treatment Prediction

Microstructure Correlation

Reserved

---

# Acceptance Criteria

✔ Material comparison completed

✔ Measured values preserved

✔ Reference values never overwrite results

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
