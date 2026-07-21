# Data Version Control

Document ID : MTDMS-DAT-006

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

The Data Version Control module maintains the complete revision history of every imported engineering dataset.

It guarantees that no approved engineering data is ever overwritten.

Instead, every modification creates a new revision while preserving all previous revisions.

This module supports ISO/IEC 17025 traceability requirements.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 15489 (Records Management)

---

# Objectives

The Version Control module shall

• Preserve all revisions

• Prevent data loss

• Support rollback

• Track modifications

• Maintain engineering traceability

• Support report reproducibility

---

# Scope

Version control applies to

Imported Files

Parsed Data

Normalized Data

Engineering Results

Graphs

Reports

PDF References

Material Assignments

Acceptance Decisions

---

# General Rule

Engineering data

shall NEVER

be overwritten.

Every modification creates

New Revision

---

# Revision Workflow

```
Original Import

↓

Revision 1

↓

Engineering Review

↓

Revision 2

↓

Report Correction

↓

Revision 3

↓

Approval

↓

Locked
```

---

# Revision Identification

Each revision contains

Revision ID

Revision Number

Parent Revision

Creation Date

Created By

Reason

Approval Status

Checksum

---

# Revision Types

Original

Automatic

Manual

Engineering

Administrative

Corrective

Archived

---

# Trigger Events

New Import

↓

Revision

Material Change

↓

Revision

Graph Correction

↓

Revision

Manual Yield Selection

↓

Revision

Report Correction

↓

Revision

---

# Locked Revisions

Approved revisions become

Read Only

No further modification allowed.

Subsequent edits require

New Revision

---

# Difference Tracking

Track changes for

Metadata

Material

Dimensions

Engineering Results

Acceptance

Graph

Remarks

Report

---

# Rollback

Administrator may restore

Any previous revision.

Rollback creates

a new revision.

Previous revisions remain unchanged.

---

# Comparison

Supported comparisons

Revision vs Revision

Original vs Current

Approved vs Draft

Automatic comparison includes

Metadata

Engineering Values

Graph References

Report References

---

# Revision Tree

Example

```
Rev 0

↓

Rev 1

↓

Rev 2

↓

Rev 3

↓

Approved
```

Branches are not supported in Version 1.

Linear history only.

---

# Database

SQLite

Tables

```
tblRevision

tblRevisionHistory

tblRevisionDifference

tblRevisionLock
```

---

# Search

Search by

Certificate Number

Revision Number

Operator

Date

Status

Material

Sample ID

---

# Audit Trail

Each revision stores

Old Revision

New Revision

User

Timestamp

Reason

Computer Name

Checksum

---

# Permissions

Administrator

Full Access

Engineering Manager

Create Revision

Reviewer

Read

Operator

Create Draft Revision

---

# Error Handling

Missing Parent Revision

↓

Reject

Duplicate Revision Number

↓

Reject

Locked Revision Modified

↓

Reject

Checksum Mismatch

↓

Abort

---

# Future Enhancements

Revision Branching

Digital Revision Signature

Automatic Revision Merge

Cloud Revision History

Reserved

---

# Acceptance Criteria

✔ No overwrite

✔ Complete revision history

✔ Rollback supported

✔ Difference tracking

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
