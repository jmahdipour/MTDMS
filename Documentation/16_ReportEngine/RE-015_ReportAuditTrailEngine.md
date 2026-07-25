# Report Audit Trail Engine

Document ID : MTDMS-RE-015

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

The Report Audit Trail Engine records every significant event related to engineering reports and laboratory certificates throughout their entire lifecycle.

Its primary function is to ensure complete traceability, accountability, and compliance with ISO/IEC 17025 quality management requirements.

The engine performs **no engineering calculations**.

---

# Objectives

The Report Audit Trail Engine shall

• Record report lifecycle events

• Preserve document history

• Record operator actions

• Support accreditation audits

• Ensure complete traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Engineering Report

↓

Audit Trail

↓

Permanent Record

Every report action shall be permanently traceable.

---

# Audited Events

Report Created

Report Modified

Report Approved

Report Rejected

Report Printed

Report Exported

PDF Generated

Certificate Generated

Revision Created

Report Archived

Report Retrieved

Report Deleted (if permitted)

Administrator configurable.

---

# Audit Workflow

```
User Action

↓

Audit Record

↓

SQLite

↓

Permanent History
```

---

# Audit Information

Each record stores

Audit ID

Timestamp

Operator

Computer

Action

Report Number

Certificate Number

Revision

Status

Reason

Comments

---

# Operator Information

Operator Name

Operator ID

Role

Department (optional)

Login Session

---

# Report Information

Report Number

Revision

Template

Document Type

Project

Customer

Material

Test Type

---

# Status History

Example

Draft

↓

Reviewed

↓

Approved

↓

Issued

↓

Archived

Every transition is permanently recorded.

---

# Change Tracking

The engine records

Previous Status

Current Status

Operator

Date

Time

Reason

---

# Audit Protection

Audit records

cannot be modified

cannot be deleted

cannot be overwritten

except by database recovery procedures.

---

# Search

Supported

Audit ID

Operator

Date

Report Number

Customer

Material

Action

Revision

Status

---

# Export

Audit records may be exported as

Excel

CSV

PDF

Administrator configurable.

---

# Engineering Independence

The Report Audit Trail Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Reports

Certificates

It records actions only.

---

# SQLite Interaction

SQLite stores

Complete Audit Trail

User History

Report History

Revision History

Approval History

Export History

Print History

---

# Error Handling

Audit Database Failure

↓

Retry

Operator Unknown

↓

Reject Login

Invalid Action

↓

Reject

Database Locked

↓

Retry

---

# Performance Targets

Record Audit Event

< 10 ms

Search Audit

< 200 ms

Export Audit

< 1 s

---

# Acceptance Criteria

✔ Complete audit history

✔ Immutable audit records

✔ Search supported

✔ Export supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file to final report

---

End of Document
