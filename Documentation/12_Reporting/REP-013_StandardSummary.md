# Standard Summary

Document ID : MTDMS-REP-013

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Reporting

Status

Production

---

# Purpose

The Standard Summary module displays a concise summary of the applicable test standard together with the engineering properties required by that standard.

This section helps the reader understand

• which standard governed the test,
• which engineering properties were required,
• and which results are reported.

The module does not evaluate compliance.

Compliance evaluation is performed by the Validation module.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ISO 630

ISO 898

INSO 3132

ASTM E8/E8M

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

• Display the governing standard

• Display the standard revision

• Display mandatory reported properties

• Display optional reported properties

• Preserve traceability

---

# Workflow

```
Selected Standard

↓

Standard Library

↓

Standard Summary

↓

Report Engine
```

---

# Standard Information

Displays

Standard Number

Standard Title

Revision

Publication Year

Test Method

Material Scope

---

# Example

Standard

ISO 6892-1

Revision

2019

Method

Method A

---

# Test Scope

Displays

Metallic Materials

Plastic Materials

Spring Testing

Impact Testing

Hardness Testing

Chemical Analysis

Administrator configurable.

---

# Mandatory Properties

The module lists only the engineering properties required by the selected standard.

Example

ISO 6892-1

Yield Strength

Ultimate Tensile Strength

Maximum Force

Elongation

Original Cross Section

Gauge Length

Stress-Strain Graph

---

# Optional Properties

Example

Young's Modulus

True Stress

True Strain

Reduction of Area

Energy

Customer Requirement

Administrator configurable.

---

# Standard Notes

Displays

Important remarks defined by the laboratory.

Examples

Test performed according to Method A.

Proof strength determined by Rp0.2.

Gauge length measured before testing.

---

# Laboratory Notes

Optional

Internal laboratory procedures

Customer-specific notes

Project-specific notes

---

# Standard Revision

Every report stores

Standard Number

Revision

Library Version

Revision Date

---

# Display Format

Example

| Standard | Revision | Method |
|-----------|----------|--------|
| ISO 6892-1 | 2019 | A |

---

# Engineering Independence

Changing the selected report template

shall not change

Standard

Revision

Engineering Results

Traceability

---

# Unsupported Standards

If a standard is not found

↓

Display

UNKNOWN STANDARD

Engineering report generation continues.

---

# Custom Standards

Supported

Each custom standard contains

Standard ID

Revision

Description

Required Properties

Report Notes

---

# SQLite Database

Tables

```
tblStandard

tblStandardRevision

tblStandardSummary

tblStandardHistory
```

---

# Audit Trail

Record

Standard

Revision

Certificate Number

Operator

Timestamp

Software Version

---

# Permissions

Administrator

Manage Standards

Quality Manager

Approve

Reviewer

Generate

Operator

Read Only

---

# Error Handling

Missing Standard

↓

UNKNOWN STANDARD

Missing Revision

↓

Warning

Corrupted Library

↓

Abort

Missing Required Property

↓

Warning

---

# Future Enhancements

Automatic Standard Updates

Customer Standard Packages

Cross-Reference Standards

Online Standards Repository

Reserved

---

# Acceptance Criteria

✔ Standard displayed

✔ Revision displayed

✔ Required properties listed

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
