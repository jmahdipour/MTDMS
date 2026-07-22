# Template Library

Document ID : MTDMS-DB-012

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

The Template Library manages all report templates used by MTDMS.

Templates define the visual appearance of reports only.

Templates never contain engineering calculations.

Templates never modify engineering values.

---

# Objectives

The Template Library shall

• Store report templates

• Support multiple layouts

• Support customer-specific templates

• Support standard-specific templates

• Preserve version history

• Prevent template duplication

---

# Design Philosophy

TXT

↓

Engineering Calculation

↓

Validated Results

↓

Report Template

↓

Final Report

Templates affect presentation only.

Engineering data remains unchanged.

---

# Table Name

tblTemplate

---

# Primary Key

TemplateID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

TemplateID

INTEGER

----------------------------

TemplateCode

TEXT

Unique

----------------------------

TemplateName

TEXT

----------------------------

TemplateVersion

TEXT

----------------------------

TemplateType

TEXT

Examples

General

Customer

Standard

Internal

Calibration

----------------------------

CustomerID

INTEGER

Nullable

Foreign Key

tblCustomer

----------------------------

StandardID

INTEGER

Nullable

Foreign Key

tblStandard

----------------------------

WorkbookTemplate

TEXT

Path

----------------------------

LogoPath

TEXT

Nullable

----------------------------

HeaderLayout

TEXT

----------------------------

FooterLayout

TEXT

----------------------------

GraphLayout

TEXT

----------------------------

PaperSize

TEXT

Examples

A4

Letter

Legal

----------------------------

Orientation

TEXT

Portrait

Landscape

----------------------------

Language

TEXT

----------------------------

DefaultTemplate

BOOLEAN

----------------------------

Active

BOOLEAN

----------------------------

Remarks

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

# Template Types

General Laboratory

Customer Template

Project Template

Standard Template

Internal Template

Administrator configurable.

---

# Template Usage

Selected

before

report generation.

Changing templates

does not

recalculate engineering data.

---

# Workbook Template

Each template may define

Worksheet Layout

Header

Footer

Margins

Named Ranges

Company Logo

Graph Position

Fonts

Colors

---

# Engineering Independence

Templates

shall never

modify

Engineering Results

Graphs

Acceptance

Validation

Material Properties

---

# Template Versioning

Every template has

Version

Revision

Modification Date

Previous versions remain archived.

---

# SQLite Relationships

tblTemplate

↓

N : 1

tblCustomer

↓

N : 1

tblStandard

↓

1 : N

tblReport

---

# Indexes

IX_TemplateCode

IX_TemplateName

IX_TemplateVersion

IX_Customer

IX_Standard

---

# Constraints

TemplateCode

UNIQUE

TemplateVersion

Required

WorkbookTemplate

Required

---

# Audit Trail

Store

Template

Version

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

Approve

Reviewer

Read

Operator

Read Only

---

# Error Handling

Missing Workbook Template

↓

Abort

Missing Logo

↓

Use Default Logo

Duplicate Template

↓

Reject

Invalid Version

↓

Reject

---

# Performance

Template loading

Target

< 1 second

---

# Acceptance Criteria

✔ Multiple templates supported

✔ Customer templates supported

✔ Standard templates supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
