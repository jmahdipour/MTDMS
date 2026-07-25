# Report Security Engine

Document ID : MTDMS-RE-024

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

The Report Security Engine protects engineering reports, laboratory certificates, and related documents from unauthorized modification, deletion, or distribution.

Its responsibility is document security only.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Security Engine shall

• Protect approved reports

• Prevent unauthorized modification

• Control report access

• Protect engineering integrity

• Support ISO/IEC 17025 document control

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Approved Report

↓

Security

↓

Protected Document

Security protects the document, not the engineering data.

---

# Protected Documents

Engineering Reports

Laboratory Certificates

PDF

Summary Reports

Customer Reports

Archive Files

Administrator configurable.

---

# Workflow

```
Approved Report

↓

Security Policy

↓

Apply Protection

↓

Store

↓

Distribute
```

---

# Security Levels

Public

Internal

Confidential

Restricted

Administrator configurable.

---

# Access Rights

View

Print

Export

Copy

Modify

Delete

Administrator configurable.

---

# User Roles

Operator

Reviewer

Approver

Quality Manager

Administrator

Each role has configurable permissions.

---

# Protected Actions

Modification

Deletion

Revision

Distribution

Export

Archive Removal

Administrator configurable.

---

# Read-Only Mode

Issued reports become

Read Only

unless a formal revision process is initiated.

---

# PDF Security

Supported

Read Only

Password Protected (optional)

Print Allowed

Copy Disabled

Future Digital Signature

Administrator configurable.

---

# Audit

Every security-related event is recorded.

Examples

Report Opened

Report Printed

Report Exported

Permission Denied

Administrator Override

---

# Engineering Independence

The Report Security Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Security affects document access only.

---

# SQLite Interaction

SQLite stores

Security Profiles

User Permissions

Security Events

Audit Trail

Access History

---

# Error Handling

Permission Denied

↓

Reject

Unauthorized Modification

↓

Reject

Missing Security Profile

↓

Use Default

Database Failure

↓

Abort

---

# Performance Targets

Permission Check

< 5 ms

Open Protected Report

< 100 ms

Audit Logging

< 10 ms

---

# Acceptance Criteria

✔ Report protection

✔ Role-based permissions

✔ Read-only issued reports

✔ Security audit

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
