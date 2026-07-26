# Parser Engine

Document ID : MTDMS-TXT-005

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

Core Engine

---

# Purpose

The Parser Engine is the central component of the TXT Import Engine.

Its responsibility is to transform decoded TXT content into a structured Engineering Dataset by recognizing sections, extracting fields, validating syntax, and coordinating specialized parsers.

The Parser Engine performs **no engineering calculations**.

---

# Role in MTDMS

```
TXT File

↓

Encoding Engine

↓

Version Detection

↓

Parser Engine

↓

Engineering Dataset Builder

↓

Calculation Engine
```

The Parser Engine is the only module responsible for interpreting the logical content of the TXT file.

---

# Design Philosophy

The parser shall be

• Modular

• Version independent

• Extensible

• Fault tolerant

• Read-only

Each logical section is parsed independently.

---

# Responsibilities

The Parser Engine shall

- Read decoded text
- Split the document into logical sections
- Detect section boundaries
- Route each section to the appropriate parser
- Collect parsed objects
- Build a normalized engineering model
- Report parsing errors
- Preserve original raw text references

---

# Parser Architecture

```
Decoded TXT

↓

Section Scanner

↓

Section Classifier

↓

Specialized Parsers

↓

Parsed Objects

↓

Engineering Dataset Builder
```

---

# Internal Components

## Section Scanner

Finds

Header

Machine

Sample

Material

Curve Data

Footer

without interpreting engineering values.

---

## Section Classifier

Assigns an internal type.

Example

```
HEADER

MACHINE

SAMPLE

LOADCELL

EXTENSOMETER

CURVE

FOOTER
```

---

## Parser Dispatcher

Routes each section

```
Machine Section

↓

Machine Parser


Sample Section

↓

Sample Parser


Curve Section

↓

Curve Parser
```

---

# Parser Interfaces

Each parser exposes

```
Initialize()

Parse()

Validate()

Build()

Dispose()
```

Every parser follows the same lifecycle.

---

# Supported Section Parsers

Header Parser

Machine Parser

Software Parser

Operator Parser

Customer Parser

Material Parser

Sample Parser

Test Parameter Parser

Load Cell Parser

Extensometer Parser

Channel Parser

Curve Parser

Footer Parser

Administrator configurable.

---

# Parsing Strategy

The parser operates in three stages.

Stage 1

Structure Recognition

↓

Stage 2

Field Extraction

↓

Stage 3

Normalization

No engineering calculations occur.

---

# Parsing Rules

The parser

shall ignore

Blank lines

Repeated spaces

Unknown comments

Optional fields

unless configured otherwise.

---

# Raw Data Preservation

Every parsed object stores

Original Line Number

Original Text

Section

Parser Version

This simplifies diagnostics.

---

# Memory Model

```
TXT Stream

↓

Read Buffer

↓

Section Buffer

↓

Parsed Object

↓

Release Buffer
```

Only required data remain in memory.

---

# VBA Classes

Recommended

```
clsParser

clsSection

clsHeader

clsMachine

clsSample

clsCurve

clsParserResult

clsParseError

clsDatasetBuilder
```

---

# Parser Result

Each parser returns

```
Success

Warnings

Errors

Parsed Object
```

The master parser decides whether import continues.

---

# Error Recovery

If one parser fails

↓

Record Error

↓

Continue if possible

↓

Build Partial Dataset

↓

Validation Engine decides final acceptance.

---

# Logging

The parser records

Parser Version

Execution Time

Detected Sections

Warnings

Errors

Line Numbers

SQLite Audit ID

---

# Thread Safety

Excel VBA is single-threaded.

The parser shall therefore execute sequentially.

Future .NET implementations may support parallel parsing.

---

# Engineering Independence

The Parser Engine

shall never calculate

Stress

Strain

Young's Modulus

Yield

Elongation

Spring Constant

Ring Stiffness

Only raw engineering information is extracted.

---

# SQLite Interaction

SQLite stores

Parser Version

Import Result

Warnings

Errors

Execution Time

Audit Information

The parsed engineering values are forwarded to the Engineering Dataset Builder.

---

# Error Handling

Unknown Section

↓

Ignore

Invalid Syntax

↓

Warning

Mandatory Section Missing

↓

Abort

Unexpected EOF

↓

Attempt Recovery

---

# Performance Targets

Section Scan

< 30 ms

Field Extraction

< 200 ms

Complete Parsing

< 1 s

Large File

Streaming

---

# Acceptance Criteria

✔ Modular parser

✔ Version independent

✔ Section routing

✔ Raw line preservation

✔ Fault tolerance

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No engineering calculations

✔ Complete traceability

---

# Related Documents

TXT-006_RecordReader

TXT-007_HeaderParser

TXT-008_TestInformationParser

TXT-013_DataSectionParser

TXT-016_EngineeringDatasetBuilder

---

End of Document
