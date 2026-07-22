# Acceptance Summary

Document ID : MTDMS-REP-014

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

The Acceptance Summary presents the final acceptance status of the tested specimen based on the acceptance criteria previously evaluated by the Validation subsystem.

This module is presentation only.

It does not determine acceptance.

It does not perform engineering calculations.

It only reports validated acceptance decisions.

---

# Reference Standards

ISO/IEC 17025

ISO 6892-1

ISO 630

ISO 898

INSO 3132

Customer Specifications

Internal Laboratory Procedures

---

# Objectives

The module shall

• Display acceptance results

• Display evaluated properties

• Display governing specification

• Present overall decision

• Preserve engineering traceability

---

# Workflow

```
Validated Engineering Results

↓

Acceptance Validation

↓

Acceptance Summary

↓

Report Engine
```

---

# Acceptance Sources

Customer Specification

International Standard

National Standard

Internal Specification

Project Specification

Administrator configurable.

---

# Overall Status

Possible values

PASS

FAIL

NOT EVALUATED

RETEST REQUIRED

MANUAL REVIEW

Only one overall status shall appear.

---

# Decision Rules

Overall status is received from

Validation Module

The Reporting module never recalculates acceptance.

---

# Property Summary

Example

| Property | Requirement | Measured | Status |
|----------|-------------|---------:|--------|
| Yield Strength | ≥355 MPa | 362 MPa | PASS |
| Ultimate Strength | 470–630 MPa | 515 MPa | PASS |
| Elongation | ≥22 % | 19 % | FAIL |

---

# Status Indicators

PASS

Green

FAIL

Red

WARNING

Yellow

NOT EVALUATED

Gray

Color definitions are configurable.

---

# Governing Specification

Displays

Specification Number

Revision

Acceptance Profile

Material Grade

Customer Requirement

---

# Comments

Optional

Laboratory Comment

Reviewer Comment

Customer Comment

Administrator configurable.

---

# Retest Information

If status

RETEST REQUIRED

Displays

Reason

Reviewer

Requested Date

Reference Number

---

# Manual Review

If status

MANUAL REVIEW

Displays

Reason

Reviewer

Approval Pending

---

# Report Position

Default

Immediately after

Engineering Results

Before

Approval Block

Administrator configurable.

---

# Multilingual Support

Supported

Persian

English

Arabic

Other configured languages

Engineering values remain unchanged.

---

# Engineering Independence

Acceptance Summary

never modifies

Engineering Results

Graphs

Material Information

Standard Information

---

# SQLite Database

Tables

```
tblAcceptanceSummary

tblAcceptanceDecision

tblAcceptanceComment

tblAcceptanceHistory
```

---

# Audit Trail

Store

Certificate Number

Acceptance Profile

Overall Status

Reviewer

Timestamp

Revision

Software Version

---

# Permissions

Administrator

Modify Layout

Quality Manager

Approve

Reviewer

Generate

Operator

Read Only

---

# Error Handling

Acceptance Missing

↓

Display

NOT EVALUATED

Profile Missing

↓

Warning

Corrupted Acceptance Data

↓

Abort

Reviewer Missing

↓

Warning

---

# Future Enhancements

Electronic Approval

Digital Acceptance Stamp

Customer Acceptance Matrix

Batch Acceptance Dashboard

Reserved

---

# Acceptance Criteria

✔ Overall decision displayed

✔ Property-level status displayed

✔ Governing specification displayed

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unchanged

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
