# Standard Compliance Validation

Document ID : MTDMS-VAL-006

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

The Standard Compliance Validation module verifies that every engineering result required by the selected test standard has been calculated, validated and reported.

This module validates compliance with the selected testing standard.

It does not perform engineering calculations.

It does not determine PASS or FAIL according to product specifications.

Product acceptance is handled separately by the Acceptance Engine.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ASTM E8/E8M

ASTM E111

ASTM A370

ISO 6508

ISO 6506

ISO 6507

ISO 148

ISO 178

ISO 527

ASTM D638

ASTM D790

Administrator configurable.

---

# Objectives

The module shall

• Verify mandatory engineering results

• Verify mandatory metadata

• Verify mandatory units

• Verify mandatory report fields

• Verify test completeness

• Prevent incomplete reports

---

# Validation Workflow

Selected Standard

↓

Load Standard Requirements

↓

Compare Engineering Results

↓

Compare Metadata

↓

Compare Report

↓

Compliance Status

---

# Compliance Levels

Complete

Complete With Warning

Incomplete

Unknown Standard

Custom Standard

---

# Standard Definition

Each standard contains

Standard ID

Revision

Mandatory Results

Optional Results

Required Units

Required Report Fields

Applicable Material Types

Applicable Test Types

---

# Mandatory Engineering Results

Examples

ISO 6892-1

Yield Strength

Ultimate Tensile Strength

Elongation

Maximum Force

Initial Cross Section

Gauge Length

Stress-Strain Curve

Fracture Point

Young's Modulus
(if requested)

---

# Mandatory Metadata

Verify

Material

Standard

Specimen Type

Operator

Date

Certificate Number

Machine

Sample ID

---

# Unit Compliance

Verify

Force

Stress

Length

Time

Temperature

Displayed units shall match the selected report configuration.

Internal calculations remain unchanged.

---

# Test Completeness

Verify

Imported Data Exists

Engineering Results Exist

Graph Exists

Report Exists

Approval Block Exists

Archive Reference Exists

---

# Unsupported Standard

If selected standard

does not exist

↓

Compliance Status

UNKNOWN

Engineering calculations remain available.

---

# Custom Standards

Laboratory-defined standards

are supported.

Each custom standard shall contain

Unique ID

Revision

Validation Rules

Mandatory Fields

---

# Compliance Results

PASS

PASS WITH WARNING

FAIL

NOT APPLICABLE

UNKNOWN STANDARD

---

# Warning Examples

Optional Result Missing

Optional Graph Missing

Optional Metadata Missing

---

# Failure Examples

Mandatory Result Missing

Mandatory Metadata Missing

Mandatory Unit Missing

Required Graph Missing

Required Section Missing

---

# SQLite Database

Tables

```
tblStandardRequirement

tblComplianceValidation

tblComplianceHistory

tblCustomStandard
```

---

# Audit Trail

Every compliance verification records

Validation ID

Standard

Revision

Certificate Number

Timestamp

Operator

Reviewer

Compliance Result

---

# Permissions

Administrator

Full Access

Quality Manager

Approve

Reviewer

Review

Operator

Read Only

---

# Error Handling

Unknown Standard

↓

Warning

Missing Requirement

↓

FAIL

Corrupted Standard Definition

↓

Reject Validation

Missing Revision

↓

Warning

---

# Future Enhancements

Automatic Standard Revision Detection

Cross-Standard Comparison

AI Standard Compliance Review

National Standard Packages

Reserved

---

# Acceptance Criteria

✔ Standard requirements verified

✔ Mandatory fields verified

✔ Mandatory engineering results verified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete compliance history

---

End of Document
