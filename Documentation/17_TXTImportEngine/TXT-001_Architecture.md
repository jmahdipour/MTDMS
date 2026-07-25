# TXT Import Engine Architecture

Document ID : MTDMS-TXT-001

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

The TXT Import Engine is the entry point of the entire MTDMS architecture.

Its responsibility is to import, validate, interpret, and convert the raw TXT file exported by the testing machine into a standardized engineering dataset that can be used by every subsequent subsystem.

The engine performs **no engineering calculations**.

---

# Scope

The engine is responsible for

• Reading TXT files

• Validating file integrity

• Detecting file format and version

• Parsing engineering information

• Building the internal engineering dataset

• Passing the dataset to the Calculation Engine

The engine never computes mechanical properties.

---

# Architectural Position

```
TXT File

↓

TXT Import Engine

↓

Engineering Dataset

↓

Calculation Engine

↓

Graph Engine

↓

Report Engine

↓

Archive
```

Every engineering module receives data only from the Engineering Dataset.

---

# Main Responsibilities

The TXT Import Engine consists of the following logical modules

• File Manager

• Encoding Detector

• Version Detector

• Header Parser

• Machine Parser

• Sample Parser

• Test Parser

• Load Cell Parser

• Extensometer Parser

• Curve Data Parser

• Dataset Builder

• Validation Engine

• Import Audit

Each module has a single responsibility.

---

# Input

Accepted source

TXT file exported directly from the testing machine software.

Supported extensions

```
*.txt
```

Future support

CSV

XML

JSON

Binary Export

Administrator configurable.

---

# Output

The engine produces one object only

Engineering Dataset

No calculations

No graphs

No reports

No database writes (except optional audit).

---

# Internal Architecture

```
TXT File

↓

File Reader

↓

Tokenizer

↓

Section Detector

↓

Section Parsers

↓

Dataset Builder

↓

Validation

↓

Engineering Dataset
```

---

# Layered Design

Layer 1

Physical File Access

------------------------

Layer 2

Encoding Detection

------------------------

Layer 3

TXT Parsing

------------------------

Layer 4

Engineering Dataset Construction

------------------------

Layer 5

Validation

------------------------

Layer 6

Output Interface

---

# VBA Modules

Recommended

```
modTXTImport

modTXTReader

modTXTParser

modTXTValidation

modDatasetBuilder

modTXTUtility

clsEngineeringDataset

clsImportSession

clsCurvePoint

clsSample

clsMachine

clsTestInformation
```

Each module shall have one responsibility.

---

# Engineering Dataset

The dataset contains

Machine Information

Operator

Sample

Material

Test Parameters

Curve Data

Load Cell

Extensometer

Units

Metadata

No calculated values.

---

# Dataset Lifetime

```
Import

↓

Dataset

↓

Calculation Engine

↓

Disposed
```

The dataset exists only while required.

---

# Memory Model

TXT File

↓

Read Once

↓

Parse Once

↓

Dataset

↓

Reuse

The TXT file shall never be parsed twice during the same session unless explicitly requested.

---

# Error Isolation

Each parser shall fail independently.

Example

Header OK

↓

Machine OK

↓

Sample Failed

↓

Continue

↓

Report Error

---

# Dependency Rules

TXT Import Engine

depends on

File System

SQLite (optional)

Excel Workbook

It does NOT depend on

Calculation Engine

Graph Engine

Report Engine

This prevents circular dependencies.

---

# SQLite Interaction

Optional

Import History

File Name

Import Date

Operator

Machine

Status

Audit

Engineering data are not stored during import unless configured.

---

# Configuration

Administrator configurable

Supported Encodings

Default Folder

Import Options

Validation Level

Audit Logging

Auto Backup

---

# Engineering Independence

The TXT Import Engine

shall never calculate

Yield Strength

Young's Modulus

Stress

Strain

Elongation

Any mechanical property

Its responsibility ends after building a validated engineering dataset.

---

# Error Handling

File Missing

↓

Abort

Encoding Unknown

↓

Try Next Encoding

Unsupported Version

↓

Reject

Corrupted File

↓

Abort

Partial File

↓

Warning

---

# Performance Targets

Open File

< 20 ms

Parse Header

< 50 ms

Build Dataset

< 300 ms

Large File Import

< 2 s

---

# Acceptance Criteria

✔ TXT file successfully imported

✔ Dataset created

✔ No engineering calculations performed

✔ Modular architecture

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Supports future machine formats

✔ Complete traceability to original TXT file

---

# Related Documents

TXT-002_FileStructure

TXT-003_VersionDetection

TXT-004_FileEncoding

TXT-005_ParserEngine

TXT-016_EngineeringDatasetBuilder

---

End of Document
