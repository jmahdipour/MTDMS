# Certificate Generation Engine

Document ID : MTDMS-RE-008

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

The Certificate Generation Engine creates formal laboratory certificates from validated engineering results obtained from the imported TXT file.

Certificates are official laboratory documents and must comply with ISO/IEC 17025 reporting requirements.

The engine performs **no engineering calculations**.

---

# Objectives

The Certificate Generation Engine shall

• Generate official certificates

• Use validated engineering data only

• Support laboratory accreditation

• Support customer requirements

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

Certificate Engine

↓

Official Certificate

Certificates are generated only after engineering validation.

---

# Supported Certificates

Tensile Test Certificate

Compression Test Certificate

Spring Test Certificate

Ring Stiffness Certificate

Three-Point Bending Certificate

Four-Point Bending Certificate

Administrator configurable.

---

# Certificate Workflow

```
Validated Engineering Results

↓

Certificate Template

↓

Populate Fields

↓

Insert Graph

↓

Approval

↓

Certificate
```

---

# Certificate Header

Laboratory Name

Accreditation Number

Certificate Number

Revision

Issue Date

Logo

Address

Contact Information

Administrator configurable.

---

# Customer Information

Customer Name

Project

Purchase Order

Sample Identification

Material

Batch

Heat Number

Optional.

---

# Test Information

Test Standard

Machine

Load Cell

Extensometer

Operator

Test Date

Environmental Conditions

Optional.

---

# Engineering Results

Only validated engineering values may appear.

Typical tensile certificate

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Elongation

Maximum Force

Reduction of Area

True Stress

True Strain

Administrator configurable.

---

# Engineering Graph

Optional

Stress–Strain

Force–Displacement

Compression Curve

Spring Curve

Ring Stiffness Curve

Comparison Graph

The graph is regenerated from validated engineering data.

---

# Compliance Statement

Optional

The certificate may include statements such as

"The test was performed in accordance with the selected standard."

"The reported values originate from validated engineering calculations."

"The results apply only to the tested specimen."

Administrator configurable.

---

# Approval Section

Prepared By

Reviewed By

Authorized By

Approval Date

Electronic Signature (future)

---

# Certificate Number

Each certificate receives a unique identifier.

Example

```
TC-2026-000153
```

Numbering rules are administrator configurable.

---

# Engineering Independence

The Certificate Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Certificates are generated from existing validated information only.

---

# SQLite Interaction

SQLite stores

Certificate Metadata

Certificate Number

Revision

Approval Status

Issue Date

Operator

Audit History

Certificate files remain external documents.

---

# Error Handling

Missing Template

↓

Abort

Missing Approval

↓

Draft Certificate

Missing Engineering Result

↓

Abort

Duplicate Certificate Number

↓

Generate New Number

---

# Performance Targets

Generate Certificate

< 2 s

Insert Graph

< 300 ms

Generate PDF

< 5 s

---

# Acceptance Criteria

✔ Official laboratory certificate generated

✔ Validated engineering data only

✔ Automatic certificate numbering

✔ Approval workflow supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
