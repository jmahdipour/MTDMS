# Database Security

Document ID : MTDMS-DB-022

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

This document defines the database security architecture for MTDMS.

Its purpose is to protect

Configuration

Metadata

Audit records

Reports

Certificates

Archive references

while preserving engineering traceability.

The original TXT file remains the engineering master record.

---

# Objectives

The security system shall

• Prevent unauthorized access

• Protect engineering records

• Protect audit records

• Protect configuration

• Preserve traceability

• Support ISO/IEC 17025 requirements

---

# Security Philosophy

TXT File

↓

Engineering Calculation

↓

Validated Results

↓

SQLite Metadata

↓

Access Control

Security protects

database contents

not engineering calculations.

---

# Security Layers

Application

↓

SQLite

↓

Operating System

↓

Backup

---

# Protected Data

Configuration

Material Library

Customer Library

Machine Library

Operator Library

Standard Library

Templates

Audit Trail

Report History

Certificate History

Archive History

Backup History

Validation History

---

# Unprotected Data

Original TXT files

remain

ordinary files

managed by

operating system permissions.

---

# User Roles

Administrator

Laboratory Manager

Quality Manager

Reviewer

Operator

Read Only

---

# Permission Matrix

Administrator

Read

Write

Modify

Delete

Backup

Restore

Migration

----------------------------

Quality Manager

Read

Approve

Archive

Export

----------------------------

Reviewer

Read

Review

Export

----------------------------

Operator

Import

Calculate

Generate Report

Read

----------------------------

Read Only

Read

Search

Print

---

# Database Protection

SQLite file

shall be

stored

inside

restricted folders.

Users shall not modify SQLite directly.

---

# Configuration Protection

Only

Administrator

may modify

Configuration

Templates

Material Library

Customer Library

Machine Library

---

# Audit Protection

Audit records

shall never

be editable

through

the user interface.

---

# Archive Protection

Archived reports

shall be

read-only.

Archive references

shall never

be modified.

---

# Password Policy

If application login is enabled

Passwords

shall be

stored as

cryptographic hashes.

Plain text passwords

are prohibited.

---

# Session Management

User Login

↓

Session Created

↓

Automatic Timeout

↓

Logout

Timeout

Administrator configurable.

---

# Failed Login

Repeated failures

shall be recorded

inside

Audit Trail.

Administrator configurable.

---

# File Permissions

Recommended

Read

Write

Modify

Delete

restricted by

Windows permissions.

---

# Engineering Independence

Security

shall never

modify

Engineering Results

TXT Files

Engineering Tables

Graph Data

Validation Results

---

# Database Encryption

Optional

Administrator configurable.

SQLite encryption

may be used

if required.

---

# Audit Trail

Every security event

shall record

Operator

Action

Timestamp

Computer

Software Version

Result

---

# Error Handling

Unauthorized Access

↓

Reject

Database Locked

↓

Retry

Permission Denied

↓

Abort

Invalid Login

↓

Audit Record

---

# Acceptance Criteria

✔ User roles supported

✔ Access control supported

✔ Audit protection

✔ Configuration protection

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
