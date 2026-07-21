# Result Consistency Validation

Document ID : MTDMS-VAL-008

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

The Result Consistency Validation module verifies that all engineering results generated from a single test are mutually consistent.

The objective is to detect contradictions between calculated values before report generation.

The module validates engineering relationships only.

It never modifies calculated values.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ASTM E8/E8M

ASTM E111

Applicable Product Standards

---

# Objectives

The module shall

• Verify internal consistency

• Detect contradictory results

• Detect missing relationships

• Detect impossible engineering combinations

• Prevent inconsistent reports

---

# Validation Workflow

```
Engineering Results

↓

Relationship Validation

↓

Consistency Rules

↓

PASS

WARNING

FAIL

↓

Report Generation
```

---

# Validation Scope

Engineering Stress

Engineering Strain

True Stress

True Strain

Yield Strength

Ultimate Tensile Strength

Maximum Force

Young's Modulus

Elongation

Reduction of Area

Proof Strength

Fracture Point

---

# Engineering Relationships

The following relationships shall be verified.

---

## Rule 1

Ultimate Tensile Strength

≥

Yield Strength

Violation

↓

FAIL

---

## Rule 2

Maximum Force

≥

Yield Force

Violation

↓

FAIL

---

## Rule 3

Young's Modulus

>

0

Violation

↓

FAIL

---

## Rule 4

Elongation

≥

0 %

Violation

↓

FAIL

---

## Rule 5

Reduction of Area

0 %

≤ RA ≤

100 %

Violation

↓

FAIL

---

## Rule 6

True Stress

shall exist only

after necking

when enabled.

---

## Rule 7

True Strain

shall exist only

when calculated.

---

## Rule 8

Fracture Point

shall occur

after

Yield Point

Violation

↓

FAIL

---

## Rule 9

Maximum Force

shall occur

before

or

at

Fracture

Violation

↓

WARNING

---

## Rule 10

Engineering Curve

shall terminate

at fracture.

No calculated data

shall exist

after fracture.

---

# Mathematical Consistency

Verify

Stress = Force / Area

Engineering Strain

matches extension

Offset Yield

matches selected method

Area Reduction

matches dimensions

---

# Graph Consistency

Verify

Yield Marker

Maximum Force Marker

Fracture Marker

Curve Length

Imported Point Count

---

# Warning Conditions

Large Young's Modulus deviation

Extremely high elongation

Extremely low elongation

Manual yield selection

Material reference unavailable

---

# Failure Conditions

UTS < Yield

Negative Force

Negative Stress

Negative Modulus

Missing Fracture

Missing Maximum Force

Division by Zero

---

# Validation Status

PASS

PASS WITH WARNING

FAIL

MANUAL REVIEW REQUIRED

---

# Reviewer Actions

Accept

Reject

Request Retest

Add Comment

Approve Warning

---

# SQLite Database

Tables

```
tblResultConsistency

tblConsistencyRule

tblConsistencyHistory
```

---

# Audit Trail

Store

Rule ID

Certificate Number

Revision

Measured Values

Validation Result

Reviewer

Timestamp

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Reviewer

Review

Operator

View Only

---

# Error Handling

Undefined Result

↓

FAIL

Impossible Relationship

↓

FAIL

Missing Required Result

↓

FAIL

Reference Missing

↓

WARNING

---

# Future Enhancements

Cross-Test Consistency

Batch Statistical Validation

AI Consistency Review

Automatic Outlier Detection

Reserved

---

# Acceptance Criteria

✔ Engineering relationships verified

✔ Mathematical consistency verified

✔ Graph consistency verified

✔ No engineering values modified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete validation history

---

End of Document
