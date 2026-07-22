# Complete Database Schema Specification

Document ID : MTDMS-DB-036

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

This document defines the complete logical database schema of MTDMS.

It provides the overall architecture of all SQLite tables and their relationships.

This document is the master reference for database design.

It does not describe engineering calculations.

---

# Database Architecture

The database is organized into four logical layers.

```
Reference Data
        │
        ▼
Import Layer
        │
        ▼
Engineering Layer
        │
        ▼
Reporting Layer
```

---

# Layer 1

Reference Tables

These tables change infrequently.

```
tblMaterialLibrary

tblMaterialProperty

tblCustomer

tblMachine

tblMachineCapability

tblOperator

tblStandard

tblUnit

tblTemplate

tblGraphStyle

tblCalculationProfile

tblApplicationSettings

tblConfiguration

tblErrorCode
```

---

# Layer 2

Import Tables

These tables originate from TXT files.

```
tblImportHistory

tblImportFile

tblImportValidation

tblBackupHistory
```

---

# Layer 3

Engineering Tables

These tables contain calculated engineering information.

```
tblEngineeringResult

tblGraphMarker

tblValidation
```

---

# Layer 4

Reporting Tables

```
tblReport

tblCertificate

tblArchive

tblExportHistory

tblAuditTrail

tblMaintenanceHistory
```

---

# Relationship Diagram

```
TXT File

    │

    ▼

tblImportHistory

    │

    ▼

tblEngineeringResult

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

# Reference Relationships

```
tblMaterialLibrary

        │

        ▼

tblMaterialProperty

        │

        ▼

tblEngineeringResult
```

---

```
tblMachine

       │

       ▼

tblMachineCapability

       │

       ▼

tblImportHistory
```

---

```
tblStandard

      │

      ▼

tblCalculationProfile

      │

      ▼

Calculation Engine
```

---

```
tblTemplate

      │

      ▼

tblReportFieldMapping

      │

      ▼

Excel Report
```

---

# Primary Keys

Every table

uses

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Foreign Keys

ImportID

↓

tblImportHistory

----------------------------

ReportID

↓

tblReport

----------------------------

CertificateID

↓

tblCertificate

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

----------------------------

TemplateID

↓

tblTemplate

---

# Database Rules

Reference tables

↓

rarely modified

Import tables

↓

never manually edited

Engineering tables

↓

generated automatically

Reporting tables

↓

generated automatically

Audit tables

↓

never edited

---

# Engineering Independence

Engineering calculations

shall always

start from

the imported TXT file.

SQLite stores

history

configuration

results

references

only.

---

# Database Growth

Reference Tables

Small

----------------------------

Import Tables

Large

----------------------------

Engineering Tables

Large

----------------------------

Archive Tables

Very Large

---

# Database Maintenance

Integrity Check

Analyze

Vacuum

Backup

Index Verification

Relationship Verification

Administrator configurable.

---

# Acceptance Criteria

✔ Complete database architecture documented

✔ Logical layering defined

✔ Foreign keys defined

✔ Primary keys standardized

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete system traceability

---

End of Document
