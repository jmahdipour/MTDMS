# TXT Import Version Compatibility

Document ID : MTDMS-IMP-049

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Module

Import Engine

Status

Production

---

# Purpose

This document defines how the Import Engine recognizes and supports different generations of TXT files produced by mechanical testing machines.

The compatibility layer allows MTDMS to import historical files without modifying the parser.

---

# Design Philosophy

Machine

↓

Version Detection

↓

Compatibility Layer

↓

Unified Parser

↓

Engineering Engine

The Engineering Engine shall never know which machine generated the file.

---

# Supported Manufacturers

Shimadzu

FATEK

Generic

Future

Instron

Zwick

MTS

Tinius Olsen

Reserved

---

# Compatibility Strategy

Every imported file receives

Machine Family

Machine Version

TXT Version

Parser Version

Compatibility Level

---

# Version Detection Priority

1

Embedded Version Number

↓

2

Machine Signature

↓

3

Header Layout

↓

4

Column Layout

↓

5

Automatic Pattern Recognition

---

# Compatibility Levels

## Level A

Fully Supported

No conversion required.

---

## Level B

Supported

Minor header conversion required.

---

## Level C

Supported

Column mapping required.

---

## Level D

Supported

Operator confirmation required.

---

## Level E

Unsupported

Import rejected.

---

# Shimadzu Compatibility

| Machine | TXT Version | Status |
|----------|-------------|--------|
| Trapezium X | 1.x | Supported |
| Trapezium X | 2.x | Supported |
| Autograph AG Series | Current | Supported |

---

# FATEK Compatibility

| Machine | Version | Status |
|----------|----------|--------|
| MTDMS PLC Export | 1.x | Supported |
| VS20NL-P1 | Current | Supported |

---

# Generic TXT

Requirements

Header

Force

Stroke

Time

Supported

Yes

---

# Version Mapping

Example

```
TXT Version

1.02

↓

Compatibility Layer

↓

Internal Version

Parser V3
```

---

# Parser Compatibility Matrix

| Parser | TXT Versions |
|----------|--------------|
| Parser V1 | Legacy |
| Parser V2 | Legacy + Current |
| Parser V3 | All Supported Versions |

Only the latest parser shall be distributed.

---

# Backward Compatibility

Older TXT

↓

Modern Parser

↓

Supported

No engineering difference allowed.

---

# Forward Compatibility

Unknown Future TXT

↓

Attempt Recognition

↓

Warning

↓

Operator Approval

↓

Import

or

Reject

---

# Compatibility Database

SQLite

```
tblImportCompatibility
```

Fields

Machine

TXTVersion

ParserVersion

CompatibilityLevel

Notes

Enabled

---

# Administrator Functions

Administrator may

Add Version

Disable Version

Edit Compatibility

Export Compatibility Table

Import Compatibility Table

No VBA source modification required.

---

# Audit Trail

Every import records

Detected Machine

Detected TXT Version

Parser Version

Compatibility Level

Operator Override

Timestamp

---

# Error Handling

Unknown Version

↓

Warning

↓

Attempt Generic Import

If impossible

↓

Abort Import

---

# Future Expansion

Automatic Internet Update

Machine Profile Download

Cloud Compatibility Database

Reserved

---

# Acceptance Criteria

✔ Legacy TXT supported

✔ Current TXT supported

✔ Version detection automatic

✔ Backward compatibility maintained

✔ SQLite configurable

✔ Excel 2019 compatible

✔ ISO 17025 traceability preserved

---

# Completion Status

After this document

**04_DataImport Module Status**

✅ Complete

Number of Documents

49

Next Module

```
05_Engineering
```

---

End of Document
