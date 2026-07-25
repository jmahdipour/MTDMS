# Engineering Test Report Engine

Document ID : MTDMS-RE-003

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

The Engineering Test Report Engine generates the primary laboratory report for every mechanical test performed within MTDMS.

The report is produced exclusively from validated engineering data reconstructed from the original machine TXT file.

The engine performs **no engineering calculations**.

---

# Objectives

The Engineering Test Report Engine shall

• Generate standardized laboratory reports

• Present validated engineering results

• Include engineering graphs

• Support laboratory approval workflow

• Maintain complete traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Calculation Engine

↓

Validation

↓

Engineering Test Report

Reports never use manually typed engineering values.

---

# Supported Tests

Tensile Test

Compression Test

Three-Point Bending

Four-Point Bending

Spring Test

Ring Stiffness Test

Administrator configurable.

---

# Report Structure

Cover Information

Sample Information

Material Information

Machine Information

Test Conditions

Engineering Results

Engineering Graph

Summary

Approval

Footer

---

# Sample Information

Report Number

Sample ID

Sample Description

Material Grade

Heat Number

Batch Number

Dimensions

Cross Section

Optional.

---

# Machine Information

Machine Name

Machine Serial Number

Load Cell

Extensometer

Calibration Status

Software Version

Optional.

---

# Test Conditions

Test Standard

Test Speed

Environment

Temperature

Humidity (optional)

Operator

Date

Time

---

# Engineering Results

Typical tensile report fields

Maximum Force

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

True Stress

True Strain

Fracture Location

Displayed values are imported directly from validated engineering results.

---

# Engineering Graph

Supported

Stress–Strain

True Stress–Strain

Force–Displacement

Compression Curve

Spring Curve

Ring Stiffness Curve

The graph is regenerated from validated engineering data.

---

# Pass / Fail

Optional

The report may automatically compare engineering results with

Material Library

Customer Specification

Selected Standard

Acceptance Profile

Administrator configurable.

---

# Remarks

Optional

Operator Remarks

Laboratory Remarks

Customer Remarks

Engineering Notes

Administrator configurable.

---

# Approval

Prepared By

Reviewed By

Approved By

Approval Date

Digital Signature (future)

---

# Report Identification

Each report receives

Unique Report Number

Unique Revision

Unique Timestamp

Unique Database ID

Traceable to the original TXT file.

---

# Engineering Independence

The Engineering Test Report Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

It presents validated information only.

---

# SQLite Interaction

SQLite stores

Report Metadata

Revision

Approval Status

Print History

Audit Trail

The report document itself remains an external Excel/PDF file.

---

# Error Handling

Missing Engineering Result

↓

Abort

Missing Graph

↓

Generate Without Graph (configurable)

Missing Template

↓

Use Default

Approval Missing

↓

Draft Report

---

# Performance Targets

Generate Report

< 1 s

Insert Graph

< 300 ms

Generate PDF

< 5 s

---

# Acceptance Criteria

✔ Standardized engineering report

✔ Validated engineering values

✔ Engineering graph included

✔ Approval workflow

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
