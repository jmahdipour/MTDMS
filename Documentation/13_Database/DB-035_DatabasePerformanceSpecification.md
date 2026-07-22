# Database Performance Specification

Document ID : MTDMS-DB-035

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Database

SQLite

Application

MTDMS

Status

Production

---

# Purpose

This document defines the expected performance requirements of the MTDMS SQLite database when operating inside Microsoft Excel 2019.

The objective is to guarantee acceptable response times while maintaining engineering traceability.

Performance optimization shall never affect engineering calculations.

---

# Objectives

The database shall

• Open quickly

• Search efficiently

• Generate reports rapidly

• Scale to large historical datasets

• Maintain engineering integrity

---

# Design Philosophy

TXT File

↓

Import

↓

Engineering Calculation

↓

SQLite Storage

↓

Search / Report

Performance optimization affects only database access.

Engineering calculations remain unchanged.

---

# Expected Database Size

Small Laboratory

Up to

10,000

reports

----------------------------

Medium Laboratory

Up to

100,000

reports

----------------------------

Large Laboratory

Up to

1,000,000

reports

---

# Expected Storage

SQLite Database

Typically

100 MB

↓

2 GB

depending on history.

Raw TXT files

remain outside

the database.

---

# Startup Performance

Open Database

Target

< 1 second

Load Configuration

Target

< 200 ms

Load Material Library

Target

< 300 ms

Load Application Settings

Target

< 100 ms

---

# Import Performance

Register TXT

< 100 ms

Checksum

Depends on TXT size

Engineering Calculation

Depends on test size

Database Save

< 100 ms

---

# Search Performance

Customer Search

< 100 ms

Certificate Search

< 100 ms

Report Search

< 100 ms

Archive Search

< 200 ms

Material Search

< 100 ms

Machine Search

< 100 ms

---

# Report Performance

Open Report

< 500 ms

Generate Report

< 2 seconds

Generate PDF

Depends on report complexity

---

# Database Operations

Insert

< 20 ms

Update

< 20 ms

Delete

< 20 ms

Read

< 5 ms

Single Record

---

# Index Performance

Primary Key

Indexed

Foreign Keys

Indexed

Search Fields

Indexed

Composite Fields

Indexed

---

# Engineering Independence

Performance optimization

shall never

modify

Imported TXT

Engineering Results

Validation Results

Graph Data

Reports

---

# Memory Usage

Typical

< 300 MB

Excel

+

SQLite

+

Application

---

# Recommended Maintenance

Weekly

Integrity Check

Monthly

Analyze

Monthly

Vacuum

Backup

Daily

---

# Scalability

The system shall continue operating correctly

after

1,000,000

engineering reports.

---

# Performance Monitoring

Monitor

Database Size

Database Growth

Query Time

Report Time

Backup Time

Integrity Check Duration

---

# Error Handling

Database Slow

↓

Analyze

Database Fragmented

↓

Vacuum

Missing Index

↓

Rebuild

Corruption

↓

Restore Backup

---

# Acceptance Criteria

✔ Startup within specification

✔ Search within specification

✔ Report generation within specification

✔ SQLite scalable

✔ Excel 2019 compatible

✔ Engineering calculations unaffected

✔ ISO/IEC 17025 compliant

✔ Long-term historical support

---

End of Document
