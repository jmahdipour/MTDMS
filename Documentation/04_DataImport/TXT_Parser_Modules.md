# TXT Parser Modules

Document ID : MTDMS-IMP-013

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

---

# Purpose

This document defines the internal modules of the TXT Import System.

Each module has a single responsibility.

No module shall perform work belonging to another module.

---

# Architecture

```
TXT Import System

│

├── ImportController

├── TXTFileReader

├── TXTEncodingDetector

├── TXTHeaderParser

├── TXTColumnDetector

├── TXTUnitDetector

├── TXTValidator

├── TXTNormalizer

├── TXTRawStorage

├── TXTSessionManager

├── TXTPerformanceMonitor

├── TXTLogger

└── ImportResultBuilder
```

---

# Module 1

ImportController

Purpose

Main coordinator.

Responsibilities

Receive Ribbon command

Call parser modules

Return ImportResult

Refresh Ribbon

Allowed Calls

All parser modules

Not Allowed

Engineering calculations

Worksheet editing

Report generation

---

# Module 2

TXTFileReader

Purpose

Read TXT file.

Responsibilities

Open file

Read entire file

Detect file size

Return String Array

Output

```
String()
```

---

# Module 3

TXTEncodingDetector

Purpose

Determine encoding.

Supported

UTF-8

ANSI

UTF-16

Output

Encoding Type

---

# Module 4

TXTHeaderParser

Purpose

Read metadata.

Reads

Machine

Operator

Material

Specimen

Area

Gauge Length

Standard

Date

Units

Output

Header Object

---

# Module 5

TXTColumnDetector

Purpose

Locate engineering columns.

Recognizes

Time

Force

Stroke

Extension

Stress

Strain

Temperature

Output

Column Dictionary

---

# Module 6

TXTUnitDetector

Purpose

Detect engineering units.

Recognizes

Force

Length

Stress

Time

Temperature

Output

Conversion Factors

---

# Module 7

TXTValidator

Purpose

Validate everything.

Checks

Header

Columns

Units

Rows

Values

Duplicates

Engineering Consistency

Output

Validation Result

---

# Module 8

TXTNormalizer

Purpose

Normalize imported data.

Operations

Decimal normalization

Unit conversion

Column ordering

Data cleanup

Output

Normalized Records

---

# Module 9

TXTRawStorage

Purpose

Store imported records.

Destination

```
tblRawData
```

Also stores

Import Session ID

Import Timestamp

TXT Filename

Operator

---

# Module 10

TXTSessionManager

Purpose

Manage import session.

Stores

Session ID

Project ID

Workbook

Machine

Material

Import State

---

# Module 11

TXTPerformanceMonitor

Purpose

Measure execution time.

Records

Open Time

Read Time

Validation Time

Storage Time

Total Import Time

---

# Module 12

TXTLogger

Purpose

Write logs.

Writes

Import Log

Validation Log

Performance Log

Error Log

SQLite Log

---

# Module 13

ImportResultBuilder

Purpose

Create ImportResult object.

Contains

Status

Rows

Warnings

Errors

Duration

Header

Units

Session

Returned to

RibbonController

---

# Module Communication

```
ImportController

↓

TXTFileReader

↓

TXTHeaderParser

↓

TXTColumnDetector

↓

TXTUnitDetector

↓

TXTValidator

↓

TXTNormalizer

↓

TXTRawStorage

↓

ImportResultBuilder

↓

RibbonController
```

---

# Data Ownership

TXTFileReader

Owns

Raw File

HeaderParser

Owns

Header

Normalizer

Owns

Normalized Data

RawStorage

Owns

Imported Dataset

Engineering Engine

Receives

Read-only data

---

# Module Independence

Each module

May be tested independently.

Each module

May be replaced independently.

---

# Future Modules

MachineProfileLoader

CloudImporter

BinaryParser

CompressionParser

FatigueParser

ImpactParser

Reserved.

---

# Design Rules

✔ One responsibility per module

✔ No circular dependencies

✔ No worksheet manipulation

✔ No engineering calculations

✔ No report generation

✔ Independent unit testing possible

✔ Excel Ribbon communicates only with ImportController

---

End of Document
