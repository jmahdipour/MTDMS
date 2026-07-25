# Report Summary Engine

Document ID : MTDMS-RE-006

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

The Report Summary Engine generates concise engineering summaries from validated test results for inclusion in reports, certificates, dashboards, and customer documentation.

The summary is generated exclusively from validated engineering values.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Summary Engine shall

• Generate engineering summaries

• Display key engineering results

• Support pass/fail evaluation

• Support customer-specific summaries

• Maintain engineering traceability

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

Summary Engine

↓

Engineering Summary

The summary is a presentation layer only.

---

# Summary Types

Engineering Summary

Executive Summary

Customer Summary

Acceptance Summary

Quality Summary

Laboratory Summary

Administrator configurable.

---

# Workflow

```
Validated Results

↓

Select Summary Template

↓

Extract Key Values

↓

Generate Summary

↓

Insert Into Report
```

---

# Engineering Values

Typical tensile summary

Maximum Force

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Fracture Position

Test Standard

Operator

Machine

Administrator configurable.

---

# Compression Summary

Maximum Load

Maximum Stress

Compression Strength

Failure Mode

Standard

Machine

Operator

---

# Spring Summary

Spring Constant

Maximum Load

Maximum Deflection

Linear Range

Acceptance

---

# Ring Stiffness Summary

Ring Stiffness

Maximum Force

Maximum Deflection

Pipe Class

Acceptance

---

# Acceptance Section

Optional

PASS

FAIL

NOT EVALUATED

The decision is based on validated engineering results and the selected acceptance profile.

---

# Customer Summary

Optional

Customer

Project

Order Number

Sample Identification

Batch

Material

Report Number

---

# Laboratory Summary

Optional

Laboratory

Machine

Operator

Calibration Status

Test Date

Software Version

---

# Summary Formatting

Supported

Table

Compact Table

Paragraph

Certificate Box

Dashboard Widget (future)

Administrator configurable.

---

# Engineering Independence

The Report Summary Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only summary presentation is generated.

---

# SQLite Interaction

SQLite stores

Summary Templates

Summary Preferences

Acceptance Profiles

Audit History

No engineering values are modified.

---

# Error Handling

Missing Result

↓

Blank

Missing Acceptance Profile

↓

Not Evaluated

Missing Template

↓

Use Default

---

# Performance Targets

Summary Generation

< 50 ms

Insert Into Report

< 100 ms

Update Summary

Immediate

---

# Acceptance Criteria

✔ Engineering summary generated

✔ Pass/Fail supported

✔ Customer summary supported

✔ Multiple layouts supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
