# File Parser

Document ID : MTDMS-DAT-003

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Data Management

Status

Production

---

# Purpose

The File Parser converts the exported machine file into the internal MTDMS engineering data model.

The parser is responsible only for interpreting the exported file.

It does not communicate with the testing machine.

It does not perform engineering calculations.

---

# Responsibilities

Read File

↓

Recognize Format

↓

Read Header

↓

Read Engineering Data

↓

Convert Units

↓

Create Internal Data Structure

↓

Pass Data to Engineering Engine

---

# Supported Input Formats

TXT

CSV

DAT

Future

XML

JSON

Administrator configurable.

---

# Parser Architecture

```
Input File

↓

Format Detector

↓

Header Parser

↓

Metadata Parser

↓

Data Parser

↓

Internal Object Model

↓

Engineering Engine
```

---

# File Sections

Typical file consists of

Header

↓

Machine Information

↓

Specimen Information

↓

Engineering Parameters

↓

Measurement Data

↓

End Of File

---

# Header Parser

Reads

Software Version

Machine Name

Export Date

Operator

Material

Specimen ID

Dimensions

Gauge Length

Area

Units

---

# Metadata Parser

Reads

Certificate Number

Project

Customer

Standard

Material Grade

Specimen Shape

Operator

Optional Fields

---

# Measurement Parser

Supported channels

Time

Force

Displacement

Extension

Engineering Strain

Engineering Stress

True Strain

True Stress

Temperature

Auxiliary Channels

Unknown channels are ignored but logged.

---

# Internal Data Model

Each imported test creates

```
TestObject

 ├── Header

 ├── Metadata

 ├── Channels

 ├── Raw Data

 ├── Status

 └── Validation
```

---

# Data Types

Integer

Double

Date

Time

Boolean

String

---

# Missing Values

Missing numeric values

↓

NULL

Missing text

↓

Empty String

Parser never invents values.

---

# Delimiter Detection

Supported

Comma

Semicolon

Tab

Space

Automatic detection available.

---

# Decimal Separator

Supported

.

,

Automatically converted to internal format.

---

# Character Encoding

Supported

UTF-8

ANSI

Unicode

Auto Detect

Preferred

UTF-8

---

# Unit Conversion

Parser converts only

display units

to the internal unit system.

Internal engineering units

remain consistent throughout the software.

---

# Unsupported Fields

Unknown header fields

↓

Stored in

Additional Metadata

No information is discarded.

---

# Parser Validation

Verify

Header Exists

Columns Match

Required Channels Present

Data Count

Units

---

# Parser Output

Output contains

Metadata

Raw Measurements

Channel Definitions

Import Status

Validation Status

No calculations.

---

# SQLite Database

Tables

```
tblRawFile

tblRawChannel

tblRawMeasurement

tblParsedMetadata
```

---

# Performance

Target

100,000 measurement rows

↓

< 2 seconds

Memory optimized.

---

# Error Handling

Unknown Format

↓

Reject

Unexpected Column Count

↓

Reject

Corrupted Header

↓

Reject

Invalid Numeric Data

↓

Reject

Unsupported Encoding

↓

Retry UTF-8

---

# Future Enhancements

Plugin Parser

Custom Parser API

Automatic Format Recognition

Batch Parsing

Reserved

---

# Acceptance Criteria

✔ Reads exported files only

✔ No machine communication

✔ No engineering calculations

✔ Supports multiple formats

✔ UTF-8 compatible

✔ SQLite compatible

✔ Excel 2019 compatible

✔ ISO/IEC 17025 compliant

---

End of Document
