# Acceptance Criteria Validation

Document ID : MTDMS-VAL-009

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

The Acceptance Criteria Validation module evaluates engineering results against the acceptance limits defined by the selected specification, standard, customer requirement or internal laboratory procedure.

This module determines only whether measured values satisfy the selected acceptance criteria.

It never changes measured values.

It never recalculates engineering properties.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ISO 630

ISO 898

INSO 3132

Customer Specifications

Project Specifications

Laboratory Procedures

---

# Objectives

The module shall

• Compare engineering results with specification limits

• Produce objective PASS / FAIL decisions

• Support multiple acceptance profiles

• Maintain complete traceability

• Prevent subjective evaluation

---

# Validation Workflow

```
Validated Engineering Results

↓

Acceptance Profile

↓

Comparison Engine

↓

Decision

↓

PASS

FAIL

NOT EVALUATED

↓

Report
```

---

# Acceptance Sources

Customer Specification

National Standard

International Standard

Internal Laboratory Specification

Project Specification

Administrator Defined Specification

---

# Acceptance Profile

Each profile contains

Profile ID

Profile Name

Revision

Standard

Material

Required Properties

Minimum Limits

Maximum Limits

Applicable Test Type

---

# Engineering Properties

Supported

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Hardness

Impact Energy

Ring Stiffness

Spring Constant

Bending Strength

Future Properties

---

# Limit Types

Minimum

Maximum

Range

Exact Value

Not Applicable

---

# Decision Logic

Measured Value

↓

Acceptance Limit

↓

PASS

or

FAIL

---

# Multiple Criteria

Example

Yield Strength

PASS

Ultimate Strength

PASS

Elongation

FAIL

↓

Overall Result

FAIL

---

# Undefined Criteria

If

Acceptance Limit

does not exist

↓

Result

NOT EVALUATED

No automatic PASS is allowed.

---

# Manual Override

Not permitted.

Acceptance decisions are generated automatically.

Only authorized reviewers may

Invalidate

or

Repeat Test.

---

# Acceptance Result

PASS

FAIL

NOT EVALUATED

RETEST REQUIRED

---

# Color Convention

PASS

Green

FAIL

Red

Warning

Yellow

Not Evaluated

Gray

Colors are configurable.

---

# Result Table

Each evaluated property records

Property

Measured Value

Required Value

Tolerance

Status

Comment

---

# Report Integration

The report shall contain

Acceptance Profile

Revision

Decision Table

Overall Decision

Reviewer

Approval Date

---

# SQLite Database

Tables

```
tblAcceptanceProfile

tblAcceptanceRule

tblAcceptanceResult

tblAcceptanceHistory
```

---

# Audit Trail

Store

Acceptance Profile

Revision

Property

Measured Value

Limit

Decision

Reviewer

Timestamp

---

# Permissions

Administrator

Manage Profiles

Quality Manager

Approve

Reviewer

Review

Operator

Read Only

---

# Error Handling

Missing Acceptance Profile

↓

NOT EVALUATED

Invalid Limit

↓

FAIL

Undefined Property

↓

Ignore

Database Error

↓

Abort Validation

---

# Future Enhancements

Customer-specific Rule Packages

Multi-level Acceptance

Statistical Batch Acceptance

AI Recommendation

Reserved

---

# Acceptance Criteria

✔ Automatic PASS / FAIL

✔ Multiple acceptance profiles

✔ No engineering values modified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
