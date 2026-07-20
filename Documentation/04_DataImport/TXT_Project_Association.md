# TXT Project Association

Document ID : MTDMS-IMP-026

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines how imported TXT files are associated with projects inside MTDMS.

Every imported test shall belong to exactly one project.

No imported data shall exist outside a project.

This guarantees complete traceability according to ISO/IEC 17025.

---

# Project Relationship

```
Project

│

├── Import Session

├── Raw Data

├── Engineering Data

├── Graphs

├── Reports

└── Audit Trail
```

---

# Import Workflow

Create Project

↓

Assign Project ID

↓

Import TXT

↓

Create Import Session

↓

Store Raw Data

↓

Engineering

↓

Reports

---

# Project ID

Generated automatically.

Format

```
YYYY-NNNNN
```

Example

```
2026-00015
```

Alternative

GUID

Future Version

---

# Import Session

Each TXT import creates

Import Session

Fields

Session ID

Project ID

TXT Filename

Import Date

Operator

Machine

Parser Version

Validation Result

Checksum

---

# One Project

May contain

One TXT

↓

Many Reports

↓

Many Graphs

↓

Many Calculations

---

# Multiple TXT Files

Current Version

Not Allowed

One Project

↓

One TXT

Future Version

Batch Import

Reserved

---

# Project Metadata

Stored

Project Name

Customer

Drawing Number

Batch Number

Heat Number

Material

Standard

Specimen

Operator

Machine

---

# SQLite Tables

```
tblProjects

tblImportSession

tblRawData

tblEngineering

tblGraphs

tblReports
```

---

# Project Folder

Logical Structure

```
Project

↓

Raw Data

↓

Engineering

↓

Graphs

↓

Reports

↓

Audit
```

Workbook stores only references.

---

# Import Lock

Once TXT imported

↓

Raw Data becomes

Read Only

Engineering data

May be recalculated

Raw data

Never modified

---

# Re-import

If operator imports again

↓

New Import Session

↓

Old Session preserved

↓

No overwrite

---

# Project History

Every import recorded

Import Number

Import Time

Operator

Workbook Version

Machine Profile

TXT Checksum

---

# Project Status

States

NEW

↓

TXT_IMPORTED

↓

ENGINEERING_READY

↓

GRAPH_READY

↓

REPORT_READY

↓

APPROVED

↓

ARCHIVED

---

# Approval

Future

Electronic Signature

Reviewer

Approval Date

Reserved

---

# Backup

Every Project

Included in

SQLite Backup

Workbook Backup

Audit Backup

---

# Project Recovery

If workbook damaged

↓

SQLite

↓

Restore Project

↓

Restore Import Session

↓

Restore Raw Data

Engineering recalculated automatically.

---

# Audit Trail

Stores

Project ID

Session ID

TXT Filename

Operator

Machine

Material

Standard

Date

Time

Validation

Checksum

---

# Acceptance Criteria

✔ Every TXT belongs to one Project

✔ No orphan imports

✔ Multiple import sessions preserved

✔ Raw Data immutable

✔ SQLite traceability

✔ ISO 17025 compliant

---

End of Document
