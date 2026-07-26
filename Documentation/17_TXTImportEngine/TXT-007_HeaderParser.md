# Header Parser

Document ID : MTDMS-TXT-007

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

The Header Parser extracts all metadata located at the beginning of the TXT file before engineering data are encountered.

The Header Parser identifies the export environment, software information, machine identity, and file characteristics required for the remainder of the import process.

The Header Parser performs **no engineering calculations**.

---

# Position in Architecture

```
TXT File

↓

Record Reader

↓

Header Parser

↓

Parser Dispatcher

↓

Engineering Dataset
```

The Header Parser is executed immediately after Version Detection.

---

# Responsibilities

The Header Parser shall

• Read the beginning of the TXT file

• Extract metadata

• Identify software information

• Identify machine information

• Detect export characteristics

• Preserve original records

• Report missing mandatory information

---

# Parsing Scope

Typical information contained in the header

Software Name

Software Version

Machine Name

Machine Model

Export Date

Export Time

Language

Operator

Separator

Units

Encoding (optional)

Laboratory

Project (optional)

Administrator configurable.

---

# Parsing Workflow

```
Header Records

↓

Recognize Field

↓

Normalize Value

↓

Validate

↓

Store

↓

Continue
```

---

# Example Logical Header

```
Software

↓

TRAPEZIUM X


Version

↓

2.45


Machine

↓

AG-25TB


Date

↓

2026-07-13


Operator

↓

Laboratory01
```

The physical TXT layout may differ.

---

# Supported Metadata

## Software Information

Software Name

Software Version

Build

Export Revision

---

## Machine Information

Machine Model

Machine Serial Number

Capacity

Frame

Controller

PLC (optional)

---

## Export Information

Export Date

Export Time

Export Language

Export Computer

---

## Laboratory Information

Laboratory Name

Department

Operator

Supervisor

Optional.

---

# Header Object

Recommended VBA Class

```
clsHeaderInformation
```

Properties

```
SoftwareName

SoftwareVersion

MachineModel

MachineSerial

ExportDate

ExportTime

Language

Operator

Project

Comments
```

---

# Missing Fields

Mandatory

Software Name

Machine Name

Export Date

Optional

Operator

Project

Comments

Unknown optional fields are ignored.

---

# Validation

The Header Parser validates

Software Name Exists

Machine Exists

Date Format Valid

Version Format Valid

Header Complete

No engineering values are validated here.

---

# Normalization

Examples

```
TRAPEZIUM X

↓

Trapezium X
```

```
2026/07/13

↓

2026-07-13
```

Only formatting changes.

Original values remain stored.

---

# Duplicate Fields

If duplicate header fields exist

↓

Last Valid Value

↓

Warning Logged

Administrator configurable.

---

# Unknown Fields

Unknown header entries are stored inside

AdditionalMetadata

for future compatibility.

---

# SQLite Interaction

Optional metadata stored

Software

Version

Machine

Import Date

Import Time

Operator

Audit ID

---

# Error Handling

Software Missing

↓

Abort

Machine Missing

↓

Abort

Invalid Date

↓

Warning

Unknown Header Field

↓

Ignore

---

# Engineering Independence

The Header Parser

shall never calculate

Stress

Strain

Yield

Young's Modulus

Any engineering value.

Its responsibility ends after metadata extraction.

---

# Performance Targets

Header Parsing

< 20 ms

Metadata Validation

< 10 ms

SQLite Logging

< 10 ms

---

# Acceptance Criteria

✔ Metadata extracted

✔ Mandatory fields validated

✔ Unknown fields preserved

✔ Header normalization

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No engineering calculations

✔ Complete traceability

---

# Related Documents

TXT-005_ParserEngine

TXT-006_RecordReader

TXT-008_TestInformationParser

TXT-016_EngineeringDatasetBuilder

---

End of Document
