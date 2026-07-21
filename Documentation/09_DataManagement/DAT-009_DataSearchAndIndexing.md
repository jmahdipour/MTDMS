# Data Search and Indexing

Document ID : MTDMS-DAT-009

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

The Data Search and Indexing module provides fast retrieval of engineering data, reports and archived information stored within MTDMS.

The module searches only locally stored data.

It has no communication with testing machines.

---

# Objectives

The Search Engine shall

• Locate engineering records

• Locate imported files

• Locate reports

• Locate archived records

• Support fast filtering

• Support multi-condition search

• Preserve database performance

---

# Search Sources

SQLite Database

Archived Database

Report Index

Material Library

Equipment Library

Certificate Database

---

# Search Workflow

```
User Query

↓

Query Parser

↓

Index Lookup

↓

Database Filter

↓

Result Ranking

↓

Display Results
```

---

# Search Fields

Certificate Number

Sample ID

Material

Material Grade

Customer

Operator

Test Type

Machine

Standard

Heat Number

Batch Number

Date

Revision

Status

Archive ID

Original File Name

---

# Advanced Filters

Date Range

Material Family

Standard

Customer

PASS

FAIL

Revision

Operator

Machine

Equipment

Approval Status

Archive Status

---

# Wildcard Search

Supported

*

?

Partial Text

Case Insensitive

Administrator configurable.

---

# Full Text Search

Supported

Remarks

Comments

Operator Notes

Customer Notes

Material Description

---

# Search Result

Each result displays

Certificate Number

Sample ID

Material

Test Type

Date

Revision

Status

Operator

Archive Status

---

# Sorting

Sort by

Date

Certificate Number

Material

Customer

Operator

Status

Revision

---

# Indexing

Indexes maintained for

Certificate Number

Sample ID

Material

Date

Customer

Machine

Archive ID

---

# Automatic Index Update

Occurs after

Import

Archive

Revision

Deletion (Logical)

Database Maintenance

---

# Performance Targets

10,000 Records

< 1 Second

100,000 Records

< 3 Seconds

1,000,000 Records

< 10 Seconds

Target values only.

---

# Saved Searches

Users may save

Frequently Used Filters

Administrator configurable.

---

# Recent Searches

Recent search history

Stored locally

Maximum Entries

50

Administrator configurable.

---

# SQLite Database

Tables

```
tblSearchHistory

tblSearchProfile

tblIndexStatistics
```

---

# Audit Trail

Record

Search User

Timestamp

Search Criteria

Returned Records

Computer Name

Search Duration

---

# Permissions

Administrator

Full Search

Reviewer

Full Search

Operator

Engineering Records Only

Guest

Restricted

---

# Error Handling

Invalid Query

↓

Warning

Database Offline

↓

Abort

No Results

↓

Empty Result Set

Corrupted Index

↓

Rebuild Index

---

# Future Enhancements

AI Semantic Search

OCR Search

Image Search

Cloud Search

Natural Language Search

Reserved

---

# Acceptance Criteria

✔ Multi-field search

✔ Indexed search

✔ Archive search

✔ SQLite compatible

✔ Excel 2019 compatible

✔ High-performance retrieval

✔ ISO/IEC 17025 compliant

✔ Complete audit trail

---

End of Document
