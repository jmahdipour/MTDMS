# Application Settings

Document ID : MTDMS-ADM-011

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

The Application Settings module manages all configurable global parameters used by MTDMS.

These settings affect application behavior only.

They shall never modify engineering algorithms or change calculated results.

Engineering constants belong to the Engineering Engine and Material Library, not to this module.

---

# Objectives

The Application Settings module shall

• Centralize configuration

• Separate configuration from source code

• Support administrator customization

• Preserve backward compatibility

• Support multiple laboratories

---

# Configuration Categories

General

Display

Regional

Engineering Defaults

Reports

Import

Export

Database

Backup

Security

Performance

Logging

Communication

---

# General Settings

Application Name

Company Name

Laboratory Name

Default Language

Default Theme

Application Version

Administrator configurable.

---

# Display Settings

Theme

Light

Dark

System

Font Size

Small

Medium

Large

Default Zoom

Grid Visibility

Toolbar Options

---

# Regional Settings

Country

Time Zone

Date Format

Time Format

Decimal Separator

Thousands Separator

Paper Size

Default

A4

---

# Engineering Defaults

Default Force Unit

N

kN

kgf

Default Stress Unit

MPa

GPa

Default Length Unit

mm

Default Temperature

°C

Administrator configurable.

These settings affect display only.

Stored engineering data remains unchanged.

---

# Report Settings

Default Template

Paper Orientation

Logo

Header

Footer

PDF Quality

Graph Resolution

Automatic Report Numbering

---

# Import Settings

Default Import Folder

Auto Detect Encoding

Automatic Header Detection

CSV Delimiter

TXT Delimiter

Import Preview

Automatic Backup Before Import

---

# Export Settings

Default Export Folder

Default PDF Folder

Default CSV Folder

Automatic PDF Export

Automatic Print

File Naming Pattern

---

# Database Settings

SQLite Location

Automatic Compact

Automatic Integrity Check

Journal Mode

Cache Size

Database Timeout

---

# Backup Settings

Backup Folder

Automatic Backup

Retention Period

Compression

Verification

---

# Security Settings

Idle Timeout

Password Expiration

Maximum Login Attempts

Session Timeout

Audit Enabled

Digital Signature Enabled

Administrator configurable.

---

# Performance Settings

Maximum Records

Memory Cache

Graph Cache

Auto Refresh Interval

Database Optimization

---

# Logging Settings

Enable Logging

Log Level

Information

Warning

Error

Critical

Log Retention

Maximum Log Size

---

# Communication Settings

Default PLC

Communication Timeout

Retry Count

Heartbeat Interval

Network Buffer

---

# Configuration Storage

SQLite

Tables

```
tblApplicationSettings

tblSystemOption

tblRegionalSettings
```

---

# Configuration Loading

Application Startup

↓

Read SQLite

↓

Validate Values

↓

Apply Defaults

↓

Load User Overrides

↓

Ready

---

# Validation Rules

Missing Value

↓

Load Default

Invalid Range

↓

Reject

Unknown Setting

↓

Ignore

Corrupted Configuration

↓

Restore Previous

---

# Audit Trail

Every configuration modification records

Setting Name

Old Value

New Value

User

Date

Time

Computer

Reason

---

# Permissions

Administrator

Full Access

Laboratory Manager

Limited Access

Operator

Read Only

---

# Reset

Administrator may

Restore Factory Defaults

or

Restore Laboratory Defaults

without affecting engineering data.

---

# Future Enhancements

Cloud Configuration

Multiple Configuration Profiles

Portable Configuration

Configuration Import/Export

Configuration Wizard

Reserved

---

# Acceptance Criteria

✔ Centralized configuration

✔ Engineering independent

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Administrator controlled

✔ ISO/IEC 17025 compliant

✔ Full audit trail

---

End of Document
