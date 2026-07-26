# Record Reader Engine

Document ID : MTDMS-TXT-006

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

The Record Reader Engine is responsible for reading the decoded TXT file sequentially and converting the physical text stream into logical records that can be processed by the Parser Engine.

It provides controlled access to every line while preserving the original file order.

The Record Reader performs **no engineering interpretation** and **no engineering calculations**.

---

# Position in Architecture

```
TXT File

↓

Encoding Engine

↓

Record Reader

↓

Parser Engine

↓

Engineering Dataset
```

The Record Reader is the first component that works with decoded text.

---

# Responsibilities

The Record Reader shall

• Read text sequentially

• Preserve line order

• Preserve original line numbers

• Normalize line endings

• Provide buffering

• Support look-ahead

• Support rollback

• Detect end-of-file

---

# Design Philosophy

The Record Reader is intentionally simple.

It knows

how to read.

It does NOT know

what the data mean.

Meaning belongs to the Parser Engine.

---

# Reader Workflow

```
Open File

↓

Read Line

↓

Normalize

↓

Assign Line Number

↓

Buffer

↓

Return Record
```

---

# Record Definition

Each physical line becomes one logical record.

Every record contains

Record ID

Line Number

Original Text

Normalized Text

Length

End Of File Flag

Parser State

---

# Record Object

Recommended VBA Class

```
clsTXTRecord
```

Properties

```
LineNumber

OriginalText

NormalizedText

Length

EOF

SectionID
```

Methods

```
Reset()

Clone()

Clear()
```

---

# Reader Interface

Recommended methods

```
Open()

Close()

ReadNext()

Peek()

Rollback()

EOF()

CurrentRecord()

Reset()
```

---

# Sequential Reading

Default mode

```
Line 1

↓

Line 2

↓

Line 3

↓

...
```

No random access is required.

---

# Look-Ahead Buffer

The parser occasionally needs to inspect the next record.

Example

```
Current

↓

Peek

↓

Decision
```

The reader therefore supports

```
Peek(1)

Peek(2)

Peek(n)
```

without advancing the file pointer.

---

# Rollback

Certain parsers may need to return one or more records.

Example

```
Read

↓

Unexpected Section

↓

Rollback

↓

Different Parser
```

Rollback shall be supported.

---

# Line Ending Normalization

Supported

CR

LF

CRLF

All records are normalized internally.

---

# Empty Lines

Supported

Empty records are preserved.

Parser decides whether they are ignored.

---

# Maximum Record Length

Recommended

32767 characters

Longer records generate warnings.

---

# Buffer Strategy

Recommended

```
Previous Record

Current Record

Next Record

Peek Buffer
```

This minimizes memory consumption.

---

# Memory Model

```
TXT Stream

↓

Reader Buffer

↓

Parser

↓

Release Buffer
```

Large files remain efficient.

---

# Error Detection

The reader detects

Unexpected EOF

Unreadable Line

Corrupted Characters

Buffer Overflow

Invalid Line Ending

---

# SQLite Logging

SQLite records

Import Start

Import End

Read Time

Number of Records

Warnings

Errors

Audit ID

---

# Performance Targets

Open File

< 20 ms

Read Record

< 1 ms

Peek

Immediate

Rollback

Immediate

---

# Engineering Independence

The Record Reader

shall never

interpret

calculate

modify

engineering values.

It reads records only.

---

# Error Handling

File Not Open

↓

Abort

Unexpected EOF

↓

Notify Parser

Invalid Record

↓

Warning

Buffer Failure

↓

Abort

---

# Acceptance Criteria

✔ Sequential reading

✔ Look-ahead supported

✔ Rollback supported

✔ Line numbers preserved

✔ Buffering

✔ SQLite compatible

✔ Excel 2019 compatible

✔ No engineering calculations

✔ Complete traceability to original TXT file

---

# Related Documents

TXT-005_ParserEngine

TXT-007_HeaderParser

TXT-013_DataSectionParser

TXT-016_EngineeringDatasetBuilder

---

End of Document
