# Documentation/13_Database/DB-001_DatabaseArchitecture.md

Document ID : MTDMS-DB-001

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Database

SQLite

Status

Production

---

# Purpose

This document defines the internal database architecture used by MTDMS.

The database is **not** the source of engineering test data.

The engineering data always originates from the imported TXT file exported by the testing machine.

SQLite is used only for

• configuration

• history

• archive

• templates

• material library

• report tracking

• audit trail

---

# Fundamental Principle

```
TXT File

↓

Import

↓

Engineering Calculation

↓

Validation

↓

Report

↓

SQLite Storage
```

The TXT file is always the Master Source.

SQLite never replaces the imported engineering data.

---

# Database Responsibilities

Store

User settings

Material library

Report history

Certificate history

Templates

Machine definitions

Audit trail

Import history

Graph settings

Customer information

Standard library

Export history

---

# Database Does NOT Store

Raw engineering calculations

Machine communication

Live testing

Force acquisition

Extension acquisition

Real-time graph generation

These operations are performed entirely inside Excel memory.

---

# Architecture

```
TXT

↓

Excel VBA

↓

Memory Objects

↓

Calculation Engine

↓

Validation Engine

↓

Report Engine

↓

SQLite
```

---

# SQLite File

Default

```
MTDMS.db
```

Single file

Local

Portable

No installation required.

---

# Database Sections

Configuration

Material Library

Customer Library

Machine Library

Operator Library

Report History

Certificate History

Archive

Audit Trail

Import History

Export History

Template Library

Standard Library

---

# Database Philosophy

Engineering calculations

↓

Temporary

Memory only

↓

Validated

↓

Stored

Only validated information is stored permanently.

---

# Import Philosophy

Every imported TXT file receives

Unique Import ID

Checksum

Original Filename

Import Time

Operator

Machine

The original TXT file is never modified.

---

# Data Flow

```
TXT

↓

Import Buffer

↓

Memory Object

↓

Engineering Calculation

↓

Validation

↓

Approved Result

↓

SQLite
```

---

# Database Rules

SQLite is never allowed

to calculate

engineering values.

SQLite only stores.

---

# Primary Keys

Every table

Integer

Auto Increment

Primary Key

---

# Foreign Keys

Enabled

Relationship integrity required.

---

# Transactions

All write operations

BEGIN

↓

INSERT

↓

UPDATE

↓

COMMIT

Failure

↓

ROLLBACK

---

# Backup

Automatic

Daily

Manual

Before Upgrade

Administrator configurable.

---

# Restore

Supported

Entire database

Configuration only

Material Library

Templates

Archive

---

# Performance Targets

Database opening

< 1 second

Insert history

< 50 ms

Material lookup

< 20 ms

Archive search

< 200 ms

---

# Maximum Size

Recommended

< 2 GB

Large graph images shall never be stored inside SQLite.

Only file references are stored.

---

# Security

Read

Write

Administrator

Quality Manager

Reviewer

Operator

Permissions controlled inside VBA.

---

# Acceptance Criteria

✔ TXT remains Master Source

✔ SQLite used only for storage

✔ Excel 2019 compatible

✔ SQLite portable

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
