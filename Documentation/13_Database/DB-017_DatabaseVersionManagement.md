# Database Version Management

Document ID : MTDMS-DB-017

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

The Database Version Management module controls database structure evolution throughout the lifetime of MTDMS.

It guarantees that older databases remain compatible with newer versions of the application.

Engineering data shall never be lost during database upgrades.

---

# Objectives

The module shall

• Store database version

• Detect version mismatch

• Upgrade schema

• Preserve data

• Roll back failed upgrades

• Record upgrade history

---

# Design Philosophy

Application Version

↓

Database Version

↓

Version Check

↓

Migration

↓

Continue

Database migration affects structure only.

Engineering records remain unchanged.

---

# Table Name

tblDatabaseVersion

---

# Primary Key

VersionID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

VersionID

INTEGER

----------------------------

DatabaseVersion

TEXT

Example

1.0.0

----------------------------

SchemaVersion

INTEGER

----------------------------

ApplicationVersion

TEXT

----------------------------

MigrationDate

DATE

----------------------------

MigrationTime

TIME

----------------------------

OperatorID

INTEGER

Nullable

----------------------------

MigrationStatus

TEXT

Examples

Success

Failed

Cancelled

----------------------------

BackupLocation

TEXT

----------------------------

RollbackAvailable

BOOLEAN

----------------------------

Remarks

TEXT

Nullable

---

# Version Check

Application Start

↓

Read Database Version

↓

Compare

↓

Match

↓

Continue

↓

Mismatch

↓

Migration Required

---

# Migration Rules

Migration shall

Never delete engineering records

Never modify imported TXT references

Never modify report history

Never modify certificate history

Only modify

Database structure

Indexes

New tables

New columns

---

# Backup Before Migration

Before every migration

Create

Complete SQLite Backup

↓

Verify Backup

↓

Start Migration

---

# Rollback

If migration fails

↓

Restore Backup

↓

Abort Application Start

---

# Migration Log

Every migration records

Old Version

New Version

Date

Time

Operator

Computer

Software Version

Result

---

# Compatibility

Supported

Older database

↓

New application

Automatic migration

Unsupported

New database

↓

Older application

Application shall stop.

---

# SQLite Relationships

tblDatabaseVersion

↓

Referenced by

System Initialization

Audit Trail

---

# Indexes

IX_DatabaseVersion

IX_SchemaVersion

---

# Constraints

Only one

Active database version

shall exist.

---

# Audit Trail

Record

Migration

Old Version

New Version

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Migration

Backup

Restore

Quality Manager

Read

Reviewer

Read

Operator

No Access

---

# Error Handling

Database Locked

↓

Retry

Backup Failure

↓

Abort

Migration Failure

↓

Rollback

Unknown Version

↓

Abort

---

# Performance

Version check

Target

< 100 ms

Migration

Depends on schema size.

---

# Acceptance Criteria

✔ Automatic version detection

✔ Automatic backup

✔ Safe migration

✔ Rollback supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering data preserved

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
