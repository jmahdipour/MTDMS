# SQLite Database Architecture

Document ID

MTDMS-DB-001

Version

1.0

Status

Core Architecture

Platform

SQLite

Application

MTDMS

Language

VBA

---

# Purpose

SQLite is used only for

Persistent Data

It is NOT used as Calculation Database.

All engineering calculations remain inside RAM.

---

# Engineering Rule

TXT

↓

EngineeringDataset

↓

Calculation

↓

Graph

↓

Report

↓

SQLite Archive

SQLite never participates in calculations.

---

# Database Layers

Database

│

├── Master Tables

├── Material Tables

├── Test Tables

├── Result Tables

├── Audit Tables

├── Configuration Tables

└── Archive Tables

---

# Master Tables

Laboratory

Operators

Machines

Standards

Customers

Projects

---

# Material Tables

Materials

Material Groups

Mechanical Properties

Chemical Composition

Young Modulus Library

Yield Library

Density

Administrator configurable

---

# Test Tables

Test Header

Test Parameters

Specimen Information

Machine Information

Extensometer Information

Environmental Information

---

# Result Tables

Maximum Force

Maximum Stress

Yield

Young Modulus

Elongation

Reduction of Area

Energy

Ring Stiffness

Spring Constant

Only Final Results

No Curve

---

# Curve Storage

Engineering curves

are NOT stored

inside SQLite

Default

Reason

Large Files

High Speed

Curves exported separately

CSV

Binary

Future

---

# Audit Tables

Every action

Import

Calculation

Graph

Correction

Report

Export

Archive

User

Date

Time

---

# Configuration Tables

Application Settings

Calculation Settings

Report Settings

Graph Settings

Material Settings

Archive Settings

---

# Archive Tables

Report History

Revision

Approval

Digital Signature

Backup Information

---

# Relationships

Project

↓

Many Tests

↓

Many Results

↓

One Report

---

# Primary Keys

INTEGER AUTOINCREMENT

Every table

---

# Foreign Keys

Always Enabled

No orphan records

---

# Transactions

Every Import

↓

BEGIN

↓

Insert

↓

Insert

↓

Insert

↓

COMMIT

Failure

↓

ROLLBACK

---

# Performance

Indexes

TestID

ProjectID

MaterialID

OperatorID

Date

---

# Backup

SQLite

↓

Automatic Backup

↓

Daily

↓

Administrator configurable

---

# Security

Read

Write

Administrator

Operator

Viewer

Future

---

# Acceptance

✔ Lightweight

✔ Fast

✔ RAM Calculation

✔ ISO 17025 Ready

✔ Audit Ready

✔ Future Expandable

---

End Of Document
