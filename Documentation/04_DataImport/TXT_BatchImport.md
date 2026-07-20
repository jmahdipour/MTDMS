# TXT Batch Import Specification

Document ID : MTDMS-IMP-045

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

Reserved for Future Version

---

# Purpose

This document defines the future Batch Import architecture.

Version 1.0 of MTDMS supports

One Project

↓

One TXT File

Future versions will allow importing multiple TXT files in a single operation.

---

# Design Goals

Reduce operator workload.

Support production laboratories.

Automatically create projects.

Automatically assign sessions.

Maintain complete ISO 17025 traceability.

---

# Current Version

```
Supported

Single TXT Import
```

```
Not Supported

Multiple TXT Import
```

Ribbon

Batch Import button

Hidden

---

# Future Workflow

Folder

↓

Scan TXT Files

↓

Recognize Machine

↓

Recognize Material

↓

Recognize Standard

↓

Validate

↓

SQLite

↓

Engineering

↓

Reports

---

# Batch Wizard

Future Ribbon

```
Batch Import
```

Steps

Select Folder

↓

Find TXT Files

↓

Display List

↓

Validate

↓

Import

↓

Summary

---

# Folder Scan

Supported Extensions

```
*.txt
```

Recursive Scan

Optional

---

# Import Queue

Each discovered TXT becomes one queue item.

Queue Item

Contains

Filename

Machine

Material

Standard

Project

Status

Checksum

---

# Queue States

Waiting

Reading

Validated

Importing

Completed

Skipped

Failed

Cancelled

---

# Batch Validation

Before importing

All files checked for

Duplicate

Readable

Correct Header

Known Machine

Known Standard

Known Material

---

# Duplicate Handling

Duplicate

↓

Skipped

↓

Logged

↓

Continue Next File

---

# Error Isolation

Failure of one TXT

↓

Does NOT stop

Entire Batch

Each file executes in its own SQLite transaction.

---

# Project Creation

Future Options

One File

↓

One Project

or

Multiple Files

↓

Single Project

↓

Multiple Sessions

Administrator selectable.

---

# Progress

Ribbon Progress

Example

```
23 / 145

Imported

15%

Current

Specimen_023.txt
```

---

# Parallel Processing

Not supported

Excel VBA

Single Thread

Future

External Engine

Reserved

---

# Batch Report

Generated automatically

Includes

Imported Files

Skipped Files

Failed Files

Warnings

Errors

Import Duration

---

# Batch Log

SQLite

```
tblBatchImport
```

Fields

BatchID

Start Time

End Time

Operator

Folder

Imported

Skipped

Failed

Duration

---

# Recovery

Interrupted Batch

↓

Resume

Reserved

---

# Performance Target

100 TXT Files

↓

Automatic Import

↓

Less than 5 Minutes

Recommended Hardware

SSD

8 GB RAM

---

# Ribbon Behaviour

Current Version

Hidden

Future Version

Visible

Only when Batch Module installed.

---

# Future Features

Automatic Folder Watch

Scheduled Import

PLC Triggered Import

Network Folder Import

Cloud Import

Reserved

---

# Acceptance Criteria

✔ Reserved for future implementation

✔ Compatible with existing SQLite structure

✔ Independent transactions

✔ Duplicate detection

✔ ISO 17025 traceability

✔ Excel 2019 architecture preserved

---

End of Document
