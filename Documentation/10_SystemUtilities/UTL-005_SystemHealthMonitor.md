# System Health Monitor

Document ID : MTDMS-UTL-005

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

System Utilities

Status

Production

---

# Purpose

The System Health Monitor continuously evaluates the operational status of the MTDMS application.

Its objective is to detect abnormal software conditions before they affect data processing.

This module monitors the software environment only.

It does not communicate with the testing machine.

It does not perform engineering calculations.

---

# Objectives

The System Health Monitor shall

• Monitor application status

• Monitor database health

• Monitor memory usage

• Monitor disk availability

• Monitor configuration consistency

• Detect abnormal conditions

• Notify administrators

---

# Monitoring Scope

Application

SQLite Database

Memory

Disk Space

Cache

Log System

Backup System

Configuration

Template Library

Archive

---

# Monitoring Workflow

```
Application Running

↓

Collect Statistics

↓

Evaluate Thresholds

↓

Generate Status

↓

Warning (if required)

↓

Store Health Report
```

---

# Health Categories

Application

Database

Memory

Storage

Configuration

Archive

Backup

Performance

Security

---

# Application Health

Monitor

Application Running

Unexpected Errors

Module Failures

Startup Status

Shutdown Status

Current Session

---

# Database Health

Verify

Connection

Integrity

Size

Fragmentation

Response Time

Locked Status

Last Maintenance

---

# Memory Health

Monitor

Current Usage

Peak Usage

Available Memory

Cache Usage

Temporary Objects

---

# Storage Health

Monitor

Free Disk Space

Database Size

Archive Size

Backup Size

Log Size

Temporary Folder Size

---

# Configuration Health

Verify

Required Settings

Template Availability

Language Files

Material Library

Standard Library

Missing configuration items generate warnings.

---

# Backup Health

Monitor

Last Backup

Backup Success

Backup Verification

Backup Age

Retention Status

---

# Archive Health

Verify

Archive Accessibility

Archive Integrity

Archive Database

Archive Size

Archive Checksum

---

# Thresholds

Memory Usage

Warning

80%

Critical

95%

Disk Usage

Warning

85%

Critical

95%

Database Size

Administrator configurable.

---

# Health Status

Healthy

Warning

Degraded

Critical

Unavailable

---

# Dashboard

Displays

Application Status

Database Status

Memory Usage

Disk Usage

Last Backup

Last Integrity Check

Current Session

Overall Health

---

# Health History

SQLite

Tables

```
tblSystemHealth

tblHealthHistory

tblHealthThreshold
```

---

# Automatic Checks

Performed

Application Startup

Every 15 Minutes

Application Shutdown

Administrator configurable.

---

# Notifications

Information

Status Bar

Warning

Message Box

Critical

Blocking Dialog

Log Entry

Always

---

# Error Handling

Database Offline

↓

Critical

Memory Overflow

↓

Critical

Configuration Missing

↓

Warning

Archive Unavailable

↓

Warning

Backup Failure

↓

Critical

---

# Audit Trail

Every health evaluation stores

Timestamp

Health Status

Module

Severity

Operator

Computer Name

---

# Permissions

Administrator

Full Access

Quality Manager

View

Operator

No Access

---

# Future Enhancements

E-mail Notification

SMS Alert

Cloud Monitoring

Health Dashboard

Predictive Diagnostics

Reserved

---

# Acceptance Criteria

✔ Continuous monitoring

✔ Database monitoring

✔ Memory monitoring

✔ Backup monitoring

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No machine communication

✔ Engineering independent

✔ Complete health history

---

End of Document
