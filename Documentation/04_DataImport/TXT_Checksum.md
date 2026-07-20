# TXT Checksum Specification

Document ID : MTDMS-IMP-043

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

This document defines how MTDMS generates, stores and validates checksums for every imported TXT file.

The checksum guarantees

- file integrity
- duplicate detection
- audit traceability
- protection against accidental modification

This mechanism is mandatory for ISO/IEC 17025 traceability.

---

# Philosophy

TXT File

↓

Checksum

↓

SQLite

↓

Future Verification

---

# Objectives

Detect duplicate imports.

Detect modified TXT files.

Verify archived projects.

Support future electronic signatures.

Provide immutable file identity.

---

# Checksum Algorithm

Current Version

```
SHA-256
```

Reason

Widely supported

Fast

Cryptographically secure

Stable

---

# Workflow

```
Select TXT

↓

Read Entire File

↓

Generate SHA-256

↓

Compare Database

↓

Duplicate?

↓

Store Checksum

↓

Continue Import
```

---

# Checksum Storage

SQLite Table

```
tblImportSession
```

Field

```
Checksum
```

Data Type

TEXT

Length

64 Characters

---

# Example

```
TXT

↓

SHA-256

↓

9D4C12B75C...

↓

SQLite
```

---

# Duplicate Detection

Comparison Keys

Checksum

Project

Machine

Import Date

---

# Rule

Same Project

+

Same SHA-256

↓

Duplicate Import

↓

Operator Warning

---

# Modified File Detection

Previous Import

↓

Checksum A

New Import

↓

Checksum B

If

```
A ≠ B
```

↓

File Modified

↓

Continue as New Session

---

# Import History

Each import session stores

ProjectID

SessionID

TXT Filename

Checksum

Timestamp

Operator

Workbook Version

Parser Version

---

# Integrity Verification

Operator may execute

```
Verify Import
```

Procedure

Read Archived TXT

↓

Generate SHA-256

↓

Compare SQLite

↓

Match

↓

PASS

Else

↓

FAIL

---

# Ribbon Commands

Import

Verify File

Show Checksum

Copy Checksum

---

# SQLite Tables

```
tblImportSession

tblAuditTrail
```

Audit stores

Checksum Generated

Checksum Verified

Verification Result

---

# Error Handling

Unable to generate checksum

↓

Critical Error

↓

Abort Import

↓

Rollback

---

# Performance

100 MB TXT

↓

SHA-256

Target

<1 Second

---

# Future Extensions

Digital Signature

Certificate Validation

Encrypted Archive

Cloud Verification

Blockchain

Reserved

---

# Security

Checksum

Never edited

Never recalculated

Except

Explicit Verification

---

# Acceptance Criteria

✔ SHA-256 implemented

✔ Duplicate detection supported

✔ File integrity verification

✔ SQLite storage

✔ Audit logging

✔ Excel 2019 compatible

✔ ISO 17025 traceability

---

End of Document
