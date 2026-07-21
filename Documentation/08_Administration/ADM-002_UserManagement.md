# User Management

Document ID : MTDMS-ADM-002

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

This document defines the User Management subsystem.

The module manages all laboratory personnel authorized to use MTDMS.

It implements authentication, authorization, user lifecycle management and traceability according to ISO/IEC 17025.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 27001 (Recommended)

21 CFR Part 11 (Future)

---

# Objectives

The User Management module shall

• Authenticate users

• Authorize operations

• Record all user activities

• Prevent unauthorized access

• Support role-based permissions

• Maintain complete audit history

---

# User Lifecycle

Create User

↓

Activate

↓

Modify

↓

Suspend

↓

Reactivate

↓

Deactivate

↓

Archive

No user shall be physically deleted.

---

# User Information

Each user record contains

User ID

Employee Number

Full Name

Department

Job Title

Username

Password Hash

Role

Status

Email

Telephone

Digital Signature

(optional)

Employment Date

Termination Date

(optional)

---

# User Status

Active

Inactive

Suspended

Locked

Archived

Expired

---

# Authentication

User Name

+

Password

↓

Authentication

↓

Role Verification

↓

System Access

Future

Windows Authentication

LDAP

Active Directory

Two-Factor Authentication

---

# Password Policy

Minimum Length

8 Characters

Recommended

12 Characters

Must contain

Uppercase

Lowercase

Number

Special Character

Administrator configurable.

---

# Password Security

Passwords shall

never

be stored as plain text.

Only

Salted Hash

shall be stored.

---

# Password Expiration

Default

90 Days

Warning

15 Days Before Expiration

Administrator configurable.

---

# Login Attempts

Maximum Failed Attempts

5

After that

↓

Account Locked

Only Administrator

may unlock.

---

# Session Management

Login Time

Logout Time

Last Activity

Idle Timeout

Default

30 Minutes

Administrator configurable.

---

# Concurrent Login

Options

Allowed

Restricted

Single Session Only

Administrator configurable.

---

# User Roles

Administrator

Laboratory Manager

Reviewer

Operator

Read Only

Guest

Future

Customer Portal

Reserved

---

# User Groups

Mechanical Laboratory

Chemical Laboratory

Calibration Laboratory

Quality Department

Management

External Auditor

Administrator configurable.

---

# Profile Information

Photo

Signature

Department

Qualifications

Training Records

Authorization Scope

Optional

---

# Authorization Matrix

Each user may be authorized for

Import

Engineering Calculations

Report Generation

Report Approval

Calibration

Material Library

Machine Configuration

Administration

Backup

Audit Review

Permissions are role dependent.

---

# Digital Signature

Optional

Each user may have

Electronic Signature

Approval Stamp

Digital Certificate

Future

PKI Certificate

---

# SQLite Database

Table

```
tblUsers
```

Fields

UserID

Username

PasswordHash

RoleID

Status

EmployeeNumber

Department

Email

Phone

CreatedDate

ModifiedDate

LastLogin

LastPasswordChange

DigitalSignature

---

# Audit Logging

Every user action shall be recorded.

Examples

Login

Logout

Password Change

Permission Change

User Creation

User Modification

Account Lock

Account Unlock

Role Assignment

Deletion Request

---

# Reports

Administrator may generate

User List

Active Users

Inactive Users

Login History

Permission Matrix

Expired Passwords

Locked Accounts

Training Authorization

---

# Error Handling

Duplicate Username

↓

Reject

Weak Password

↓

Reject

Expired Account

↓

Access Denied

Inactive User

↓

Access Denied

Database Failure

↓

Abort Login

---

# Future Enhancements

Single Sign-On

Biometric Authentication

Face Recognition

Hardware Security Token

Mobile Approval

Cloud Identity

Reserved

---

# Acceptance Criteria

✔ Role-based authentication

✔ Password hashing

✔ ISO 17025 traceability

✔ Complete audit trail

✔ SQLite compatible

✔ Excel 2019 compatible

✔ User lifecycle management

✔ Digital signature ready

---

End of Document
