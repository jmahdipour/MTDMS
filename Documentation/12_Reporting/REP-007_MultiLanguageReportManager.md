# Multi-Language Report Manager

Document ID : MTDMS-REP-007

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

The Multi-Language Report Manager enables the generation of laboratory reports in multiple languages while preserving identical engineering data.

Only report text changes.

Engineering calculations remain identical.

Graphs remain identical.

Numerical values remain identical.

---

# Objectives

The module shall

• Support multiple languages

• Keep engineering data identical

• Translate report labels

• Translate fixed report text

• Support customer language selection

• Support future language expansion

---

# Supported Languages

Persian

English

Arabic

Turkish

Russian

French

German

Administrator configurable.

---

# Language Architecture

```
Engineering Data

↓

Language Manager

↓

Language Dictionary

↓

Report Template

↓

Report Engine

↓

Output
```

---

# Translation Scope

Translate

Titles

Headers

Footers

Table Names

Column Names

Units (Display)

Comments

Acceptance Text

Warnings

Static Notes

---

# Non-Translated Content

Never translated

Engineering Values

Certificate Number

Revision

Sample ID

Heat Number

Material Grade

Measured Values

Graph Coordinates

Archive ID

Software Version

---

# Language Files

Each language contains

Language ID

Language Name

Version

Dictionary

Template Mapping

Date Format

Number Format

---

# Language Dictionary

Each entry contains

Key

Persian

English

Arabic

French

German

Description

---

# Template Mapping

Each language may use

Independent Report Template

or

Shared Template

Administrator configurable.

---

# Text Direction

Supported

Left-to-Right

English

French

German

Right-to-Left

Persian

Arabic

Automatic according to selected language.

---

# Font Management

Each language defines

Primary Font

Secondary Font

Fallback Font

Missing fonts generate warnings.

---

# Date Format

Examples

Persian Calendar

Gregorian Calendar

Administrator configurable.

Dates remain internally unchanged.

---

# Number Format

Supports

Decimal Separator

Thousands Separator

Digit Style

Engineering values remain unchanged.

---

# Units

Engineering units

remain identical.

Only captions may be translated.

Example

```
Yield Strength

↓

تنش تسلیم

↓

Limite d'élasticité
```

Value

```
355 MPa
```

never changes.

---

# Customer Language

Default language may be selected

Per Customer

Per Project

Per Report

Administrator configurable.

---

# Missing Translation

If translation does not exist

↓

Fallback

English

↓

Log Warning

---

# SQLite Database

Tables

```
tblLanguage

tblLanguageDictionary

tblLanguageHistory

tblLanguageTemplate
```

---

# Audit Trail

Store

Language

Template

Certificate Number

Revision

Operator

Timestamp

Software Version

---

# Permissions

Administrator

Manage Languages

Quality Manager

Approve

Reviewer

Generate

Operator

Select Available Language

---

# Error Handling

Missing Dictionary

↓

Fallback Language

Missing Template

↓

Abort

Missing Font

↓

Warning

Unsupported Language

↓

Default Language

---

# Future Enhancements

Automatic Translation

AI Translation Verification

Customer Translation Packs

Online Dictionary Update

Reserved

---

# Acceptance Criteria

✔ Multiple languages supported

✔ Engineering values unchanged

✔ Independent templates supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

✔ Complete language traceability

---

End of Document
