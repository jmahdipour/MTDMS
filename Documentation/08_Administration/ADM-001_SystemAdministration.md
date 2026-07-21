# System Administration

Document ID : MTDMS-ADM-001

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

This document defines the Administration Module of MTDMS.

The Administration Module controls all global system settings.

Engineering calculations shall never be performed inside this module.

Only system configuration and administration are allowed.

---

# Responsibilities

System Configuration

↓

Security

↓

User Management

↓

Equipment Management

↓

Material Library

↓

Standards

↓

Database Maintenance

↓

Backup

↓

Audit

---

# Administration Modules

ADM-001

System Administration

ADM-002

User Management

ADM-003

Role Management

ADM-004

Material Library

ADM-005

Equipment Manager

ADM-006

Machine Configuration

ADM-007

Standard Library

ADM-008

Backup Manager

ADM-009

Audit Log

ADM-010

License Manager

ADM-011

Application Settings

ADM-012

Language Manager

ADM-013

Template Manager

ADM-014

Database Maintenance

ADM-015

System Diagnostics

---

# Administrator Responsibilities

Create Users

Assign Roles

Manage Equipment

Manage Standards

Manage Materials

Configure Reports

Configure Backup

Review Logs

Database Maintenance

Software Updates

---

# Global Configuration

Company Name

Laboratory Name

Accreditation Number

Address

Telephone

Email

Website

Logo

Default Language

Default Units

---

# Default Engineering Settings

Stress Unit

MPa

Force Unit

N

kN

Length

mm

Temperature

°C

Administrator configurable.

---

# Default Report Settings

Paper Size

A4

Portrait

PDF Export

Enabled

Digital Signature

Optional

Watermark

Optional

---

# System Settings

SQLite Database

Location

Backup Folder

Report Folder

Import Folder

Temporary Folder

Log Folder

---

# Environment Settings

Date Format

Time Format

Decimal Separator

Thousands Separator

Language

Time Zone

---

# Startup Sequence

Load Configuration

↓

Verify Database

↓

Verify License

↓

Verify User

↓

Load Material Library

↓

Load Standards

↓

Ready

---

# Shutdown Sequence

Save Settings

↓

Flush Database

↓

Close Connections

↓

Backup (Optional)

↓

Exit

---

# Configuration Storage

SQLite

Table

```
tblSystemConfiguration
```

---

# Editable Parameters

Administrator Only

Company Information

Folders

Default Units

Default Templates

Machine Defaults

Security Settings

---

# Read Only Parameters

Database Version

Application Version

Schema Version

Installation Date

Machine ID

---

# Audit Requirements

Every configuration change

shall be recorded.

User

Old Value

New Value

Timestamp

Computer

Reason

---

# Security

Only Administrators

may modify

Global Configuration.

---

# Error Handling

Configuration Missing

↓

Load Defaults

Database Missing

↓

Abort

Invalid Configuration

↓

Restore Previous

---

# Future Enhancements

Cloud Configuration

Central Administration

Remote Management

Multi-site Synchronization

Reserved

---

# Acceptance Criteria

✔ Administrator controlled

✔ SQLite compatible

✔ ISO 17025 compliant

✔ Audit trail

✔ Excel 2019 compatible

✔ Engineering independent

---

End of Document
