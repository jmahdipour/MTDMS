# Multi-Language Report Engine

Document ID : MTDMS-RE-018

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

The Multi-Language Report Engine manages the generation of engineering reports in one or more languages from the same validated engineering dataset.

Unlike the Report Localization Engine, which translates a single report into a selected language, this engine can generate multiple language versions simultaneously.

The engine performs **no engineering calculations**.

---

# Objectives

The Multi-Language Report Engine shall

• Generate reports in multiple languages

• Preserve identical engineering values

• Maintain consistent formatting

• Support international customers

• Maintain complete engineering traceability

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Validated Results

↓

Language A

↓

Report A

+

↓

Language B

↓

Report B

+

↓

Language C

↓

Report C

Engineering values remain identical across every version.

---

# Workflow

```
Validated Engineering Report

↓

Selected Languages

↓

Translation Engine

↓

Generate Individual Reports

↓

Save
```

---

# Supported Modes

Single Language

Dual Language

Multiple Languages

Administrator configurable.

---

# Example Output

```
TR-2026-00125_EN.pdf

TR-2026-00125_FA.pdf

TR-2026-00125_AR.pdf
```

Each file represents the same engineering results.

---

# Language Independence

The following items remain unchanged in every version

Engineering Results

Graphs

Report Number

Certificate Number

Sample Data

Machine Data

Validation Results

Only language-dependent text changes.

---

# Right-to-Left Support

Automatically enabled for

Persian

Arabic

Supported adjustments

Text Direction

Paragraph Alignment

Table Direction

Header

Footer

Page Layout

Graphs retain the same engineering geometry.

---

# Language Selection

The operator may select

One Language

Multiple Languages

Default Laboratory Language

Customer Preferred Language

Administrator configurable.

---

# Translation Sources

SQLite Translation Dictionary

Laboratory Dictionary

Approved Engineering Terms

Customer Terminology (optional)

Administrator configurable.

---

# File Naming

Default

```
ReportNumber_LanguageCode

Example

TR-2026-00125_EN

TR-2026-00125_FA

TR-2026-00125_DE
```

Administrator configurable.

---

# Batch Generation

The engine supports simultaneous multilingual generation for multiple reports.

Example

100 reports

↓

English

↓

Persian

↓

Arabic

↓

300 generated documents

---

# Engineering Independence

The Multi-Language Report Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Each language version references the same engineering dataset.

---

# SQLite Interaction

SQLite stores

Language Definitions

Translation Dictionary

Preferred Customer Language

Generation History

Audit Information

---

# Error Handling

Missing Language

↓

Use Default

Missing Translation

↓

Fallback

Unsupported Language

↓

Reject

Translation Database Failure

↓

Abort

---

# Performance Targets

Single Language

< 500 ms

Three Languages

< 1.5 s

Batch Generation

Depends on report count

---

# Acceptance Criteria

✔ Multiple language reports

✔ Simultaneous generation

✔ RTL support

✔ Translation dictionary

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Complete traceability from TXT file

---

End of Document
