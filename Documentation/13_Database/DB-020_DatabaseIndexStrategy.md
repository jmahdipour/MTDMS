# Database Index Strategy

Document ID : MTDMS-DB-020

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

This document defines the indexing strategy used by the MTDMS SQLite database.

Indexes are used to improve

Search

Filtering

Sorting

Relationship performance

Report generation

Indexes never modify engineering data.

---

# Objectives

The indexing strategy shall

• Improve query performance

• Improve report generation speed

• Reduce search time

• Support large databases

• Preserve SQLite integrity

---

# Design Philosophy

TXT

↓

Import

↓

Engineering Calculation

↓

SQLite

↓

Indexed Search

Indexes improve access speed only.

Engineering calculations remain unchanged.

---

# Index Categories

Primary Key Indexes

Unique Indexes

Foreign Key Indexes

Search Indexes

Composite Indexes

---

# Primary Key Indexes

Every table

shall have

AUTOINCREMENT PRIMARY KEY

SQLite automatically creates

PRIMARY KEY index.

---

# Unique Indexes

Examples

MaterialCode

CustomerCode

MachineCode

OperatorCode

CertificateNumber

ReportNumber

ArchiveNumber

TemplateCode

---

# Foreign Key Indexes

Every Foreign Key

shall have

its own index.

Examples

ImportID

ReportID

CustomerID

MaterialID

MachineID

OperatorID

StandardID

CertificateID

---

# Search Indexes

Frequently searched fields

shall be indexed.

Examples

IssueDate

CustomerName

MachineName

MaterialName

OperatorName

ApprovalStatus

ArchiveDate

ImportDate

---

# Composite Indexes

Examples

CustomerID

+

IssueDate

----------------------------

MaterialID

+

StandardID

----------------------------

MachineID

+

ImportDate

----------------------------

ApprovalStatus

+

IssueDate

---

# Recommended Indexes

tblImportHistory

SHA256

ImportDate

MachineID

OperatorID

---

tblReport

CertificateNumber

CustomerID

MaterialID

IssueDate

ApprovalStatus

---

tblCertificate

CertificateNumber

IssueDate

CustomerID

---

tblArchive

ArchiveNumber

ArchiveDate

ReportID

---

tblAuditTrail

EventDate

OperatorID

Module

Action

---

tblValidation

ValidationDate

ReportID

ValidationStatus

---

# SQLite Performance Rules

Do not create

duplicate indexes.

Do not index

low-selectivity fields

unless frequently searched.

---

# Engineering Independence

Indexes

never

modify

Engineering Results

TXT Files

Engineering Tables

Graph Data

Indexes improve

retrieval only.

---

# Rebuild Index

Supported

Manual

Automatic

After major import

Administrator configurable.

---

# Analyze Database

SQLite

ANALYZE

may be executed

after large imports.

Improves query planner performance.

---

# Vacuum

Supported

Administrator configurable.

Recommended

after

large archive cleanup.

---

# Error Handling

Index Missing

↓

Create Index

Duplicate Index

↓

Ignore

Index Corruption

↓

Rebuild

Database Locked

↓

Retry

---

# Performance Targets

Certificate Search

< 100 ms

Customer Search

< 100 ms

Archive Search

< 200 ms

Import Search

< 100 ms

Report Search

< 100 ms

---

# Acceptance Criteria

✔ Primary key indexes

✔ Unique indexes

✔ Foreign key indexes

✔ Composite indexes

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Optimized query performance

---

End of Document
