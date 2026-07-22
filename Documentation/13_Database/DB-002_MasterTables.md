# Master Tables

Document ID : MTDMS-DB-002

Version : 1.0

Platform

Microsoft Excel 2019

Database

SQLite

Application

MTDMS

Module

Database

Status

Production

---

# Purpose

Master Tables contain the permanent reference data used throughout MTDMS.

These tables define the controlled vocabulary, reference values and configuration data used by the application.

Engineering test results are **not** stored in these tables.

---

# Design Principles

Master data

• changes infrequently
• is centrally managed
• is shared by all modules
• is referenced through foreign keys

---

# Master Table Groups

01

Material Library

02

Standard Library

03

Machine Library

04

Operator Library

05

Customer Library

06

Department Library

07

Unit Library

08

Test Method Library

09

Status Library

10

Configuration Library

---

# General Rules

Every master table shall contain

Primary Key

Unique Name

Status

Created Date

Modified Date

Created By

Modified By

Remarks

---

# Status Values

Active

Inactive

Archived

Deleted
(Not physically removed)

---

# Physical Deletion

Not permitted.

Records are marked

Inactive

or

Archived.

---

# Common Fields

| Field | Type | Description |
|--------|------|-------------|
| ID | INTEGER | Primary Key |
| Name | TEXT | Display Name |
| Code | TEXT | Unique Code |
| Status | INTEGER | Active/Inactive |
| CreatedDate | TEXT | ISO Date |
| ModifiedDate | TEXT | ISO Date |
| Remarks | TEXT | Optional |

---

# Relationships

Master tables are referenced by

Imported Files

Engineering Tests

Reports

Calibration

Audit

Users

---

# Lookup Strategy

All engineering modules shall retrieve reference data using

Primary Key

never

Display Name.

---

# Caching

Frequently used master tables

may be loaded into memory

during application startup.

Examples

Material Library

Unit Library

Standard Library

---

# Validation

Before insertion

Verify

Unique Code

Unique Name

Valid Status

---

# Localization

Display names

may be translated.

Internal codes

shall never change.

Example

```
MAT_S355

Display

S355

Persian

فولاد S355
```

---

# Versioning

Master tables

do not use

record revision.

Changes are logged through

Audit Tables.

---

# Import / Export

Supported

CSV

Excel

SQLite Backup

Administrator configurable.

---

# SQLite Tables Included

```
tblMaterial

tblStandard

tblMachine

tblCustomer

tblOperator

tblDepartment

tblUnit

tblTestMethod

tblStatus

tblConfiguration
```

---

# Indexes

Recommended

Primary Key

Unique Code

Unique Name

Status

---

# Audit Trail

Every modification stores

Table Name

Record ID

Old Value

New Value

Operator

Timestamp

Computer Name

---

# Permissions

Administrator

Create

Modify

Archive

Quality Manager

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Duplicate Code

↓

Reject

Duplicate Name

↓

Reject

Missing Required Field

↓

Reject

Foreign Key Failure

↓

Reject

---

# Acceptance Criteria

✔ Master data centralized

✔ Duplicate protection

✔ Referential integrity

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
