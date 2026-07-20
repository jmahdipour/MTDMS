# TXT SQLite Synchronization Specification

Document ID : MTDMS-IMP-041

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Module

Import Engine

---

# Purpose

This document defines how the TXT Import Engine synchronizes imported data with the SQLite database.

Synchronization guarantees that:

- no duplicate imports occur,
- every project remains traceable,
- engineering data is always linked to its original raw data,
- database consistency is maintained.

---

# Design Philosophy

TXT File

↓

Import Session

↓

SQLite Transaction

↓

Commit

↓

Engineering Engine

No engineering module shall write directly to SQLite without passing through the synchronization layer.

---

# Synchronization Workflow

```
Open Database

↓

Begin Transaction

↓

Verify Project

↓

Verify Machine

↓

Verify Material

↓

Verify Standard

↓

Create Import Session

↓

Insert Raw Data

↓

Commit

↓

Engineering Engine
```

---

# Transaction Policy

Every TXT import shall execute inside

ONE

SQLite Transaction.

```
BEGIN TRANSACTION

↓

INSERT

↓

COMMIT
```

If any critical error occurs

```
ROLLBACK
```

shall be executed immediately.

---

# Synchronization Order

1

Project

↓

2

Machine Profile

↓

3

Material

↓

4

Standard

↓

5

Import Session

↓

6

Raw Data

↓

7

Engineering Data

↓

8

Graphs

↓

9

Reports

---

# Database Tables

Synchronization affects

```
tblProjects

tblMachines

tblMaterials

tblStandards

tblImportSession

tblRawData

tblEngineeringData

tblAuditTrail
```

---

# Duplicate Detection

Before import

Compare

TXT File Name

Checksum

Project

Machine

Import Date

---

# Duplicate Rules

Same Project

+

Same Checksum

↓

Duplicate Import

↓

Operator Warning

↓

Abort

or

Create New Session

---

# Checksum

Every TXT file receives

SHA-256

Checksum

Stored in

```
tblImportSession
```

---

# Project Synchronization

If Project Exists

↓

Reuse ProjectID

If Project Does Not Exist

↓

Create Project

↓

Continue

---

# Material Synchronization

Search

```
tblMaterials
```

Found

↓

Use MaterialID

Not Found

↓

Operator Selection

↓

Continue

---

# Standard Synchronization

Search

```
tblStandards
```

Found

↓

Load StandardID

Not Found

↓

Operator Selection

↓

Continue

---

# Machine Synchronization

Machine Profile

↓

MachineID

↓

Project

Machine configuration stored only once.

---

# Raw Data Synchronization

Each sample

↓

One Row

↓

tblRawData

No updates allowed.

---

# Engineering Synchronization

Engineering tables are rebuilt

from

Raw Data.

Old Engineering Data

↓

Deleted

↓

Recalculated

↓

Inserted

---

# Report Synchronization

Reports are never synchronized.

Reports are regenerated.

Only report metadata stored.

---

# Graph Synchronization

Graph objects

Not stored

Only graph metadata

Stored.

---

# Rollback Conditions

Rollback occurs when

Database Locked

Transaction Failure

Primary Key Conflict

Invalid Raw Data

Critical Parser Error

Unexpected Exception

---

# Recovery

After rollback

Database

↓

Consistent

Workbook

↓

Open

Operator

↓

May Retry

---

# Synchronization Logging

Every synchronization stores

ProjectID

SessionID

Checksum

Start Time

End Time

Inserted Rows

Rollback Status

Operator

---

# Performance Target

100000 Samples

↓

Complete Synchronization

↓

Less than

10 Seconds

SSD

Recommended

---

# Future Synchronization

Cloud SQLite

Multi-user

Replication

Incremental Synchronization

Reserved

---

# Acceptance Criteria

✔ Single transaction import

✔ Automatic rollback

✔ Duplicate detection

✔ Checksum verification

✔ Raw Data immutable

✔ Engineering regenerated

✔ SQLite integrity preserved

✔ Excel 2019 compatible

---

End of Document
