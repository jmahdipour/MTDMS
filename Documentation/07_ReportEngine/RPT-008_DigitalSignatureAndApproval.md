# Digital Signature and Approval System

Document ID : MTDMS-RPT-008

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Report Engine

Status

Production

---

# Purpose

This document defines the Digital Signature and Approval System used by MTDMS.

The system guarantees that every released report has been reviewed, approved and protected against unauthorized modification.

The approval process fulfills the documentation and traceability requirements of

ISO/IEC 17025.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

21 CFR Part 11 (Future)

ISO 27001 (Recommended)

---

# Approval Workflow

```
Engineering Results

↓

Review

↓

Verification

↓

Approval

↓

Digital Signature

↓

Certificate Lock

↓

PDF

↓

Archive
```

---

# Approval Levels

Level 1

Operator

↓

Level 2

Reviewer

↓

Level 3

Laboratory Manager

Administrator configurable.

---

# Operator Responsibilities

Verify specimen information

Verify calculations

Verify graphs

Verify remarks

Submit report

Operator cannot approve his own report
(if enabled).

---

# Reviewer Responsibilities

Verify calculations

Verify standards

Verify uncertainty

Verify graphs

Approve or Reject

---

# Manager Responsibilities

Final approval

Digital release

Certificate authorization

Report locking

---

# Digital Signature

Each approval stores

Operator Name

Employee ID

Approval Time

Approval Date

Approval Level

Digital Hash

Certificate Revision

Computer Name

Windows User

Optional

---

# Approval States

Draft

Under Review

Verified

Approved

Rejected

Archived

Cancelled

---

# Certificate Locking

After final approval

The following become read-only

Engineering Results

Graphs

Tables

Remarks

Approval Block

Only a new revision may modify the report.

---

# Revision Control

Revision

0

Draft

Revision

1

Released

Revision

2+

Modified Certificate

Previous revisions remain archived.

---

# Digital Hash

Each certificate receives a unique checksum

Example

```
SHA-256
```

Stored in SQLite

Used to verify

that the document has not changed.

---

# Electronic Signature

Current Version

Internal Approval Record

Future Version

PKI Certificate

USB Token

Smart Card

Windows Certificate Store

Reserved

---

# QR Verification

Optional

QR Code contains

Certificate Number

Revision

Issue Date

Verification Hash

Future

Online Verification URL

---

# Approval Log

Every approval action is recorded

Action

Operator

Timestamp

Computer

Old Status

New Status

Reason

---

# Approval Database

SQLite

Tables

```
tblApproval

tblApprovalHistory

tblDigitalSignature

tblCertificate
```

---

# User Permissions

Operator

Create

Edit Draft

Submit

Reviewer

Review

Reject

Approve

Manager

Approve

Release

Archive

Administrator

Full Access

---

# Rejection

Reviewer may reject

a report.

Reason required.

Report returns to

Draft

Status.

---

# Audit Trail

Every action shall be recorded.

Examples

Created

Modified

Submitted

Reviewed

Approved

Printed

Exported

Archived

Deleted (logical only)

---

# Security

No report may be modified

after approval.

No engineering value

may change

without

creating a new revision.

Deletion of approval history

is prohibited.

---

# Backup

Approval database

shall be included in

automatic backup.

Daily backup recommended.

---

# Error Handling

Missing Reviewer

↓

Reject Approval

Duplicate Approval

↓

Ignore

Hash Failure

↓

Certificate Invalid

Permission Failure

↓

Access Denied

---

# Future Enhancements

PKI Digital Signature

Cloud Authentication

Two-Factor Authentication

Electronic Seal

Blockchain Verification

Electronic Approval Workflow

Reserved

---

# Acceptance Criteria

✔ ISO/IEC 17025 compliant

✔ Multi-level approval

✔ Complete audit trail

✔ Certificate locking

✔ Revision control

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Ready for future PKI implementation

---

End of Document
