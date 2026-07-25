# TXT File Encoding Engine

Document ID : MTDMS-TXT-004

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

The File Encoding Engine detects and decodes the character encoding of the imported TXT file before parsing begins.

Its objective is to guarantee that every character, engineering symbol, unit, decimal separator, and multilingual field is interpreted correctly regardless of the computer that generated the file.

The engine performs **no engineering calculations**.

---

# Design Philosophy

The parser must always receive correctly decoded text.

```
TXT File

↓

Encoding Detection

↓

Character Conversion

↓

Parser

↓

Engineering Dataset
```

The parser shall never work directly on raw byte streams.

---

# Why Encoding Detection Is Required

Different testing software and Windows installations may export TXT files using different encodings.

Typical differences include

• ANSI code pages

• UTF-8

• UTF-16 Little Endian

• UTF-16 Big Endian

• UTF-8 with BOM

• UTF-8 without BOM

Without correct decoding

- Engineering symbols may be corrupted.
- Material names may become unreadable.
- Persian or Arabic text may be lost.
- Degree symbols and unit symbols may be invalid.

---

# Supported Encodings

Current version

UTF-8

UTF-8 BOM

UTF-16 LE

UTF-16 BE

ANSI

Windows-1252

Windows-1256

Administrator configurable.

Future

ISO-8859

Shift-JIS

GB2312

UTF-32

---

# Detection Workflow

```
Read First Bytes

↓

Check BOM

↓

Known Encoding?

↓

YES

↓

Decode

↓

Parser


NO

↓

Heuristic Detection

↓

Confidence

↓

Decode

↓

Parser
```

---

# BOM Detection

Supported signatures

UTF-8 BOM

EF BB BF

----------------------------

UTF-16 LE

FF FE

----------------------------

UTF-16 BE

FE FF

----------------------------

UTF-32

Future support

---

# Heuristic Detection

If no BOM exists

The engine evaluates

Printable Characters

Invalid Byte Sequences

Control Characters

Language Distribution

Confidence Score

---

# Language Detection

Optional

English

Persian

Arabic

Mixed

Administrator configurable.

This information is used only to improve decoding.

---

# Character Normalization

After decoding

The engine normalizes

CR

LF

CRLF

Tab

Multiple Spaces

Non-breaking Space

Unicode Quotes

Unicode Minus

Administrator configurable.

---

# Engineering Symbols

The engine preserves

°

μ

µ

%

‰

×

±

≤

≥

Ω

N

MPa

GPa

mm

kN

These symbols must never be replaced.

---

# Decimal Separators

Supported

.

,

Localization occurs later.

Raw values remain unchanged.

---

# Line Ending Support

Windows

CRLF

Unix

LF

Classic Mac

CR

All are accepted.

---

# Maximum File Size

Recommended

500 MB

Larger files are supported through streaming mode.

---

# Memory Strategy

The engine shall avoid loading very large TXT files entirely into memory.

Preferred architecture

```
Stream Reader

↓

Decode

↓

Buffer

↓

Parser
```

---

# SQLite Logging

SQLite stores

Detected Encoding

Detection Confidence

Normalization Applied

Import Timestamp

Operator

Import Result

---

# Administrator Configuration

Preferred Encoding

Strict BOM Check

Automatic Detection

Fallback Encoding

Maximum File Size

Streaming Buffer Size

---

# Engineering Independence

The Encoding Engine

shall never

interpret

calculate

validate

engineering values.

Its responsibility ends after producing correctly decoded text.

---

# Error Handling

Unknown Encoding

↓

Fallback

Invalid UTF Sequence

↓

Replace Character

Corrupted BOM

↓

Ignore

Unreadable File

↓

Abort

---

# Performance Targets

Encoding Detection

< 20 ms

Character Normalization

< 50 ms

Streaming Decode

Real Time

---

# Acceptance Criteria

✔ Automatic encoding detection

✔ BOM detection

✔ UTF support

✔ ANSI support

✔ Unicode preservation

✔ Engineering symbols preserved

✔ Streaming capable

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No engineering calculations

---

# Related Documents

TXT-001_Architecture

TXT-002_TXTFileStructure

TXT-003_VersionDetection

TXT-005_ParserEngine

TXT-016_EngineeringDatasetBuilder

---

End of Document
