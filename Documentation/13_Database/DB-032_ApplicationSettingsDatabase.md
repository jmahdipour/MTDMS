# Application Settings Database

Document ID : MTDMS-DB-032

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

The Application Settings Database stores all configurable parameters used by the Excel application.

These settings define how the application behaves.

They never modify engineering calculations.

They never modify imported TXT files.

---

# Objectives

The Application Settings Database shall

• Store application preferences

• Store folder locations

• Store default options

• Support user customization

• Eliminate hardcoded values

---

# Design Philosophy

Application

↓

Read Settings

↓

Operate

↓

Engineering Calculation

Settings affect

application behavior only.

Engineering calculations remain unchanged.

---

# Table Name

tblApplicationSettings

---

# Primary Key

SettingID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

SettingID

INTEGER

----------------------------

SettingGroup

TEXT

Examples

General

Import

Export

Graph

Backup

Report

Archive

SQLite

System

----------------------------

SettingKey

TEXT

Unique

Examples

DefaultTXTFolder

DefaultReportFolder

AutoBackup

DefaultGraphStyle

CompanyName

LogoPath

AutoSave

SQLiteLocation

ArchiveFolder

PDFFolder

----------------------------

SettingValue

TEXT

----------------------------

ValueType

TEXT

Examples

String

Integer

Boolean

Real

Date

----------------------------

DefaultValue

TEXT

----------------------------

Editable

BOOLEAN

----------------------------

RequiresRestart

BOOLEAN

----------------------------

Description

TEXT

Nullable

----------------------------

CreatedDate

DATE

----------------------------

ModifiedDate

DATE

----------------------------

ModifiedBy

TEXT

---

# Typical Settings

Default TXT Folder

SQLite Folder

Backup Folder

Archive Folder

Report Folder

PDF Folder

Company Name

Company Logo

Auto Backup

Auto Save

Default Graph Style

Default Report Template

CSV Export Enabled

Mouse Coordinate Display

Yield Detection Mode

Administrator configurable.

---

# Folder Settings

TXT Folder

Archive Folder

Backup Folder

PDF Folder

Excel Report Folder

Temporary Folder

All folder locations

shall be configurable.

---

# Engineering Independence

Application settings

shall never modify

Imported TXT

Engineering Results

Validation Results

Graphs

Reports

except

presentation preferences.

---

# SQLite Relationships

tblApplicationSettings

↓

Referenced by

Import Engine

Export Engine

Report Engine

Graph Engine

Backup Engine

Archive Engine

Application Startup

---

# Indexes

IX_SettingGroup

IX_SettingKey

---

# Constraints

SettingKey

UNIQUE

SettingValue

Required

---

# Audit Trail

Store

Setting

Old Value

New Value

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Modify

Quality Manager

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Missing Setting

↓

Load Default Value

Invalid Folder

↓

Prompt User

Duplicate Key

↓

Reject

Invalid Value Type

↓

Reject

---

# Performance

Application settings loading

Target

< 50 ms

---

# Acceptance Criteria

✔ All settings configurable

✔ No hardcoded paths

✔ Default values supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability

---

End of Document
