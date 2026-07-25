# Engineering Graph Audit & Traceability Engine

Document ID : MTDMS-GE-020

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Chart Technology

Microsoft Excel Chart Objects

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

The Engineering Graph Audit & Traceability Engine records every significant action performed on engineering graphs to ensure complete traceability in accordance with ISO/IEC 17025.

The engine documents graphical interactions without altering engineering calculations or the original imported data.

---

# Objectives

The Graph Audit Engine shall

• Record graph operations

• Record operator actions

• Preserve traceability

• Support laboratory audits

• Maintain engineering integrity

---

# Engineering Philosophy

TXT File

↓

Engineering Dataset

↓

Graph

↓

Operator Action

↓

Audit Record

Every graphical action shall be traceable.

No engineering value shall be changed silently.

---

# Audited Operations

Graph Created

Graph Refreshed

Graph Printed

Graph Exported

Zoom

Pan

Marker Added

Marker Moved

Marker Deleted

Annotation Added

Yield Approved

Fracture Approved

Template Changed

Overlay Created

Workspace Changed

Administrator configurable.

---

# Audit Information

Each audit record stores

Unique Audit ID

Date

Time

Operator

Computer

Project

Report Number

Graph Type

Action

Object

Previous Value

New Value

Approval Status

---

# Read-Only Audit

Audit records are immutable.

They may be viewed

searched

filtered

exported

but never edited.

---

# Traceability Chain

TXT File

↓

Engineering Dataset

↓

Engineering Calculation

↓

Graph

↓

Operator Review

↓

Report

↓

Audit Record

Every stage is linked through unique identifiers.

---

# Search

The engine shall support searching by

Report Number

Operator

Date

Machine

Material

Customer

Graph Type

Audit Action

---

# Export

Audit records may be exported as

Excel

CSV

PDF

Administrator configurable.

---

# Retention

Audit retention period

is configurable.

Default

Never Automatically Deleted

---

# Engineering Independence

The Graph Audit Engine

shall never modify

TXT

Engineering Dataset

Engineering Results

Validation Results

Graph Objects

It records actions only.

---

# SQLite Interaction

SQLite stores

Complete Audit History

Operator Information

Action History

Timestamp

Configuration Version

This is the permanent audit repository.

---

# Error Handling

Audit Database Unavailable

↓

Warning

Continue Graph Operation

Audit Write Failure

↓

Retry

Operator Unknown

↓

Reject Login

---

# Performance Targets

Audit Record Creation

< 10 ms

Audit Search

< 200 ms

Audit Export

< 1 s

---

# Acceptance Criteria

✔ Complete graph audit trail

✔ Immutable records

✔ Search supported

✔ Export supported

✔ SQLite compatible

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Full traceability from TXT file to final graph

---

# End of Graph & Visualization Engine Chapter
