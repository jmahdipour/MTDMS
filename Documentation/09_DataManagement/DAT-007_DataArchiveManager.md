# Data Archive Manager

Document ID : MTDMS-DAT-007

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Data Management

Status

Production

---

# Purpose

The Data Archive Manager is responsible for the long-term storage, organization and retrieval of all engineering data generated within MTDMS.

Its purpose is to preserve laboratory records while maintaining complete traceability and ensuring that archived data can always be recovered without altering the original engineering information.

The Archive Manager never changes engineering calculations.

---

# Reference Standards

ISO/IEC 17025

ISO 9001

ISO 15489

ISO 14721 (OAIS Reference Model)

Recommended

---

# Objectives

The Archive Manager shall

• Preserve original exported files

• Preserve engineering results

• Preserve reports

• Preserve revision history

• Support long-term retrieval

• Prevent accidental deletion

• Support laboratory audits

---

# Archive Scope

Archived items include

Original Machine File

Imported Dataset

Normalized Dataset

Engineering Results

Graphs

PDF Reports

Certificates

Material Snapshot

Standard Snapshot

Revision History

Audit References

---

# Archive Workflow

```
Approved Report

↓

Archive Package

↓

Integrity Verification

↓

Archive Database

↓

Long-Term Storage

↓

Search

↓

Restore
```

---

# Archive Package

Each archive package contains

Original File

Engineering Dataset

Graphs

Report

PDF

Metadata

Checksums

Revision History

Archive Manifest

---

# Archive Identifier

Each archive receives

Archive ID

Archive Date

Certificate Number

Sample ID

Material

Revision

Checksum

Operator

---

# Archive Status

Pending

Archived

Verified

Restored

Locked

Destroyed (Logical Only)

---

# Archive Organization

Recommended Folder Structure

```
Archive

 ├── 2026

 │      ├── Tensile

 │      ├── Hardness

 │      ├── Impact

 │      ├── Spring

 │      ├── Ring Stiffness

 │      └── Other
```

Administrator configurable.

---

# Archive Naming

Recommended

```
CertificateNumber_Revision_Date.zip
```

Example

```
T-2026-00125_R03_20260720.zip
```

---

# Archive Database

SQLite

Tables

```
tblArchive

tblArchiveItem

tblArchiveHistory

tblArchiveRestore
```

---

# Archive Metadata

Archive ID

Certificate Number

Customer

Material

Standard

Test Type

Operator

Approval Date

Revision

Archive Date

Checksum

Storage Location

---

# Archive Integrity

Verification

SHA-256

File Count

Revision Count

Manifest

Database Reference

Verification required before storage.

---

# Search

Archive ID

Certificate Number

Sample ID

Material

Customer

Date

Operator

Test Type

Revision

---

# Restore

Supported

Complete Archive

Original File

Engineering Dataset

Report

PDF

Graph

Restore never overwrites existing data.

A restored copy creates

New Working Instance

---

# Retention Policy

Recommended

Engineering Records

10 Years Minimum

Calibration Records

According to Laboratory Policy

Administrator configurable.

---

# Deletion Policy

Physical deletion

Not Supported

Logical deletion only

Status becomes

Inactive

Archived records remain recoverable.

---

# Permissions

Administrator

Full Access

Quality Manager

Archive / Restore

Reviewer

Read

Operator

No Archive Access

---

# Audit Trail

Every archive operation records

Archive ID

User

Date

Time

Operation

Verification Status

Computer Name

Reason

---

# Error Handling

Archive Missing

↓

Warning

Checksum Failure

↓

Reject Restore

Manifest Missing

↓

Reject

Database Reference Missing

↓

Warning

---

# Future Enhancements

Cloud Archive

Optical Media Support

WORM Storage

Automatic OAIS Export

Long-Term Digital Preservation

Reserved

---

# Acceptance Criteria

✔ Original files preserved

✔ Long-term storage

✔ Searchable archive

✔ Restore supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
