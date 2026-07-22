# Report Export Manager

Document ID : MTDMS-REP-020

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Reporting

Status

Production

---

# Purpose

The Report Export Manager is responsible for exporting completed reports from Excel into their final storage locations.

The module controls file generation and storage only.

It never performs engineering calculations.

It never modifies validated engineering data.

---

# Design Principles

One validated report

↓

One controlled export

↓

One archive record

All exported files shall be traceable.

---

# Objectives

The module shall

• Export Excel reports

• Export PDF reports

• Prevent accidental overwrite

• Store export history

• Preserve traceability

• Support configurable storage paths

---

# Workflow

```
Approved Report

↓

Export Request

↓

Report Export Manager

↓

Export Validation

↓

Generate Files

↓

Archive

↓

Log Export
```

---

# Supported Export Types

Excel Workbook

PDF

Print

Archive Copy

Future

CSV Summary

XML

JSON

---

# Excel Export

Default format

```
*.xlsx
```

Workbook shall remain editable according to worksheet protection rules.

---

# PDF Export

Generated from

Approved Excel Report

The PDF shall preserve

Formatting

Graphs

Page Layout

Page Numbers

---

# Export Locations

Supported

Project Folder

Archive Folder

Customer Folder

Temporary Folder

Administrator configurable.

---

# Default Directory Structure

```
Reports

│

├── 2026

│     ├── Excel

│     ├── PDF

│     └── Archive

│

├── 2027

│     ├── Excel

│     ├── PDF

│     └── Archive
```

---

# File Naming

Default

Excel

```
CertificateNumber_Revision.xlsx
```

PDF

```
CertificateNumber_Revision.pdf
```

Examples

```
T-2026-000124_R00.xlsx

T-2026-000124_R00.pdf
```

Administrator configurable.

---

# Duplicate File Protection

Before saving

Verify

File Exists

↓

Yes

↓

Append

Timestamp

or

Abort

according to configuration.

---

# Export Validation

Verify

Certificate Number

Revision

Approval Status

Report Complete

Graphs Present

Acceptance Present

---

# Export Rules

Only

Approved Reports

may be exported

to

Final Archive

Draft reports

may only be exported

to

Draft Folder

---

# Archive Copy

Every released report shall automatically create

Archive Copy

Archive copy is read-only.

---

# Folder Creation

If folder

does not exist

↓

Create Folder

↓

Continue

---

# Export Log

Every export records

File Name

Extension

Location

Certificate Number

Revision

Operator

Timestamp

Export Result

---

# SQLite Database

Tables

```
tblExportHistory

tblExportConfiguration

tblExportQueue

tblArchiveLocation
```

---

# Audit Trail

Record

Certificate Number

Revision

Excel File

PDF File

Destination

Operator

Timestamp

Computer Name

Software Version

---

# Permissions

Administrator

Configure

Quality Manager

Export

Reviewer

Export Draft

Operator

Generate Draft Only

---

# Error Handling

Destination Missing

↓

Create Folder

Disk Full

↓

Abort

Access Denied

↓

Abort

File Locked

↓

Retry

Export Failure

↓

Rollback

---

# Performance

Target

Excel Export

< 2 seconds

PDF Export

< 5 seconds

Standard Report

---

# Future Enhancements

Compressed Archive Package

Automatic Backup

Cloud Synchronization

Customer Portal Export

Reserved

---

# Acceptance Criteria

✔ Excel export

✔ PDF export

✔ Automatic archive copy

✔ Duplicate protection

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering values unchanged

✔ ISO/IEC 17025 compliant

✔ Complete export history

---

End of Document
