# Report Number Manager

Document ID : MTDMS-REP-015

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

The Report Number Manager generates and manages the unique report numbers used for all engineering reports issued by MTDMS.

Every report shall have one unique report number.

Report numbers shall never be duplicated.

Assigned report numbers shall never be reused.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 15489

Laboratory Document Control Procedures

---

# Objectives

The module shall

• Generate unique report numbers

• Prevent duplication

• Maintain sequential numbering

• Support yearly numbering

• Support configurable numbering rules

• Maintain complete traceability

---

# Workflow

```
Generate Report

↓

Request Report Number

↓

Report Number Manager

↓

Uniqueness Verification

↓

Assign Number

↓

Lock Number

↓

Report Engine
```

---

# Numbering Principles

Each report number shall be

Unique

Permanent

Traceable

Sequential

Read-only after release

---

# Default Format

```
YYYY-XXXXX
```

Example

```
2026-00001
2026-00002
2026-00003
```

Administrator configurable.

---

# Alternative Formats

Examples

```
LAB-2026-00001

MTDMS-2026-00001

T-2026-00001

LAB01-2026-00001
```

Configured by laboratory policy.

---

# Reset Rules

Supported

Never Reset

Yearly Reset

Monthly Reset

Custom

Default

Yearly Reset

---

# Number Reservation

Report numbers are reserved

before

report generation.

Unused reserved numbers remain recorded.

They are never reassigned.

---

# Duplicate Protection

Before assignment

Verify

Number Exists

↓

Yes

Generate Next Number

↓

No

Assign Number

---

# Deleted Reports

Deleted reports

do not free

their report numbers.

The numbering sequence remains continuous.

---

# Archived Reports

Archived reports retain

their original report numbers permanently.

---

# Manual Number Entry

Not permitted

by default.

Optional

Administrator Override

with full audit trail.

---

# Report Number Components

Optional fields

Laboratory Code

Department

Test Type

Year

Sequence Number

Customer Prefix

Administrator configurable.

---

# SQLite Database

Tables

```
tblReportNumber

tblReportSequence

tblReportNumberHistory
```

---

# Audit Trail

Every assignment records

Report Number

Operator

Timestamp

Computer Name

Software Version

Sequence Value

Status

---

# Permissions

Administrator

Configure

Override

Quality Manager

Generate

Reviewer

Read

Operator

Automatic Only

---

# Error Handling

Database Locked

↓

Retry

Duplicate Found

↓

Generate Next

Sequence Corrupted

↓

Abort

Missing Configuration

↓

Use Default Format

---

# Future Enhancements

Department-specific Numbering

Customer-specific Numbering

Cloud Synchronization

Distributed Number Server

Reserved

---

# Acceptance Criteria

✔ Unique report numbers

✔ Duplicate prevention

✔ Permanent numbering

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
