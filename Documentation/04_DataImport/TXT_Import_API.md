# TXT Import Internal API Specification

Document ID : MTDMS-IMP-047

Version : 1.0

Platform

Microsoft Excel 2019

Language

VBA

Application

MTDMS

Architecture

Internal API

---

# Purpose

This document defines the internal interfaces between Import Engine and the remaining MTDMS modules.

This is NOT a Web API.

This is the internal VBA architecture that allows every module to communicate without direct dependency.

Every module shall communicate only through these interfaces.

---

# Architecture

Ribbon

↓

Import API

↓

Parser

↓

Validation

↓

SQLite

↓

Engineering

↓

Graphs

↓

Reports

---

# Design Goals

Loose Coupling

Maintainability

Module Independence

Future Expansion

Unit Testing

---

# Import API Modules

ImportController

↓

ParserService

↓

ValidationService

↓

SQLiteService

↓

EngineeringService

↓

GraphService

↓

ReportService

---

# ImportController

Responsibilities

Start Import

Cancel Import

Resume

State Management

Progress Reporting

Public Methods

```
StartImport()

CancelImport()

ResumeImport()

ResetImport()

GetImportState()
```

---

# ParserService

Responsibilities

TXT Reading

Header Parsing

Column Parsing

Metadata Extraction

Public Methods

```
ParseHeader()

ParseColumns()

ParseRawData()

ParseMetadata()
```

---

# ValidationService

Responsibilities

Header Validation

Dimension Validation

Unit Validation

Material Validation

Standard Validation

Public Methods

```
ValidateHeader()

ValidateColumns()

ValidateDimensions()

ValidateUnits()

ValidateMaterial()

ValidateStandard()
```

---

# SQLiteService

Responsibilities

Transactions

Insert

Update

Rollback

Audit

Public Methods

```
BeginTransaction()

Commit()

Rollback()

InsertRawData()

InsertAudit()

GetProject()

CreateProject()
```

---

# EngineeringService

Responsibilities

Engineering Stress

Engineering Strain

True Stress

True Strain

Yield

Young's Modulus

Public Methods

```
CalculateEngineering()

CalculateYield()

CalculateYoung()

CalculateTrueStress()

CalculateTrueStrain()
```

---

# GraphService

Responsibilities

Prepare Dataset

Correction Layer

Markers

Graph Cache

Public Methods

```
PrepareGraph()

CorrectGraph()

ResetGraph()

CreateMarkers()
```

---

# ReportService

Responsibilities

Generate Report

Export PDF

Export Excel

Export CSV

Public Methods

```
GenerateReport()

ExportPDF()

ExportExcel()

ExportCSV()
```

---

# Import Data Object

All modules exchange one common object.

```
ImportContext
```

Contains

Project

Machine

Material

Standard

Specimen

Units

RawData

EngineeringData

Warnings

Errors

Audit

---

# Return Values

Every public method returns

```
Success

Warning

Error

Cancelled
```

Never Boolean only.

---

# Error Propagation

Parser

↓

Validation

↓

Controller

↓

Ribbon

No module displays MessageBox directly.

Only Controller communicates with UI.

---

# Thread Model

Current Version

Single Thread

Future

Background Worker

Reserved

---

# Logging

Every API call logs

Module

Method

Execution Time

Result

Operator

Timestamp

---

# Dependency Rules

Parser

Must NOT know

Engineering

Graph

Report

Engineering

Must NOT know

Ribbon

Parser

Graph

Must NOT know

Parser

SQLite

Only Engineering Dataset

---

# Future Expansion

REST API

PLC API

Python API

Web API

Cloud API

Reserved

---

# Acceptance Criteria

✔ Loose coupling

✔ Independent modules

✔ No circular dependency

✔ Common ImportContext object

✔ Excel 2019 VBA compatible

✔ Future migration to VB.NET possible

---

End of Document
