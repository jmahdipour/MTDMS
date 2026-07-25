# Report Localization Engine

Document ID : MTDMS-RE-017

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Primary Data Source

TXT File (Testing Machine Export)

Application

MTDMS

Status

Production

---

# Purpose

The Report Localization Engine generates engineering reports in different languages while preserving identical engineering values, formatting, and traceability.

Only the report text changes.

Engineering calculations and engineering results remain unchanged.

---

# Objectives

The Report Localization Engine shall

• Support multilingual reports

• Preserve engineering terminology

• Maintain engineering consistency

• Support customer language requirements

• Preserve report integrity

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Localization

↓

Engineering Report

Only language changes.

Engineering values remain identical.

---

# Supported Languages

English

Persian (فارسی)

Arabic

French

German

Russian

Administrator configurable.

---

# Workflow

```
Validated Report

↓

Select Language

↓

Load Translation Dictionary

↓

Replace Text

↓

Generate Localized Report
```

---

# Localized Elements

Report Title

Headings

Table Headers

Section Names

Units (when required)

Approval Labels

Remarks

Footer

Administrator configurable.

---

# Non-Localized Elements

Engineering Values

Graphs

Report Number

Certificate Number

Dates (optional)

Machine Data

Sample Data

Engineering calculations

These remain identical in every language.

---

# Engineering Terminology

The translation dictionary shall preserve standardized engineering terminology.

Examples

Yield Strength

Ultimate Tensile Strength

Young's Modulus

Engineering Strain

True Stress

Fracture

Spring Constant

Ring Stiffness

Translations are administrator controlled.

---

# Right-to-Left Support

Supported for

Persian

Arabic

The report engine automatically adjusts

Text Direction

Alignment

Table Layout

Header

Footer

Graph labels remain unchanged unless translated.

---

# Date Format

Supported

ISO

Gregorian

Local Format

Administrator configurable.

---

# Number Format

Supported

Decimal Point

Decimal Comma

Digit Grouping

Administrator configurable.

Engineering precision is unchanged.

---

# Translation Dictionary

SQLite stores

Original Text

Translated Text

Language

Revision

Approval

Administrator configurable.

---

# Missing Translation

If a translation is unavailable

↓

Use Default Language

↓

Record Warning

---

# Engineering Independence

The Report Localization Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Only report text is translated.

---

# SQLite Interaction

SQLite stores

Translation Dictionary

Language Settings

Localization History

Administrator Changes

Audit Information

---

# Error Handling

Missing Language

↓

Use Default

Missing Translation

↓

Fallback

Invalid Dictionary

↓

Reject

---

# Performance Targets

Language Switch

< 100 ms

Localized Report

< 500 ms

Translation Lookup

Immediate

---

# Acceptance Criteria

✔ Multiple languages supported

✔ Engineering terminology preserved

✔ RTL support

✔ Translation dictionary

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
