# Customer Library

Document ID : MTDMS-DB-004

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

The Customer Library stores customer information used for report generation and document management.

The Customer Library contains administrative information only.

No engineering calculations are stored.

No engineering calculations are performed.

---

# Objectives

The Customer Library shall

• Store customer information

• Store customer specifications

• Store report preferences

• Store customer logos

• Store customer numbering rules

---

# Design Philosophy

TXT File

↓

Engineering Results

↓

Customer Information

↓

Report

Customer information is independent from engineering calculations.

---

# Table Name

tblCustomer

---

# Primary Key

CustomerID

INTEGER

AUTOINCREMENT

PRIMARY KEY

---

# Fields

CustomerID

INTEGER

----------------------------

CustomerCode

TEXT

Unique

----------------------------

CustomerName

TEXT

----------------------------

ShortName

TEXT

Nullable

----------------------------

CompanyType

TEXT

Examples

Manufacturer

Supplier

Contractor

Laboratory

Government

University

Private

----------------------------

Address

TEXT

----------------------------

City

TEXT

----------------------------

Country

TEXT

----------------------------

PostalCode

TEXT

----------------------------

Phone

TEXT

----------------------------

Email

TEXT

----------------------------

Website

TEXT

Nullable

----------------------------

ContactPerson

TEXT

----------------------------

Department

TEXT

Nullable

----------------------------

CustomerLogo

TEXT

File Path

----------------------------

DefaultTemplate

TEXT

----------------------------

DefaultLanguage

TEXT

----------------------------

DefaultPaperSize

TEXT

----------------------------

DefaultReportFormat

TEXT

----------------------------

SpecificationReference

TEXT

Nullable

----------------------------

Remarks

TEXT

Nullable

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

# Customer Categories

Steel Plant

Pipe Manufacturer

Spring Manufacturer

Automotive

Construction

Oil & Gas

Petrochemical

Power Plant

University

Research Center

Private Customer

Administrator configurable.

---

# Report Preferences

Each customer may define

Preferred Language

Preferred Report Template

Preferred Logo

Preferred Paper Size

Preferred Export Format

Preferred Acceptance Layout

---

# Engineering Independence

Customer information

shall never affect

Engineering Results

Material Calculations

Graph Calculations

Validation Results

Acceptance Results

---

# Customer Logo

Customer logo is optional.

If no logo exists

↓

Use Laboratory Default Logo.

---

# Customer Specifications

Optional

Each customer may define

Reference Standard

Acceptance Profile

Internal Specification

Project Specification

These references are informational.

Engineering validation uses the selected validation profile.

---

# SQLite Relationships

tblCustomer

↓

1 : N

tblReport

↓

1 : N

tblCertificate

↓

1 : N

tblExportHistory

---

# Indexes

IX_CustomerCode

IX_CustomerName

IX_ContactPerson

IX_CompanyType

---

# Constraints

CustomerCode

UNIQUE

CustomerName

Required

---

# Audit Trail

Store

Customer

Modification

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

Modify

Reviewer

Read

Operator

Read Only

---

# Error Handling

Duplicate CustomerCode

↓

Reject

Missing Customer Name

↓

Reject

Missing Logo

↓

Use Default Logo

Missing Template

↓

Use Default Template

---

# Acceptance Criteria

✔ Customer information stored

✔ Customer preferences supported

✔ Engineering calculations unaffected

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
