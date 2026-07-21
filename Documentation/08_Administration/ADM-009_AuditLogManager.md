# Audit Log Manager

Document ID : MTDMS-ADM-009

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Administration

Status

Production

---

# Purpose

The Audit Log Manager records every significant action performed within MTDMS.

The audit trail guarantees complete traceability of engineering activities, administrative actions and report generation.

Audit records are permanent.

They shall never be physically deleted.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 27001

21 CFR Part 11 (Future)

---

# Objectives

The Audit Log Manager shall

• Record every important action

• Prevent unauthorized modification

• Support investigations

• Support accreditation audits

• Maintain permanent traceability

---

# Architecture

```
User Action

↓

Audit Engine

↓

SQLite Database

↓

Audit Viewer

↓

Audit Reports
```

---

# Logged Events

System Login

Logout

Failed Login

Password Change

User Creation

User Modification

Role Assignment

Configuration Change

Material Library Change

Standard Library Change

Equipment Registration

Machine Configuration Change

Calibration Record

Engineering Calculation

Yield Point Manual Edit

Graph Correction

Report Generation

PDF Export

Certificate Approval

Certificate Rejection

Backup

Restore

Database Maintenance

Software Update

License Change

Import

Export

Archive

---

# Event Structure

Each record contains

Audit ID

Timestamp

User ID

Username

Role

Computer Name

Module

Action

Object

Old Value

New Value

Status

Reason

---

# Event Severity

Information

Warning

Error

Critical

Security

---

# Categories

Authentication

Administration

Engineering

Reporting

Calibration

Machine

Material

Database

Security

Backup

---

# Event Identification

Each event receives

Unique Audit ID

Sequential

Non-reusable

---

# Audit Viewer

The viewer supports filtering by

Date

User

Module

Action

Severity

Equipment

Sample

Certificate

---

# Search

Audit ID

User

Computer

Certificate Number

Material

Equipment

Keyword

---

# Export

Excel

CSV

PDF

Administrator configurable.

---

# Audit Reports

Login History

Engineering Changes

Manual Yield Corrections

Report Approvals

Configuration Changes

Database Operations

Security Events

Calibration Activities

---

# Data Protection

Audit records

cannot be edited.

Deletion is prohibited.

Only archival is permitted.

---

# Retention Policy

Minimum

10 Years

Administrator configurable.

---

# SQLite Database

Tables

```
tblAuditLog

tblAuditCategory

tblAuditSeverity
```

---

# Performance

Target

100,000+

audit records

without noticeable performance degradation.

---

# Permissions

Administrator

Full Access

Quality Manager

Read

Auditor

Read

Operator

No Access

---

# Error Handling

Database Locked

↓

Retry

Write Failure

↓

Critical Warning

Corrupted Record

↓

Skip

Continue Logging

---

# Future Enhancements

Digital Audit Signature

Blockchain Audit

Cloud Audit

SIEM Integration

Immutable Storage

Reserved

---

# Acceptance Criteria

✔ Complete traceability

✔ Read-only audit records

✔ Export support

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ High-performance search

✔ Long-term retention

---

End of Document
