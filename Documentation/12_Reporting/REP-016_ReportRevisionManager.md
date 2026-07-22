# Report Revision Manager

Document ID : MTDMS-REP-016

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

The Report Revision Manager controls every revision applied to laboratory reports after the initial issue.

Its purpose is to preserve complete document history while preventing unauthorized modification of released reports.

Engineering calculations are never changed automatically.

Any revision affecting engineering data requires a completely new validation cycle.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 15489

Laboratory Document Control Procedure

---

# Objectives

The module shall

• Manage report revisions

• Preserve previous revisions

• Record revision history

• Prevent revision loss

• Support document traceability

---

# Revision Workflow

```
Released Report

↓

Revision Request

↓

Revision Manager

↓

Reason Verification

↓

New Revision

↓

Approval

↓

Release
```

---

# Revision Principle

Released reports

shall never be overwritten.

Every modification creates

a new revision.

---

# Revision Format

Default

```
R00

R01

R02

R03
```

Administrator configurable.

---

# Initial Revision

Default

```
R00
```

The first released report always begins with

Revision

R00

---

# Revision Triggers

Revision required when

Customer information changes

Laboratory information changes

Report formatting changes

Approval information changes

Engineering result correction

Template update

Administrative correction

---

# Engineering Data Revisions

If engineering values change

↓

Entire validation chain

must be executed again.

Engineering revisions

are not cosmetic revisions.

---

# Cosmetic Revisions

Examples

Logo update

Typographical correction

Footer correction

Contact information

Watermark

Page numbering

Engineering revalidation

Not Required

---

# Engineering Revisions

Examples

Yield Strength corrected

Material corrected

Graph corrected

Acceptance corrected

Engineering revalidation

Required

---

# Revision History

Each revision stores

Revision Number

Previous Revision

Reason

Reviewer

Approval Date

Release Date

Operator

---

# Report Header

Displays

Certificate Number

Revision

Issue Date

Previous Revision

(Optional)

---

# Previous Revisions

All previous revisions remain archived.

Deletion is not permitted.

---

# Revision Comparison

Supported

Current Revision

Previous Revision

Differences

Reviewer Notes

Future enhancement

Automatic comparison.

---

# SQLite Database

Tables

```
tblRevision

tblRevisionHistory

tblRevisionReason

tblRevisionApproval
```

---

# Audit Trail

Every revision records

Certificate Number

Revision

Operator

Reviewer

Reason

Timestamp

Computer Name

Software Version

---

# Permissions

Administrator

Create Revision

Quality Manager

Approve

Reviewer

Review

Operator

Draft Only

---

# Error Handling

Missing Previous Revision

↓

Warning

Invalid Revision Number

↓

Abort

Revision Conflict

↓

Abort

Database Failure

↓

Abort

---

# Future Enhancements

Automatic Difference Report

Revision Comparison Viewer

Electronic Approval

Revision Notifications

Reserved

---

# Acceptance Criteria

✔ Revision history preserved

✔ Previous revisions retained

✔ Engineering revisions force revalidation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
