# Engineering Report Data Preparation Engine

Document ID : MTDMS-CE-017

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File

Application

MTDMS

Status

Production

---

# Purpose

The Engineering Report Data Preparation Engine collects validated engineering results from the Calculation Engine and prepares them for insertion into Excel report templates.

This engine performs **no engineering calculations**.

It organizes validated information for reporting.

---

# Objectives

The Report Data Preparation Engine shall

• Collect validated engineering results

• Format report data

• Prepare graph references

• Prepare certificate values

• Supply report templates

---

# Engineering Philosophy

TXT File

↓

Engineering Calculation

↓

Validation

↓

Report Data Preparation

↓

Excel Report

Only validated engineering values may be prepared for reporting.

---

# Data Sources

Engineering Results

Validation Results

Material Library

Customer Library

Machine Library

Operator Library

Application Settings

Graph Metadata

Certificate Information

---

# Workflow

```
Engineering Results

↓

Validation Check

↓

Collect Report Fields

↓

Apply Formatting Rules

↓

Prepare Graph References

↓

Prepare Report Dataset

↓

Excel Report Engine
```

---

# Prepared Information

Report Number

Certificate Number

Customer Information

Material Information

Machine Information

Operator Information

Test Date

Test Time

Standard

Engineering Results

Validation Status

Graph References

Approval Information

---

# Engineering Results Included

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Maximum Force

Maximum Stress

Maximum Strain

Spring Constant

Ring Stiffness

Compression Strength

Flexural Strength

Only results applicable to the selected test type are included.

---

# Graph References

The engine prepares

Graph Style

Graph Metadata

Graph Marker Positions

Graph Image Reference

The actual graph is inserted later by the Report Engine.

---

# Number Formatting

Engineering values remain numeric.

Formatting

Decimal Places

Units

Thousands Separator

Scientific Notation

is applied according to the selected report template.

---

# Missing Data

If optional values are unavailable

↓

Leave Blank

If mandatory values are unavailable

↓

Report Generation Prohibited

---

# Engineering Independence

The Report Data Preparation Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It prepares copies only.

---

# SQLite Interaction

SQLite stores

Prepared Report Metadata

Report History

Certificate History

Audit Information

Prepared datasets are regenerated whenever the report is recreated.

---

# Error Handling

Validation Failed

↓

Abort Report

Missing Mandatory Field

↓

Abort

Missing Optional Field

↓

Blank Field

Missing Graph

↓

Report without Graph (configurable)

---

# Performance Targets

Typical Report Dataset

< 200 ms

Graph Reference Preparation

< 50 ms

Complete Dataset

< 300 ms

---

# Acceptance Criteria

✔ Validated engineering results collected

✔ Report fields prepared

✔ Graph references prepared

✔ Numeric formatting preserved

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete reproducibility from TXT

---

End of Document
