# TXT Version Detection Engine

Document ID : MTDMS-TXT-003

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

The Version Detection Engine identifies the exact structure and export format of every imported TXT file before parsing begins.

The purpose is to ensure that the correct parser is selected automatically without requiring user intervention.

The engine performs **no engineering calculations**.

---

# Design Principle

Every TXT file shall be identified before parsing.

The parser shall never assume that all TXT files have the same structure.

```
TXT File

↓

Version Detection

↓

Parser Selection

↓

Engineering Dataset
```

---

# Why Version Detection Is Required

Testing machine software evolves over time.

Changes may include

• New header fields

• Different separators

• Additional channels

• Modified column order

• Different unit names

• Different metadata blocks

Without version detection, the parser becomes unreliable.

---

# Detection Strategy

The engine shall identify the format using multiple independent indicators.

Priority:

1. Explicit software version
2. Export signature
3. Header keywords
4. Section layout
5. Column definitions
6. Statistical confidence

---

# Detection Sources

## 1. Software Name

Typical examples

```
TRAPEZIUM X

TRAPEZIUM Lite

Autograph

Autograph AGS-X

Autograph AG-X

Shimadzu
```

---

## 2. Software Version

Examples

```
Version 1.xx

Version 2.xx

Version 3.xx
```

The parser stores the complete version string.

---

## 3. Header Signature

Example

```
Exported by ...

Software ...

Machine ...

Date ...
```

The exact signature is stored for future compatibility.

---

## 4. File Layout

Detection based on

Number of header lines

Location of curve data

Section ordering

Presence of metadata blocks

---

## 5. Column Definition

Examples

```
Force

Extension

Stroke

Time

Stress

Strain
```

Channel order is analyzed before parsing.

---

# Detection Levels

Level 1

Exact Match

100%

---

Level 2

Compatible Match

95%

---

Level 3

Probable Match

80%

---

Level 4

Unknown

Manual confirmation required.

---

# Internal Version Identifier

Every supported layout receives an internal identifier.

Example

```
TXT-V1

TXT-V2

TXT-V3

TXT-CUSTOM
```

These identifiers are used internally.

They are independent from manufacturer version numbers.

---

# Unknown Files

If the version cannot be identified

↓

Unknown Layout

↓

Parser Disabled

↓

Diagnostic Report Generated

↓

User Notification

No engineering calculations begin.

---

# Parser Mapping

Example

```
TXT-V1

↓

Parser V1


TXT-V2

↓

Parser V2


TXT-V3

↓

Parser V3
```

The Calculation Engine is unaffected.

---

# SQLite Storage

SQLite records

Original File Name

Detected Version

Detection Confidence

Software Name

Software Version

Machine Model

Detection Timestamp

Operator

Import Result

---

# Administrator Options

Allow Unknown Layout

Default Parser

Strict Detection

Verbose Diagnostics

Future Version Learning

Administrator configurable.

---

# Diagnostics

Diagnostic information includes

Detected Signature

Unknown Keywords

Header Length

Column Count

Section Count

Confidence Score

Recommended Parser

---

# Future Compatibility

The engine shall support adding new versions without modifying existing parsers.

Only the mapping table requires updating.

---

# Engineering Independence

The Version Detection Engine

shall never

calculate

modify

interpret

engineering values.

Its responsibility ends after selecting the appropriate parser.

---

# Error Handling

No Signature

↓

Continue Detection

Multiple Matches

↓

Highest Confidence

Unknown Version

↓

Reject

Corrupted Header

↓

Abort

---

# Performance Targets

Version Detection

< 30 ms

Parser Selection

Immediate

SQLite Logging

< 10 ms

---

# Acceptance Criteria

✔ Automatic version detection

✔ Confidence evaluation

✔ Parser selection

✔ Unknown layout detection

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Future parser extensibility

✔ No engineering calculations

✔ Complete traceability to original TXT file

---

# Related Documents

TXT-001_Architecture

TXT-002_TXTFileStructure

TXT-004_FileEncoding

TXT-005_ParserEngine

TXT-016_EngineeringDatasetBuilder

---

End of Document
