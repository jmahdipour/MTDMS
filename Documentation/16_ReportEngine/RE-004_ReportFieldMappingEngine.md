# Report Field Mapping Engine

Document ID : MTDMS-RE-004

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

The Report Field Mapping Engine is responsible for transferring validated engineering information into report templates.

It creates the connection between engineering data and report placeholders.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Field Mapping Engine shall

• Map engineering data to report fields

• Prevent manual data entry

• Support multiple report templates

• Preserve engineering consistency

• Maintain complete traceability

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

Field Mapping

↓

Report

Every displayed value originates from validated engineering data.

---

# Mapping Workflow

```
Engineering Result

↓

Field Identifier

↓

Template Placeholder

↓

Report Output
```

---

# Field Categories

General Information

Customer Information

Material Information

Machine Information

Operator Information

Engineering Results

Graphs

Approval Information

Footer Information

---

# General Fields

Report Number

Certificate Number

Revision

Issue Date

Issue Time

Laboratory Name

Project

---

# Customer Fields

Customer Name

Customer Code

Project Name

Purchase Order

Sample Owner

Optional.

---

# Material Fields

Material Name

Material Grade

Material Standard

Heat Number

Batch Number

Dimensions

Cross Section

Optional.

---

# Machine Fields

Machine Name

Machine Number

Load Cell

Extensometer

Calibration Date

Software Version

Optional.

---

# Engineering Fields

Examples

Maximum Force

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

True Stress

True Strain

Compression Strength

Spring Constant

Ring Stiffness

All values are read-only.

---

# Graph Fields

Stress–Strain Graph

True Stress–Strain Graph

Force–Displacement Graph

Compression Graph

Spring Graph

Ring Stiffness Graph

The Report Engine requests graphs from the Graph Engine.

---

# Approval Fields

Prepared By

Reviewed By

Approved By

Approval Date

Approval Status

Digital Signature (future)

---

# Placeholder Format

Example

```
<<ReportNumber>>

<<CustomerName>>

<<YieldStrength>>

<<UltimateStrength>>

<<StressStrainGraph>>
```

Administrator configurable.

---

# Automatic Population

All placeholders are populated automatically.

Manual typing of engineering values inside the report is prohibited.

---

# Missing Values

If an optional value is unavailable

↓

Leave Blank

If a mandatory value is unavailable

↓

Abort Report Generation

---

# Engineering Independence

The Field Mapping Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It transfers existing values only.

---

# SQLite Interaction

SQLite stores

Field Definitions

Template Mapping

Version

Administrator Changes

Audit Information

---

# Error Handling

Unknown Placeholder

↓

Warning

Missing Mandatory Value

↓

Abort

Missing Optional Value

↓

Blank

Template Version Conflict

↓

Use Approved Version

---

# Performance Targets

Map Single Field

< 2 ms

Complete Report Mapping

< 100 ms

Template Population

< 300 ms

---

# Acceptance Criteria

✔ Automatic field mapping

✔ Read-only engineering values

✔ Multiple templates supported

✔ Placeholder validation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
