# Documentation/13_Database/DB-002_ImportHistory.md

Document ID : MTDMS-DB-002

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

The Import History table stores information about every TXT file imported into MTDMS.

This table does NOT store engineering data.

It stores only import metadata.

The original TXT file remains the master engineering record.

---

# Objectives

The table shall

• Identify every imported TXT file

• Prevent duplicate imports

• Preserve traceability

• Record import history

• Allow regeneration of reports from the original TXT

---

# Source

Only

TXT files exported from the testing machine.

No manual engineering data entry is permitted.

---

# Table Name

tblImportHistory

---

# Primary Key

ImportID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ImportID

Unique database identifier

INTEGER

----------------------------

ImportGUID

Global unique identifier

TEXT

UUID

----------------------------

OriginalFileName

Original TXT filename

TEXT

----------------------------

OriginalFolder

Folder containing TXT

TEXT

----------------------------

FullPath

Complete file path

TEXT

----------------------------

MachineName

Testing machine

TEXT

----------------------------

MachineModel

Machine model

TEXT

----------------------------

MachineSerial

Machine serial number

TEXT

----------------------------

TXTVersion

TXT format version

TEXT

----------------------------

ImportDate

Date imported

DATE

----------------------------

ImportTime

Time imported

TIME

----------------------------

Operator

Logged-in operator

TEXT

----------------------------

Workstation

Computer name

TEXT

----------------------------

WindowsUser

Windows account

TEXT

----------------------------

SoftwareVersion

MTDMS version

TEXT

----------------------------

TXTSize

File size

INTEGER

Bytes

----------------------------

TXT_SHA256

SHA256 checksum

TEXT

64 characters

----------------------------

TXT_MD5

Optional

TEXT

32 characters

----------------------------

ImportStatus

Success

Failed

Cancelled

TEXT

----------------------------

FailureReason

Optional

TEXT

----------------------------

DuplicateImport

BOOLEAN

----------------------------

OriginalImportID

Reference to first import

INTEGER

Nullable

----------------------------

Remarks

TEXT

Nullable

---

# Duplicate Detection

Before importing

↓

Calculate SHA256

↓

Search tblImportHistory

↓

Checksum exists

↓

Warning

↓

Operator chooses

Cancel

or

Import Again

If imported again

DuplicateImport = TRUE

OriginalImportID = previous record

---

# File Integrity

The SHA256 hash shall always be calculated before processing.

If the file changes

↓

New checksum

↓

New Import Record

---

# File Location

SQLite stores only

Reference

Never stores

TXT contents.

---

# Relationships

tblImportHistory

↓

1 : N

tblReport

↓

1 : N

tblArchive

↓

1 : N

tblAuditTrail

---

# Indexes

IX_SHA256

IX_FileName

IX_ImportDate

IX_Operator

IX_Machine

---

# Constraints

SHA256

UNIQUE

unless

DuplicateImport = TRUE

---

# Recovery

If report regeneration is required

↓

Locate original TXT

↓

Re-import

↓

Recalculate

↓

Generate new report

Engineering values are never recovered from SQLite.

---

# Audit Trail

Every import records

ImportID

Checksum

Operator

Machine

Timestamp

SoftwareVersion

---

# Acceptance Criteria

✔ Every TXT uniquely identified

✔ Duplicate detection

✔ SHA256 verification

✔ Original file preserved

✔ SQLite stores metadata only

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

---

End of Document
