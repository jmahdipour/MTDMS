# TXT Raw Data Table Specification

Document ID : MTDMS-IMP-028

Version : 0.1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

---

# Purpose

This document defines the database structure of the Raw Data table.

The Raw Data table stores every imported measurement exactly as received from the TXT parser after unit normalization.

Raw data shall never be modified by the Engineering Engine.

---

# Table Name

```
tblRawData
```

---

# Primary Key

```
RawDataID
```

Type

INTEGER

Primary Key

Auto Increment

---

# Foreign Keys

```
ProjectID

SessionID

SpecimenID
```

---

# Table Structure

| Field | Type | Description |
|---------|------|-------------|
| RawDataID | INTEGER | Primary Key |
| ProjectID | INTEGER | Project Reference |
| SessionID | INTEGER | Import Session |
| RowIndex | INTEGER | Original Sample Number |
| Time | REAL | Second |
| Force | REAL | Newton |
| Stroke | REAL | Millimeter |
| Extension | REAL | Millimeter |
| Temperature | REAL | Celsius |
| Speed | REAL | mm/min |
| LoadCellID | INTEGER | Active Load Cell |
| ExtensometerID | INTEGER | Active Extensometer |
| StatusFlag | INTEGER | Sample Status |
| Created | DATETIME | Timestamp |

---

# Internal Units

Time

Second

Force

Newton

Stroke

Millimeter

Extension

Millimeter

Temperature

°C

Speed

mm/min

---

# Row Order

Rows are stored exactly in acquisition order.

Sorting

```
ProjectID

↓

SessionID

↓

RowIndex
```

---

# Status Flag

0

Valid

1

Ignored

2

Duplicate

3

Invalid

4

Filtered

Future

5

Interpolated

---

# Data Integrity

Every record belongs to

One Project

One Import Session

One Specimen

---

# Read Only Policy

After insertion

Records become

Read Only

No UPDATE

No DELETE

Only INSERT

---

# Indexes

Primary

RawDataID

Secondary

ProjectID

SessionID

RowIndex

Performance Index

(ProjectID, SessionID)

---

# Record Count

Typical

500

↓

200000

Maximum Supported

500000

---

# Import Sequence

TXT

↓

Variant Array

↓

tblRawData

↓

Engineering Engine

---

# Data Validation

Before insertion

Numeric

Finite

Units Converted

Time Ordered

Mandatory Values Present

---

# Storage Rules

Every imported sample

↓

One Database Row

No aggregation

No averaging

No compression

---

# Example Record

```
RawDataID      15234

ProjectID      15

SessionID      2

RowIndex       1578

Time           78.550

Force          15423.44

Stroke         18.332

Extension      15.924

Temperature    23.6

Speed          10

StatusFlag     0
```

---

# Backup

Included in

SQLite Backup

Never exported back to TXT.

---

# Future Fields

Humidity

Hydraulic Pressure

Motor Torque

PLC State

Digital Inputs

Digital Outputs

Encoder Position

Reserved

---

# Acceptance Criteria

✔ Immutable after import

✔ Normalized engineering units

✔ Indexed for fast access

✔ Supports 500000 records

✔ SQLite compatible

✔ Engineering Engine reads only

---

End of Document
