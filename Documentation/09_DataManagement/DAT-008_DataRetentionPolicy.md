# Data Retention Policy

Document ID : MTDMS-DAT-008

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Data Management

Status

Production

---

# Purpose

The Data Retention Policy defines how long every category of information shall be retained inside MTDMS.

The objective is to preserve engineering traceability while preventing accidental loss of laboratory records.

This module defines retention policies only.

It never modifies engineering calculations.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 15489

Customer Contract Requirements

Applicable National Regulations

---

# Objectives

The Retention Policy shall

• Define retention periods

• Prevent unauthorized deletion

• Preserve traceability

• Support laboratory audits

• Support legal compliance

• Define archive lifecycle

---

# Data Categories

Original Machine Files

Imported Data

Normalized Data

Engineering Results

Reports

PDF Reports

Graphs

Material Library

Standard Library

Calibration Records

Audit Logs

System Configuration

Backup Files

User Records

---

# Default Retention Period

| Data Category | Minimum Retention |
|---------------|------------------|
| Original Test Files | 10 Years |
| Engineering Results | Permanent (Recommended) |
| Reports | 10 Years |
| PDF Certificates | 10 Years |
| Calibration Records | According to laboratory policy |
| Audit Logs | 10 Years |
| Material Library | Permanent |
| Standard Library | Permanent |
| Configuration | Permanent |
| Backup Files | Administrator Configurable |

---

# Archive Lifecycle

```
Imported

↓

Processed

↓

Approved

↓

Archived

↓

Inactive

↓

Retained

↓

Logical Disposal
```

Physical deletion is not supported.

---

# Logical Disposal

Records marked as

Disposed

remain inside the database.

Their status changes only.

No engineering information is removed.

---

# Retention Rules

Engineering records

shall never expire automatically.

Only administrators may change retention policies.

Changes are fully audited.

---

# Storage Classes

Active Data

Frequently accessed

↓

Archive Data

Occasionally accessed

↓

Historical Data

Rarely accessed

---

# Protected Records

The following records cannot be removed

Approved Reports

Approved Engineering Results

Calibration History

Audit Logs

Material Revisions

Standard Revisions

---

# Review Cycle

Retention policies shall be reviewed

Annually

or

Whenever regulations change.

---

# Database

SQLite

Tables

```
tblRetentionPolicy

tblRetentionCategory

tblRetentionHistory
```

---

# Audit Trail

Every policy modification records

User

Timestamp

Old Value

New Value

Reason

Computer Name

---

# Permissions

Administrator

Modify Policy

Quality Manager

Review

Operator

Read Only

---

# Error Handling

Unknown Category

↓

Reject

Invalid Retention Period

↓

Reject

Protected Record

↓

Deletion Denied

---

# Future Enhancements

Automatic Archive Migration

Cloud Cold Storage

Regulatory Profiles

Customer-specific Retention Rules

Reserved

---

# Acceptance Criteria

✔ ISO/IEC 17025 compliant

✔ Logical disposal only

✔ Permanent engineering traceability

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Complete audit trail

---

End of Document
