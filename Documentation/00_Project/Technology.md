# Technology Specification

Document ID: MTDMS-TECH-001

Version: 0.1.0

Status: Draft

---

# 1. Purpose

This document defines the technologies approved for the development of the Mechanical Testing Data Management System (MTDMS).

No technology outside this document may be used without approval.

---

# 2. Development Platform

Application

Microsoft Excel 2019

Architecture

Desktop

Operating System

Windows 10

Windows 11

Supported Office

Excel 2019

Preferred

64-bit Office

---

# 3. Programming Language

Language

Visual Basic for Applications

(VBA)

Required

YES

Visual Studio

NO

VB.NET

NO

C#

NO

Python Runtime

NO

Java

NO

---

# 4. User Interface

Technology

Ribbon XML

Mandatory

YES

UserForms

NOT ALLOWED

ActiveX Controls

NOT ALLOWED

Custom Task Pane

Future Version

---

# 5. Input Data

Supported

TXT

Encoding

UTF-8

ANSI

Windows-1252

Line Ending

CRLF

File Extension

.txt

Other Formats

Not Supported

CSV

Excel

XML

JSON

PDF

---

# 6. Database

Primary Database

SQLite

Database File

MTDMS.db

Driver

SQLite3

Connection

Embedded

Network Database

Future

SQL Server

Future

PostgreSQL

Future

---

# 7. Report Engine

Output

Excel

PDF

Printer

Technology

Native Excel Objects

PDF Export

ExportAsFixedFormat

---

# 8. Graph Engine

Technology

Native Excel Chart Object

Supported

Stress–Strain

Force–Stroke

Load–Displacement

Features

Zoom

Pan

Crosshair

Yield Marker

Fracture Marker

Graph Correction

Export

---

# 9. Engineering Engine

Calculations performed in VBA

No worksheet formulas shall contain engineering logic.

Worksheet formulas are limited to presentation only.

---

# 10. Ribbon Communication

Ribbon

↓

Callback

↓

Controller

↓

Service Module

↓

Calculation Module

↓

Database

The Ribbon shall never communicate directly with worksheets.

---

# 11. File Structure

Workbook

WorkbookTemplate.xlsm

Ribbon

customUI.xml

Database

MTDMS.db

Configuration

Settings Sheet

TXT Samples

TXT Folder

Documentation

Markdown

---

# 12. External Libraries

Approved

SQLite DLL

Optional

Windows API

Optional

Forbidden

COM Automation Libraries

Office Add-ins

Third-party Ribbon Libraries

Internet Dependencies

Cloud SDKs

---

# 13. Version Control

Git

GitHub

Branch Strategy

Git Flow

Main Branch

main

Development Branch

develop

Feature Branch

feature/*

Release Branch

release/*

Hotfix

hotfix/*

---

# 14. Coding Convention

Language

English

Comments

English

Variable Names

camelCase

Procedure Names

PascalCase

Module Names

PascalCase

Constants

UPPER_CASE

---

# 15. Performance Requirements

TXT Import

100000 rows

< 5 seconds

Graph Refresh

< 1 second

Database Search

< 1 second

Report Generation

< 3 seconds

---

# 16. Security

Offline Operation

YES

Internet Required

NO

Administrator Settings

YES

User Settings

YES

Audit Log

YES

Error Log

YES

---

# 17. Future Technologies

VB.NET Service

Optional

REST API

Optional

Cloud Backup

Optional

Machine Learning

Optional

Web Dashboard

Optional

---

# 18. Technology Rules

✔ Excel 2019 Only

✔ VBA Only

✔ Ribbon XML Only

✔ SQLite Only

✔ TXT Only

✔ Native Excel Charts

✘ UserForms

✘ ActiveX

✘ External Office Add-ins

✘ Cloud Dependencies

✘ Internet Requirement

---

End of Document
