# Backup Manager

Document ID : MTDMS-ADM-008

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

The Backup Manager is responsible for protecting all engineering, laboratory and administrative information stored by MTDMS.

Its objective is to guarantee data availability, integrity and recoverability in accordance with ISO/IEC 17025 document control requirements.

The Backup Manager shall never modify engineering results.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 27001 (Recommended)

ISO 22301 (Business Continuity)

---

# Objectives

The Backup Manager shall

• Protect SQLite databases

• Protect reports

• Protect templates

• Protect configuration

• Protect audit logs

• Support automatic recovery

• Maintain backup history

---

# Protected Resources

SQLite Database

Material Library

Standard Library

Machine Configuration

Report Templates

Generated Reports

PDF Certificates

Graphs

Audit Logs

Configuration Files

User Database

Calibration Records

---

# Backup Architecture

```
Application

↓

Backup Manager

↓

Backup Package

↓

Verification

↓

Archive

↓

Recovery
```

---

# Backup Types

Full Backup

Incremental Backup

Differential Backup

Manual Backup

Automatic Backup

Emergency Backup

---

# Backup Schedule

Default

Daily

Weekly

Monthly

Administrator configurable.

---

# Automatic Backup

Triggered

Application Shutdown

Scheduled Time

Manual Command

Before Database Upgrade

Before Import (optional)

---

# Backup Package

A backup package contains

SQLite Database

Configuration

Templates

Reports

Logs

Checksums

Version Information

Backup Manifest

---

# Compression

Supported

ZIP

No Compression

Future

7Z

Administrator configurable.

---

# Encryption

Optional

AES-256

Password Protected Archive

Administrator configurable.

---

# Backup Verification

After every backup

verify

Archive Exists

Readable

Checksum Valid

File Count Correct

Database Integrity

---

# Retention Policy

Daily

30 Copies

Weekly

12 Copies

Monthly

60 Copies

Administrator configurable.

---

# Backup Naming

Format

```
YYYYMMDD_HHMMSS_FULL.zip
```

Example

```
20260721_230000_FULL.zip
```

---

# Backup Location

Primary Folder

Secondary Folder

Network Share

External Drive

Cloud (Future)

Administrator configurable.

---

# Recovery Workflow

Select Backup

↓

Verify Checksum

↓

Restore Database

↓

Restore Files

↓

Verify Integrity

↓

Application Ready

---

# Recovery Options

Complete System

Database Only

Templates Only

Reports Only

Configuration Only

User Database Only

---

# Database

SQLite

Tables

```
tblBackup

tblBackupHistory

tblRestoreHistory
```

Fields

Backup ID

Type

Date

Operator

Size

Checksum

Status

Location

---

# Audit Trail

Every backup operation records

Operator

Timestamp

Backup Type

Destination

Result

Verification Status

Computer Name

---

# Permissions

Administrator

Full Access

Laboratory Manager

Manual Backup

Operator

No Access

Read Only

View History

---

# Error Handling

Destination Full

↓

Abort

Database Locked

↓

Retry

Verification Failed

↓

Delete Backup

↓

Notify Administrator

Checksum Failure

↓

Reject Recovery

---

# Performance Targets

Full Backup

< 60 seconds

Incremental Backup

< 10 seconds

Restore

< 120 seconds

Verification

< 30 seconds

---

# Future Enhancements

Cloud Backup

Automatic Offsite Replication

Version Snapshot

Immutable Backup

Disaster Recovery Wizard

Reserved

---

# Acceptance Criteria

✔ Automatic backup

✔ Verified backup

✔ Recovery support

✔ Retention policy

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
