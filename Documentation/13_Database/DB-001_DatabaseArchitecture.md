# Documentation/13_Database/DB-001_DatabaseArchitecture.md

# Database Architecture

Document ID : MTDMS-DB-001

Version : 1.0

Platform

Microsoft Excel 2019

Database

SQLite

Programming Language

VBA

Application

MTDMS

Status

Production

---

# Purpose

This document defines the overall architecture of the SQLite database used by MTDMS.

The database is responsible for permanent storage of all laboratory information except temporary calculation data.

No engineering calculations are performed inside the database.

The database only stores validated information.

---

# Design Philosophy

Engineering Calculation

↓

Validation

↓

SQLite Storage

↓

Reporting

The database is a permanent storage system.

It is not a calculation engine.

---

# Design Goals

The database shall

• Preserve all engineering information

• Prevent duplicate records

• Support traceability

• Support report generation

• Support calibration history

• Support audit trail

• Support future expansion

---

# Database Engine

SQLite 3

Database File

```
MTDMS.db
```

Single database file

No client-server required.

---

# Character Encoding

UTF-8

Supports

Persian

English

Arabic

Unicode

---

# File Structure

```
Database

│

├── Master Tables

├── Test Tables

├── Material Tables

├── Machine Tables

├── Calibration Tables

├── Reporting Tables

├── User Tables

├── Configuration Tables

└── Audit Tables
```

---

# Main Categories

01

Master Data

02

Imported Files

03

Engineering Tests

04

Machines

05

Materials

06

Calibration

07

Reporting

08

Users

09

Configuration

10

Audit

---

# Primary Keys

Every table

shall have

INTEGER PRIMARY KEY

AUTOINCREMENT

---

# Foreign Keys

Foreign Keys

Enabled

Relationship integrity

Mandatory

---

# Date Storage

ISO Format

```
YYYY-MM-DD
```

Time

```
HH:MM:SS
```

Timestamp

UTC

Recommended

---

# Numeric Storage

Engineering values

REAL

Identifiers

INTEGER

Names

TEXT

Boolean

INTEGER

0

1

---

# File Storage

Large files

shall NOT

be stored

inside SQLite.

Only

File Path

File Hash

File Size

Import Date

are stored.

---

# Engineering Rule

SQLite

never

stores temporary calculations.

Only validated results.

---

# Transaction Policy

Every write operation

shall use

BEGIN TRANSACTION

COMMIT

Automatic rollback on failure.

---

# Integrity Rules

Primary Keys

Unique

Foreign Keys

Enforced

Duplicate Certificate

Forbidden

Duplicate Report Number

Forbidden

Duplicate Archive ID

Forbidden

---

# Index Policy

Indexes required on

Certificate Number

Report Number

Archive ID

Import Date

Material Grade

Machine ID

Customer ID

Heat Number

---

# Backup

Manual

Automatic

Versioned

Backup

Recommended

---

# Restore

Entire Database

Single Table

Future

Single Record

Reserved

---

# Maximum Database Size

Target

<10 GB

SQLite supports larger sizes.

---

# Database Version

Stored

Inside

tblDatabaseVersion

Every schema change

increments

Database Version.

---

# Compatibility

SQLite 3

Excel 2019

64-bit

32-bit

Windows

---

# Audit Policy

Every modification

shall be recorded.

No silent updates.

---

# Acceptance Criteria

✔ SQLite

✔ UTF-8

✔ Referential Integrity

✔ Transaction Safe

✔ ISO/IEC 17025 Compatible

✔ Audit Ready

✔ Excel 2019 Compatible

---

End of Document
