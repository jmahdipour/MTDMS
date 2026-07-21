# Role Management

Document ID : MTDMS-ADM-003

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

This document defines the Role Management subsystem.

Role Management determines what each authenticated user is permitted to do inside MTDMS.

Permissions are assigned to roles rather than individual users.

This simplifies administration while maintaining complete ISO/IEC 17025 traceability.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 27001 (Recommended)

21 CFR Part 11 (Future)

---

# Objectives

The Role Management module shall

• Centralize permissions

• Prevent unauthorized operations

• Support least-privilege access

• Record every permission change

• Maintain audit history

---

# Architecture

```
User

↓

Assigned Role

↓

Permission Set

↓

Authorized Functions

↓

System
```

---

# Built-in Roles

Administrator

Laboratory Manager

Technical Reviewer

Operator

Calibration Engineer

Chemical Analyst

Mechanical Analyst

Quality Manager

Auditor

Read Only

Guest

Administrator may create additional roles.

---

# Permission Categories

System

Database

Engineering

Reports

Calibration

Machine Configuration

Material Library

Standards

User Management

Backup

Audit

Security

---

# Engineering Permissions

Import Data

View Data

Edit Raw Data

Recalculate Results

Approve Results

Delete Results

Export Results

Generate Graphs

Manual Yield Correction

Elastic Region Editing

Graph Correction

---

# Report Permissions

Preview

Generate

Edit Template

Approve

Reject

Export PDF

Print

Archive

Delete Draft

---

# Calibration Permissions

Create Calibration

Edit Calibration

Approve Calibration

Issue Certificate

View History

Reference Standard Management

Uncertainty Configuration

---

# Administration Permissions

Create User

Modify User

Reset Password

Assign Roles

Create Roles

Delete Roles

System Configuration

License Management

Database Maintenance

---

# Material Library Permissions

Create Material

Modify Material

Delete Material

Import Material

Export Material

Approve Material

Revision Management

---

# Machine Permissions

Register Machine

Modify Machine

Delete Machine

Assign Load Cell

Assign Extensometer

Configure Channels

Configure PLC

Configure Communication

---

# Security Permissions

Unlock User

View Audit Log

Delete Audit Log

Never Allowed

Export Security Data

Administrator configurable.

---

# Permission Matrix

Example

| Permission | Administrator | Manager | Reviewer | Operator | Read Only |
|------------|---------------|---------|----------|----------|-----------|
| Import Data | ✔ | ✔ | ✔ | ✔ | ✖ |
| Engineering Calculation | ✔ | ✔ | ✔ | ✔ | ✖ |
| Manual Yield Editing | ✔ | ✔ | ✔ | ✔ | ✖ |
| Approve Results | ✔ | ✔ | ✔ | ✖ | ✖ |
| Generate Reports | ✔ | ✔ | ✔ | ✔ | ✔ |
| PDF Export | ✔ | ✔ | ✔ | ✔ | ✔ |
| User Management | ✔ | ✖ | ✖ | ✖ | ✖ |
| System Configuration | ✔ | ✖ | ✖ | ✖ | ✖ |

---

# Permission Evaluation

When a user requests an action

```
User

↓

Role

↓

Permission Lookup

↓

Authorized ?

↓

Execute / Reject
```

---

# Multiple Roles

A user may optionally have

Multiple Roles.

Effective permissions are

Union

of assigned roles.

Administrator configurable.

---

# Temporary Roles

Optional

Temporary permissions

may expire automatically

after

Date

Time

Project

Calibration

---

# Role Versioning

Each role maintains

Role ID

Role Name

Version

Revision

Created By

Created Date

Modified By

Modified Date

Approved

---

# SQLite Database

Tables

```
tblRoles

tblPermissions

tblRolePermission

tblUserRole
```

---

# Audit Trail

Every permission change

shall record

Role

Permission

Old Value

New Value

Operator

Timestamp

Computer

Reason

---

# Security Rules

Only Administrators

may

Create Roles

Delete Roles

Modify Permissions

Assign Administrator Role

---

# Validation

Every role must contain

Minimum

Login Permission

Otherwise

Role Invalid

---

# Error Handling

Duplicate Role

↓

Reject

Missing Permission

↓

Use Default

Corrupted Matrix

↓

Restore Backup

Unknown Role

↓

Access Denied

---

# Future Enhancements

Attribute-Based Access Control (ABAC)

Department-Based Roles

Project-Based Roles

Time-Limited Roles

Cloud Identity Mapping

Reserved

---

# Acceptance Criteria

✔ Role-based security

✔ Centralized permissions

✔ ISO 17025 traceability

✔ Complete audit trail

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Supports custom roles

✔ Least-privilege architecture

---

End of Document
