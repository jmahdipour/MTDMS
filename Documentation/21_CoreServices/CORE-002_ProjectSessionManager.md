# Project Session Manager

Document ID

MTDMS-CORE-002

Version

1.0

Status

Core Service

Platform

Excel 2019 VBA

Application

MTDMS

---

# Purpose

Project Session Manager controls the complete life cycle of one test.

A Session begins when the operator selects a TXT file.

A Session ends when the report is archived.

Everything belongs to one Session.

---

# Session Life Cycle

Idle

↓

Open TXT

↓

Import

↓

Calculation

↓

Graph

↓

Report

↓

Archive

↓

Close Session

---

# Responsibilities

Open Session

Close Session

Keep Current Dataset

Keep User Settings

Track State

Undo

Redo

Temporary Objects

Log

---

# Session Object

clsSession

Contains

Dataset

Project Settings

Operator

Current Report

Current Graph

Current State

Execution Log

---

# States

Idle

Importing

Imported

Calculating

Calculated

Graph Ready

Report Ready

Archived

Closed

---

# State Transition

Idle

↓

Import

↓

Imported

↓

Calculation

↓

Calculated

↓

Report

↓

Archive

↓

Closed

---

# Session Rule

Only one Active Session exists.

Second Session cannot start until the first is closed.

---

# Session Components

Session

│

├── Dataset

├── Settings

├── Results

├── Graph

├── Report

├── Audit

└── Temporary Memory

---

# Temporary Objects

Temporary arrays

Regression buffers

Graph markers

Undo buffers

are destroyed when the session closes.

---

# Autosave

Optional

Administrator configurable.

Example

Every

5 minutes

---

# Recovery

If Excel crashes

↓

Last autosaved session

↓

Recover

---

# Session ID

Every Session has a unique ID.

Example

20260726-000154

---

# Logging

Every action is stored.

Import

Calculate

Graph

Report

Export

Archive

---

# Audit

Timestamp

Operator

Action

Result

Duration

---

# Acceptance

✔ One Session

✔ Full Traceability

✔ Crash Recovery Ready

✔ ISO 17025 Compatible

✔ Independent from Excel Worksheets

---

End Of Document
