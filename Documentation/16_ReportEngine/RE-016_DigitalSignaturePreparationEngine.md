# Digital Signature Preparation Engine

Document ID : MTDMS-RE-016

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

Future Ready

---

# Purpose

The Digital Signature Preparation Engine prepares the report architecture for future implementation of electronic signatures and digital certificate authentication.

In the current version of MTDMS, electronic signatures are **not** applied automatically.

The architecture is designed so that future digital signature support can be added without changing report generation, report templates, or engineering calculations.

---

# Objectives

The Digital Signature Preparation Engine shall

• Prepare report signature locations

• Prepare digital certificate integration

• Preserve document integrity

• Support ISO/IEC 17025 document control

• Support future electronic approval

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Engineering Report

↓

Approval

↓

Digital Signature (Future)

Engineering values remain independent of signatures.

---

# Current Status

Current Version

Manual Approval

Future Version

Electronic Signature

Digital Certificate

Timestamp

Signature Validation

---

# Workflow

```
Approved Report

↓

Signature Placeholder

↓

PDF Generation

↓

Future Signature

↓

Issued Document
```

---

# Signature Locations

Prepared By

Reviewed By

Approved By

Quality Manager

Laboratory Manager

Administrator configurable.

---

# Signature Metadata

Reserved fields

Signer Name

Signer ID

Role

Certificate ID

Signature Timestamp

Verification Status

---

# Signature Types

Future support

Image Signature

Digital Certificate

PKI

Smart Card

USB Token

Administrator configurable.

---

# Signature Validation

Future support

Certificate Valid

Certificate Expired

Certificate Revoked

Signature Verified

Signature Invalid

---

# PDF Compatibility

The report structure shall reserve sufficient space for future PDF digital signatures.

No redesign shall be required.

---

# Revision Interaction

Every signed revision remains independent.

Signing a new revision shall never modify previous signed reports.

---

# Engineering Independence

The Digital Signature Preparation Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Reports

Only signature placeholders are prepared.

---

# SQLite Interaction

SQLite stores

Signature Placeholder

Future Certificate ID

Approval Information

Timestamp

Audit Information

No certificate data are currently stored.

---

# Error Handling

Signature Not Available

↓

Continue Manual Approval

Certificate Missing

↓

Future Implementation

Verification Failure

↓

Future Implementation

---

# Performance Targets

Placeholder Creation

Immediate

Metadata Storage

< 10 ms

---

# Acceptance Criteria

✔ Future-ready architecture

✔ Signature placeholders prepared

✔ PDF compatibility

✔ Revision compatibility

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 ready

✔ No redesign required for future digital signatures

---

End of Document
