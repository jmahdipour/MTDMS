# Database Relationships

Document ID : MTDMS-DB-019

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

This document defines the logical relationships between all SQLite tables used by MTDMS.

It establishes database integrity.

It defines foreign key dependencies.

It does not describe engineering calculations.

---

# Design Philosophy

TXT File

↓

Import History

↓

Engineering Calculation

↓

Validation

↓

Report

↓

Certificate

↓

Archive

SQLite stores relationships

between records.

The TXT file remains the engineering master record.

---

# Master Tables

tblMaterialLibrary

tblCustomer

tblMachine

tblOperator

tblStandard

tblTemplate

tblConfiguration

---

# Transaction Tables

tblImportHistory

tblValidation

tblReport

tblCertificate

tblArchive

tblExportHistory

tblAuditTrail

tblBackupHistory

---

# Relationship Overview

```
tblMaterialLibrary

        │

        ├──────────────┐

        │              │

        ▼              ▼

    tblReport     tblCertificate

```

---

```
tblCustomer

      │

      ├─────────────┐

      │             │

      ▼             ▼

  tblReport    tblCertificate

```

---

```
tblMachine

      │

      ▼

tblImportHistory

      │

      ▼

tblReport

```

---

```
tblOperator

     │

     ├──────────────┐

     │              │

     ▼              ▼

tblValidation   tblReport

     │

     ▼

tblCertificate

```

---

```
tblImportHistory

      │

      ▼

tblValidation

      │

      ▼

tblReport

      │

      ▼

tblCertificate

      │

      ▼

tblArchive

```

---

```
tblReport

     │

     ├──────────────┐

     │              │

     ▼              ▼

tblExportHistory

tblAuditTrail

```

---

# Foreign Keys

tblReport

ImportID

↓

tblImportHistory

----------------------------

CustomerID

↓

tblCustomer

----------------------------

MaterialID

↓

tblMaterialLibrary

----------------------------

MachineID

↓

tblMachine

----------------------------

OperatorID

↓

tblOperator

----------------------------

StandardID

↓

tblStandard

---

tblCertificate

ReportID

↓

tblReport

----------------------------

CustomerID

↓

tblCustomer

----------------------------

OperatorID

↓

tblOperator

---

tblArchive

ReportID

↓

tblReport

----------------------------

CertificateID

↓

tblCertificate

----------------------------

ImportID

↓

tblImportHistory

---

tblValidation

ReportID

↓

tblReport

----------------------------

ImportID

↓

tblImportHistory

----------------------------

OperatorID

↓

tblOperator

---

tblExportHistory

ReportID

↓

tblReport

----------------------------

CertificateID

↓

tblCertificate

----------------------------

OperatorID

↓

tblOperator

---

tblAuditTrail

OperatorID

↓

tblOperator

---

# Referential Integrity

Foreign Keys

Enabled

ON

DELETE

RESTRICT

ON

UPDATE

CASCADE

Recommended

---

# Engineering Independence

Relationships

never modify

Engineering Results

TXT Files

Engineering Tables

Graph Data

Relationships manage

references only.

---

# Orphan Record Prevention

Deletion shall be prevented when

Customer

is referenced by reports.

Machine

is referenced by imports.

Material

is referenced by reports.

Operator

is referenced by audit records.

Report

is referenced by certificates.

Certificate

is referenced by archives.

---

# Index Strategy

Every Foreign Key

shall have

its own index.

This improves

Search

Join

Filtering

Performance.

---

# Transaction Strategy

All multi-table operations

shall use

SQLite transactions.

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

# Acceptance Criteria

✔ Referential integrity

✔ Foreign keys enabled

✔ Orphan records prevented

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete database consistency

---

End of Document
