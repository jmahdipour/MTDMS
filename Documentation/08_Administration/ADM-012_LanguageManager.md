# Language Manager

Document ID : MTDMS-ADM-012

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Administration

Status

Production

---

# Purpose

The Language Manager provides multilingual support throughout MTDMS.

Its responsibility is to translate user interface elements, report labels, messages and documentation without affecting engineering calculations or stored measurement data.

All engineering values remain language-independent.

---

# Objectives

The Language Manager shall

• Support multiple interface languages

• Support multilingual reports

• Separate language resources from source code

• Allow future language expansion

• Preserve engineering terminology

---

# Supported Languages

Persian (Default)

English

Future

Arabic

Turkish

French

German

Russian

Administrator configurable.

---

# Scope

The Language Manager controls

Menus

Ribbon Labels

Buttons

Dialogs

Messages

Warnings

Tooltips

Reports

Templates

PDF Labels

Help System

It shall **not** translate

Database field names

Engineering constants

Material IDs

Certificate IDs

Audit IDs

Internal table names

---

# Architecture

```
Application

↓

Language Manager

↓

Resource Dictionary

↓

Translated Interface

↓

User
```

---

# Language Resources

Each language resource contains

Language ID

Language Name

Version

Revision

Translation Status

Author

Approval Status

---

# Translation Dictionary

Each dictionary entry contains

Resource Key

English Text

Persian Text

Description

Category

Version

Example

```
BTN_IMPORT

Import

ورود اطلاعات
```

---

# Resource Categories

Ribbon

Forms

Menus

Buttons

Messages

Warnings

Errors

Reports

Templates

Graphs

Status Bar

Help

---

# Runtime Translation

Application Startup

↓

Load Language

↓

Load Dictionary

↓

Replace Resource Keys

↓

Display Interface

No application restart required
(optional implementation).

---

# Report Translation

Report labels

may be

Persian

English

Bilingual

Administrator configurable.

Engineering values remain unchanged.

---

# User Language

Each user may select

Preferred Language

stored in

User Profile.

If not defined

↓

System Default

---

# Font Management

Persian

Noto Sans

Tahoma

B Nazanin

Administrator configurable.

English

Calibri

Arial

Segoe UI

---

# Right-to-Left Support

Supported

Ribbon

Forms

Reports

PDF

Graphs (labels only)

---

# Missing Translation

If a resource is missing

↓

Use Default Language

↓

Log Warning

Application shall continue.

---

# SQLite Database

Tables

```
tblLanguage

tblTranslation

tblResourceCategory
```

---

# Import

Supported

Excel

CSV

SQLite

Future

JSON

XML

---

# Export

Excel

CSV

Translation Package

---

# Audit Trail

Every translation modification records

Resource Key

Old Text

New Text

User

Date

Time

Reason

---

# Permissions

Administrator

Full Access

Translator

Modify Translation

Operator

Read Only

---

# Validation Rules

Duplicate Resource Key

↓

Reject

Missing Translation

↓

Warning

Invalid Language

↓

Use Default

---

# Future Enhancements

Automatic Language Detection

Online Translation Repository

Customer Language Packs

AI Translation Assistant

Reserved

---

# Acceptance Criteria

✔ Multilingual interface

✔ Multilingual reports

✔ RTL support

✔ Translation dictionary

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering independent

✔ Full audit trail

---

End of Document
