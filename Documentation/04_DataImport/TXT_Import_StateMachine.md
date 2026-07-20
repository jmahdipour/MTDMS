# TXT Import State Machine

Document ID : MTDMS-IMP-042

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Module

Import Engine

---

# Purpose

This document defines the complete state machine controlling the TXT Import process.

The Import Engine shall always be in one and only one state.

State transitions guarantee deterministic behaviour and prevent partially imported projects.

---

# Design Philosophy

Idle

↓

Import

↓

Validation

↓

Storage

↓

Engineering

↓

Ready

or

↓

Error

---

# State Diagram

```
IDLE

↓

FILE_SELECTED

↓

READING_FILE

↓

PARSING

↓

HEADER_VALIDATION

↓

COLUMN_VALIDATION

↓

UNIT_CONVERSION

↓

MATERIAL_LOOKUP

↓

STANDARD_LOOKUP

↓

SPECIMEN_RECOGNITION

↓

DATABASE_SYNCHRONIZATION

↓

RAWDATA_STORAGE

↓

ENGINEERING_INITIALIZATION

↓

GRAPH_INITIALIZATION

↓

READY
```

Failure at any state

↓

ERROR

↓

ROLLBACK

↓

IDLE

---

# State List

## IDLE

System waiting for user.

Ribbon

Import Button

Enabled

All other import actions

Disabled.

---

## FILE_SELECTED

TXT selected.

Checks

Extension

Existence

Read Permission

---

## READING_FILE

Read TXT

↓

Memory Buffer

Progress Bar

Visible

Cancel Button

Enabled

---

## PARSING

Parser separates

Header

Columns

Data

Comments

Metadata

---

## HEADER_VALIDATION

Verify

Required Headers

Machine

Material

Standard

Area

Gauge Length

---

## COLUMN_VALIDATION

Verify

Force

Stroke

Time

Required

Optional columns

Recognized

Unknown columns

Logged

Ignored

---

## UNIT_CONVERSION

Convert

Force

Length

Stress

Temperature

Speed

Time

Internal Units

Only

---

## MATERIAL_LOOKUP

Search

SQLite

Material Library

Found

↓

Continue

Not Found

↓

Operator Selection

---

## STANDARD_LOOKUP

Search

SQLite

Standard Library

Found

↓

Continue

Not Found

↓

Operator Selection

---

## SPECIMEN_RECOGNITION

Determine

Round

Flat

Pipe

Ring

Spring

Compression

Calculate Area

Validate Dimensions

---

## DATABASE_SYNCHRONIZATION

Create Transaction

Verify Project

Verify Session

Verify Duplicate

Create Import Session

---

## RAWDATA_STORAGE

Insert

tblRawData

Progress

Displayed

Commit

Deferred

---

## ENGINEERING_INITIALIZATION

Generate

Engineering Data

Stress

Strain

True Stress

True Strain

Elastic Region

Yield

---

## GRAPH_INITIALIZATION

Prepare

Engineering Dataset

Markers

Elastic Line

Yield Marker

Fracture Marker

---

## READY

Import Complete.

Ribbon

Engineering Commands

Enabled

Reports

Enabled

Graphs

Enabled

---

# ERROR

Entered whenever

Critical Error

Occurs.

---

# ERROR Behaviour

Display

Message

↓

Rollback

↓

Release Memory

↓

Return to

IDLE

---

# State Transitions

| Current | Next |
|-----------|------|
| IDLE | FILE_SELECTED |
| FILE_SELECTED | READING_FILE |
| READING_FILE | PARSING |
| PARSING | HEADER_VALIDATION |
| HEADER_VALIDATION | COLUMN_VALIDATION |
| COLUMN_VALIDATION | UNIT_CONVERSION |
| UNIT_CONVERSION | MATERIAL_LOOKUP |
| MATERIAL_LOOKUP | STANDARD_LOOKUP |
| STANDARD_LOOKUP | SPECIMEN_RECOGNITION |
| SPECIMEN_RECOGNITION | DATABASE_SYNCHRONIZATION |
| DATABASE_SYNCHRONIZATION | RAWDATA_STORAGE |
| RAWDATA_STORAGE | ENGINEERING_INITIALIZATION |
| ENGINEERING_INITIALIZATION | GRAPH_INITIALIZATION |
| GRAPH_INITIALIZATION | READY |

---

# Illegal Transitions

READY

↓

PARSING

Not Allowed

GRAPH_INITIALIZATION

↓

HEADER_VALIDATION

Not Allowed

ENGINEERING_INITIALIZATION

↓

READING_FILE

Not Allowed

---

# Ribbon Behaviour

State

↓

Ribbon Controls

Automatically Updated

Example

IDLE

↓

Import Enabled

Engineering Disabled

READY

↓

All Analysis Commands Enabled

---

# SQLite Logging

Every state change stored

State

Timestamp

Operator

Project

Session

Status

Duration

---

# Timeout

If state exceeds

Configured Timeout

↓

Import Aborted

↓

Rollback

↓

Error Logged

---

# Recovery

After ERROR

↓

System returns

IDLE

No partial project remains.

---

# Future States

LIVE_IMPORT

ETHERNET_IMPORT

REMOTE_DATABASE

CLOUD_SYNC

Reserved

---

# Acceptance Criteria

✔ Deterministic workflow

✔ Single active state

✔ Automatic rollback

✔ Ribbon synchronized with state

✔ SQLite logging

✔ Excel 2019 compatible

✔ ISO 17025 traceable

---

End of Document
