# Pass / Fail Evaluation Engine

Document ID : MTDMS-RE-007

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Pass / Fail Evaluation Engine determines whether a tested specimen complies with the selected engineering specification.

The engine compares validated engineering results with acceptance limits defined by standards, customer specifications, or laboratory acceptance profiles.

The engine does **not** calculate engineering values.

---

# Objectives

The Pass / Fail Evaluation Engine shall

• Compare engineering results with limits

• Generate pass/fail decisions

• Support multiple specifications

• Preserve engineering traceability

• Support laboratory accreditation

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Calculation Engine

↓

Validated Results

↓

Acceptance Profile

↓

Pass / Fail

The decision is based exclusively on validated engineering values.

---

# Supported Decision Sources

Material Library

Customer Specification

National Standard

International Standard

Project Requirement

Laboratory Specification

Administrator configurable.

---

# Workflow

```
Validated Results

↓

Acceptance Profile

↓

Limit Comparison

↓

Decision

↓

Report
```

---

# Supported Test Types

Tensile

Compression

Spring

Ring Stiffness

Three-Point Bending

Four-Point Bending

Administrator configurable.

---

# Typical Tensile Evaluation

Compare

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Fracture Behaviour (optional)

---

# Compression Evaluation

Maximum Stress

Maximum Load

Failure Mode

Administrator configurable.

---

# Spring Evaluation

Spring Constant

Maximum Force

Maximum Deflection

Linear Range

---

# Ring Stiffness Evaluation

Ring Stiffness

Maximum Force

Specified Deflection

Pipe Class

---

# Decision States

PASS

FAIL

NOT EVALUATED

INSUFFICIENT DATA

INVALID TEST

Administrator configurable.

---

# Tolerance Handling

Supported

Minimum Limit

Maximum Limit

Nominal ± Tolerance

Percentage Tolerance

Administrator configurable.

---

# Multiple Criteria

A specimen may require

all criteria

or

selected criteria

to pass.

Decision rules are configurable.

---

# Decision Explanation

The report may include

Reason for Failure

Exceeded Limit

Below Minimum

Missing Data

Invalid Result

Optional.

---

# Engineering Independence

The Pass / Fail Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It evaluates existing engineering values only.

---

# SQLite Interaction

SQLite stores

Acceptance Profiles

Decision History

Decision Rules

Operator

Timestamp

Audit Information

---

# Error Handling

Missing Acceptance Profile

↓

Not Evaluated

Missing Engineering Value

↓

Insufficient Data

Conflicting Limits

↓

Reject

---

# Performance Targets

Single Evaluation

< 10 ms

Complete Report Evaluation

< 100 ms

Batch Evaluation

< 1 s

---

# Acceptance Criteria

✔ Automatic pass/fail evaluation

✔ Multiple specifications supported

✔ Multiple tolerance methods

✔ Decision explanation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
