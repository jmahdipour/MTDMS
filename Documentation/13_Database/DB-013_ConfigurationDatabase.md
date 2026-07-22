# Configuration Database

Document ID : MTDMS-DB-013

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

The Configuration Database stores all configurable system parameters used by MTDMS.

Configuration values control the behavior of the application.

They never modify engineering calculations.

They never overwrite imported TXT values.

---

# Objectives

The Configuration Database shall

• Store application settings

• Store default values

• Store user preferences

• Store report options

• Store graph options

• Store import options

• Support future expansion

---

# Design Philosophy

Configuration

↓

Application

↓

Engineering Workflow

Configuration controls

application behavior only.

Engineering calculations always use the imported TXT data.

---

# Table Name

tblConfiguration

---

# Primary Key

ConfigurationID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

ConfigurationID

INTEGER

----------------------------

Category

TEXT

Examples

General

Import

Calculation

Graph

Report

Export

Database

System

----------------------------

ParameterName

TEXT

----------------------------

ParameterValue

TEXT

----------------------------

ParameterType

TEXT

Examples

Integer

Real

Boolean

Text

Date

----------------------------

DefaultValue

TEXT

----------------------------

Description

TEXT

----------------------------

Editable

BOOLEAN

----------------------------

RestartRequired

BOOLEAN

----------------------------

Active

BOOLEAN

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

# Categories

General

Import

Graph

Calculation

Reporting

Export

Printing

Database

Archive

System

Administrator configurable.

---

# General Configuration Examples

Application Language

Default Folder

Default Template

Company Name

Laboratory Name

Paper Size

Default Printer

---

# Import Configuration Examples

TXT Encoding

Field Separator

Decimal Separator

Date Format

Automatic Duplicate Detection

Import Folder

---

# Graph Configuration Examples

Grid Visible

Legend Visible

Marker Size

Line Width

Graph Colors

Zoom Limits

---

# Report Configuration Examples

Default Logo

Header Height

Footer Height

Report Font

Table Style

Print Quality

---

# Export Configuration Examples

Default Excel Folder

Default PDF Folder

Archive Folder

Overwrite Policy

Automatic PDF Export

---

# Database Configuration Examples

SQLite Location

Automatic Backup

Backup Folder

Retention Period

Database Version

---

# Engineering Independence

Configuration values

shall never

change

Imported Measurements

Engineering Results

Validation Results

Acceptance Results

---

# SQLite Relationships

tblConfiguration

↓

Independent

Referenced by

All application modules

---

# Indexes

IX_Category

IX_ParameterName

---

# Constraints

Category

Required

ParameterName

Required

ParameterName

Unique within Category

---

# Audit Trail

Store

Category

Parameter

Old Value

New Value

Operator

Timestamp

Computer

Software Version

---

# Permissions

Administrator

Create

Modify

Delete

Quality Manager

Modify Approved Parameters

Reviewer

Read

Operator

Read Only

---

# Error Handling

Unknown Parameter

↓

Use Default Value

Missing Configuration

↓

Restore Default

Invalid Type

↓

Reject

Corrupted Value

↓

Restore Default

---

# Configuration Backup

Every configuration change

shall automatically create

a backup copy

before saving.

---

# Acceptance Criteria

✔ Central configuration storage

✔ Default value support

✔ Automatic fallback

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
