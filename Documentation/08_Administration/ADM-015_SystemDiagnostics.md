# System Diagnostics

Document ID : MTDMS-ADM-015

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

The System Diagnostics module verifies the operational health of the entire MTDMS system.

It is used for

• Startup verification
• Troubleshooting
• Maintenance
• Accreditation audits
• Preventive inspection
• Support activities

The module shall never modify engineering results.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 27001 (Recommended)

---

# Diagnostic Scope

Database

Import Engine

Engineering Engine

Graph Engine

Report Engine

Backup System

Audit System

Material Library

Standard Library

Machine Configuration

PLC Communication

Load Cells

Extensometers

License System

---

# Diagnostic Workflow

```
Start Diagnostics

↓

Database Check

↓

Configuration Check

↓

Communication Check

↓

Hardware Check

↓

Module Check

↓

Performance Check

↓

Generate Diagnostic Report
```

---

# Database Diagnostics

Verify

SQLite file exists

Integrity check

Foreign keys

Index status

File size

Read/write access

Schema version

Result

PASS / FAIL

---

# Configuration Diagnostics

Verify

Application settings

Folders

Templates

Log paths

Backup paths

Language files

Missing items

↓

Warning

---

# Communication Diagnostics

Supported

Ethernet

RS-232

RS-485

TCP/IP

Checks

Connection

Timeout

Retry

Latency

Packet loss

PLC response

---

# PLC Diagnostics

Verify

PLC reachable

Correct model

Correct firmware

Communication driver

Heartbeat

Register access

---

# Load Cell Diagnostics

Verify

Load Cell ID

Capacity

Calibration status

Signal range

Zero reading

Communication

---

# Extensometer Diagnostics

Verify

Extensometer ID

Range

Calibration status

Signal range

Connection

---

# Engineering Diagnostics

Verify

Yield algorithms

Rp algorithms

Rt algorithms

UTS detection

Fracture detection

Young's modulus calculation

True stress calculation

Hardening calculation

---

# Graph Diagnostics

Verify

Rendering engine

Zoom

Pan

Markers

Correction engine

Export engine

Memory usage

---

# Report Diagnostics

Verify

Templates

PDF export

Graph insertion

Logo loading

Approval block

Font availability

---

# Backup Diagnostics

Verify

Backup folder

Write access

Available space

Latest backup

Checksum verification

Retention policy

---

# Audit Diagnostics

Verify

Audit logging enabled

Write access

Record creation

Retention configuration

---

# License Diagnostics

Verify

License present

License valid

Machine ID match

Expiration

Enabled modules

---

# Performance Diagnostics

Measure

Database response time

Graph render time

PDF export time

Memory usage

CPU usage

File I/O speed

---

# Diagnostic Levels

Quick

Startup checks

Standard

All major modules

Full

Complete hardware and software verification

---

# Diagnostic Report

The report shall include

Date

Operator

Computer Name

Application Version

Database Version

License Status

Results Table

Warnings

Errors

Recommendations

---

# SQLite Database

Tables

```
tblDiagnostics

tblDiagnosticsHistory
```

Fields

Diagnostic ID

Level

Date

Operator

Result

Warning Count

Error Count

Duration

---

# Error Classification

Information

Warning

Error

Critical

Critical errors may block operation.

---

# Recommendations

Examples

Run database optimization

Calibrate load cell

Replace expired reference standard

Increase backup frequency

Check network connection

---

# Automatic Diagnostics

Optional

Run at startup

Run daily

Run weekly

Run before calibration

Run before software update

Administrator configurable.

---

# Permissions

Administrator

Full Access

Maintenance Engineer

Run Diagnostics

Quality Manager

View Reports

Operator

View Status Only

---

# Future Enhancements

Remote Diagnostics

Cloud Monitoring

Predictive Failure Detection

Automatic Repair Suggestions

IoT Health Monitoring

Reserved

---

# Acceptance Criteria

✔ Complete system verification

✔ Hardware verification

✔ Database verification

✔ Performance measurement

✔ Diagnostic report generation

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

---

End of Document
