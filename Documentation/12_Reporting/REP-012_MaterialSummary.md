# Material Summary

Document ID : MTDMS-REP-012

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

The Material Summary module generates a concise summary of the tested material and its validated engineering properties.

This section provides a quick overview for the customer without replacing the complete engineering report.

The module presents validated results only.

No engineering calculations are performed.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ISO 630

ISO 898

INSO 3132

Customer Specifications

Laboratory Procedures

---

# Objectives

The module shall

• Summarize tested material

• Summarize key engineering properties

• Present validated values only

• Support multiple material families

• Support configurable report layouts

---

# Workflow

```
Validated Engineering Results

↓

Material Information

↓

Material Summary

↓

Report Engine
```

---

# Material Information

Displays

Material Grade

Material Name

Material Family

Heat Number

Batch Number

Specification

Applicable Standard

Heat Treatment

Product Form

Manufacturer
(Optional)

---

# Product Forms

Plate

Sheet

Bar

Round Bar

Pipe

Tube

Wire

Spring

Casting

Forging

Extrusion

Custom

---

# Heat Treatment

If available

Displays

Annealed

Normalized

Quenched

Tempered

Solution Treated

Aged

Unknown

---

# Mechanical Summary

Displays

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Reduction of Area

Maximum Force

Proof Strength
(if applicable)

---

# Hardness Summary

If available

Displays

Hardness Value

Scale

Load

Holding Time

Standard

---

# Impact Summary

If available

Displays

Impact Energy

Test Temperature

Specimen Size

Orientation

Standard

---

# Chemical Summary

If available

Displays

Major alloying elements only.

Default

C

Si

Mn

Cr

Ni

Mo

V

Cu

P

S

Administrator configurable.

---

# Ring Stiffness Summary

If applicable

Displays

Ring Stiffness

Instantaneous Stiffness

Load

Displacement

---

# Spring Summary

If applicable

Displays

Spring Constant

Maximum Load

Deflection

Permanent Set

---

# Bending Summary

If applicable

Displays

Maximum Load

Maximum Stress

Deflection

Flexural Modulus
(if available)

---

# Summary Rules

Only validated engineering results

shall appear.

Unavailable properties

shall not be estimated.

Missing properties

display

—

---

# Layout

Default

Two-column layout

Administrator configurable.

---

# Multilingual Support

Supported

Persian

English

Arabic

Other configured languages

Engineering symbols remain unchanged.

---

# Example

| Property | Value | Unit |
|----------|------:|------|
| Material | S355JR | — |
| Standard | ISO 630 | — |
| Yield Strength | 355 | MPa |
| Ultimate Strength | 510 | MPa |
| Young's Modulus | 210 | GPa |
| Elongation | 24 | % |

---

# SQLite Database

Tables

```
tblMaterialSummary

tblMaterialSummaryLayout

tblMaterialSummaryHistory
```

---

# Audit Trail

Record

Certificate Number

Revision

Material

Template

Operator

Timestamp

Software Version

---

# Permissions

Administrator

Modify Layout

Quality Manager

Approve

Reviewer

Generate

Operator

Generate

---

# Error Handling

Missing Material

↓

Display Unknown

Missing Property

↓

Display —

Unknown Grade

↓

Warning

Database Failure

↓

Abort

---

# Future Enhancements

Automatic Material Datasheet

Microstructure Summary

Heat Treatment Diagram

Material Comparison

Reserved

---

# Acceptance Criteria

✔ Material information summarized

✔ Only validated engineering values shown

✔ No calculated values modified

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
