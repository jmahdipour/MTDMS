# Standard Library Integration

Document ID : MTDMS-IMP-022

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines how the TXT Import System communicates with the Standard Library.

The Standard Library determines which engineering calculations, acceptance criteria, report templates and graph correction methods shall be used.

The TXT parser identifies the testing standard only.

The Engineering Engine executes the required calculations.

---

# Architecture

TXT

↓

Standard Name

↓

Standard Library

↓

Calculation Profile

↓

Engineering Engine

↓

Report Engine

---

# Objectives

Automatically identify the testing standard.

Load calculation rules.

Load report template.

Load graph correction parameters.

Prevent operator mistakes.

Maintain ISO 17025 compliance.

---

# Standard Recognition

Priority

1

Standard Code

↓

2

Alias

↓

3

Keyword Search

↓

4

Operator Selection

---

# Supported Standards

## Tensile

ISO 6892-1

ISO 6892-2

ASTM E8

ASTM A370

INSO 3132

---

## Structural Steel

ISO 630

ASTM A36

ASTM A572

EN 10025

---

## Fasteners

ISO 898

ASTM F568

---

## Bending

ASTM E290

ISO 7438

---

## Spring

DIN 2095

ISO 2162

---

## Ring Stiffness

ISO 9969

ASTM D2412

---

## Compression

ASTM E9

ISO 7500

---

# SQLite Table

```
tblStandards
```

Fields

Standard ID

Standard Name

Alias

Category

Calculation Profile

Report Template

Active

Revision

---

# Alias Table

```
tblStandardAlias
```

Examples

```
ISO6892

↓

ISO 6892-1
```

```
ISO-6892

↓

ISO 6892-1
```

```
ASTM E8M

↓

ASTM E8
```

---

# Calculation Profile

Each standard loads

Calculation Method

Yield Method

Young's Modulus Method

Elongation Method

Acceptance Limits

Graph Correction Method

CSV Export Rules

---

# Example

ISO 6892-1

↓

Yield

Rp0.2

↓

Young's Modulus

Elastic Linear Regression

↓

Elongation

After Fracture

↓

Graph Correction

Enabled

---

# Engineering Parameters Loaded

Elastic Region Rules

Proof Stress Rules

Yield Detection Rules

Fracture Rules

Reporting Rules

Acceptance Rules

---

# Report Template

Each standard selects

Default Report

Example

ISO 6892

↓

ISO6892_Report.dotx

ASTM E8

↓

ASTME8_Report.dotx

---

# CSV Export

Each standard defines

Column Order

Units

Precision

Decimal Separator

Header

Footer

---

# Unknown Standard

Unknown Standard

↓

Warning

↓

Operator Selection

↓

Continue

All overrides logged.

---

# Revision Control

Each standard contains

Revision

Publication Date

Replacement Standard

Obsolete Flag

---

# Future Standards

ISO

ASTM

DIN

JIS

BS

GOST

API

ASME

AWS

Automatically expandable.

---

# Logging

Store

Original Standard

Matched Standard

Calculation Profile

Operator Override

Timestamp

---

# Acceptance Criteria

✔ Automatic standard recognition

✔ Alias support

✔ SQLite compatible

✔ Automatic calculation profile loading

✔ Automatic report template selection

✔ Complete audit trail

---

End of Document
