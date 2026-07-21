# Final Release Validation

Document ID : MTDMS-VAL-010

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Validation

Status

Production

---

# Purpose

The Final Release Validation module performs the last verification before a test report or certificate is officially released.

This module ensures that every required validation stage has successfully completed and that no unresolved issues remain.

It is the final software gate before report approval.

This module never changes engineering calculations.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 15489

Applicable Test Standards

---

# Objectives

The module shall

• Verify completion of all validation stages

• Prevent release of incomplete reports

• Verify report integrity

• Verify approval status

• Verify traceability

• Lock released records

---

# Release Workflow

Engineering Calculation

↓

Engineering Validation

↓

Graph Validation

↓

Acceptance Validation

↓

Report Validation

↓

Final Release Validation

↓

Release

↓

Archive

---

# Validation Checklist

The following items shall be verified.

---

## Data Validation

Imported file

PASS

Engineering input

PASS

Metadata

PASS

Units

PASS

---

## Engineering Validation

Calculation validation

PASS

Consistency validation

PASS

Material validation

PASS

Standard validation

PASS

Acceptance validation

PASS

---

## Graph Validation

Engineering graph exists

Graph validated

Markers validated

Graph linked to report

---

## Report Validation

Report generated

Report validated

Certificate number assigned

Revision assigned

PDF successfully generated

---

## Traceability Validation

Archive ID exists

Import File ID exists

Engineering Revision exists

Software Version recorded

Material Library Version recorded

Standard Library Version recorded

---

## Approval Validation

Reviewer assigned

Approval date exists

Report status

Approved

---

# Release Decision

If every validation item

PASS

↓

Release Allowed

Otherwise

↓

Release Blocked

---

# Release Status

Draft

Under Review

Approved

Released

Archived

Obsolete

---

# Record Locking

After release

The following become

Read Only

Engineering Results

Graphs

Reports

Approval

Acceptance

Certificate Number

Revision

---

# Unlock Policy

Released records

cannot be edited.

Any modification requires

New Revision

---

# Release Package

The release package contains

Engineering Results

Report

PDF

Graphs

Metadata

Archive Reference

Validation History

Checksums

---

# Certificate Verification

Verify

Certificate Number

Unique

Assigned

Not Duplicated

Valid Format

---

# Revision Verification

Verify

Revision exists

Revision approved

Revision matches report

Revision matches archive

---

# Final Validation Result

READY FOR RELEASE

RELEASE BLOCKED

MANUAL REVIEW REQUIRED

---

# Blocking Conditions

Engineering validation failed

Graph validation failed

Report validation failed

Acceptance validation failed

Approval missing

Certificate number missing

Revision missing

Archive reference missing

---

# SQLite Database

Tables

```
tblRelease

tblReleaseHistory

tblReleaseChecklist

tblReleaseLock
```

---

# Audit Trail

Every release stores

Release ID

Certificate Number

Revision

Reviewer

Approval Date

Release Date

Software Version

Operator

Computer Name

Validation Summary

---

# Permissions

Administrator

Release

Quality Manager

Release

Reviewer

Approve

Operator

Cannot Release

---

# Error Handling

Approval Missing

↓

Release Blocked

Certificate Missing

↓

Release Blocked

Database Error

↓

Abort

Archive Failure

↓

Release Blocked

---

# Future Enhancements

Digital Signature

Electronic Approval

QR Verification

Electronic Certificate Validation

Blockchain Certificate Registry

Reserved

---

# Acceptance Criteria

✔ Complete validation chain

✔ Release blocking implemented

✔ Record locking after release

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

✔ Engineering values remain unchanged

---

End of Document
