# Automatic Report Distribution Engine

Document ID : MTDMS-RE-020

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

The Automatic Report Distribution Engine manages the controlled delivery of approved engineering reports and laboratory certificates to internal departments and external customers.

Distribution occurs only after the report has completed the approval workflow.

The engine performs **no engineering calculations**.

---

# Objectives

The Automatic Report Distribution Engine shall

• Distribute approved reports

• Support multiple delivery destinations

• Prevent distribution of unapproved reports

• Record delivery history

• Preserve engineering traceability

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

Distribution

↓

Recipient

Only approved documents may be distributed.

---

# Distribution Workflow

```
Approved Report

↓

Select Destination

↓

Generate Output

↓

Deliver

↓

Record Delivery
```

---

# Supported Destinations

Local Folder

Network Folder

Customer Folder

Archive

Email Queue

Document Management System (future)

Cloud Storage (future)

Administrator configurable.

---

# Distribution Rules

Reports with status

Draft

Rejected

Under Review

Pending Approval

shall never be distributed automatically.

Only

Approved

Issued

reports are eligible.

---

# Distribution Package

A delivery package may contain

Engineering Report

Laboratory Certificate

Engineering Graphs

Raw TXT File (optional)

CSV Export (optional)

Attachments

Administrator configurable.

---

# Automatic Naming

Distributed files retain the official report number.

Example

```
TR-2026-00125.pdf

TC-2026-00125.pdf
```

---

# Customer Profiles

Each customer may define

Preferred Language

Preferred Format

Preferred Destination

Preferred Attachments

Preferred Delivery Method

Administrator configurable.

---

# Distribution History

Each delivery records

Report Number

Recipient

Destination

Operator

Date

Time

Status

Result

---

# Delivery Status

Pending

Delivered

Failed

Cancelled

Resent

Administrator configurable.

---

# Retry Policy

Failed deliveries may be retried automatically according to administrator-defined rules.

---

# Engineering Independence

The Distribution Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Approved Reports

It distributes existing documents only.

---

# SQLite Interaction

SQLite stores

Distribution Rules

Customer Profiles

Delivery History

Retry Status

Audit Trail

---

# Error Handling

Destination Missing

↓

Retry

Access Denied

↓

Retry

Recipient Missing

↓

Reject

File Missing

↓

Abort

---

# Performance Targets

Local Distribution

< 100 ms

Network Distribution

Depends on Network

Batch Distribution

Sequential

---

# Acceptance Criteria

✔ Automatic report distribution

✔ Approval verification

✔ Delivery history

✔ Customer profiles

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
